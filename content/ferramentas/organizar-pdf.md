---
title: "Organizar PDF"
seoTitle: "Organizar PDF"
description: "Organizar PDF: reordene, gire e remova páginas de um PDF. Grátis e online, sem cadastro."
summary: "Reordene, gire e remova páginas de um PDF."
date: 2026-11-06
draft: false
category: "midia"
tags: ["pdf", "edição de pdf"]
keywords: ["organizar pdf", "organizar pdf online", "pdf", "edição de pdf"]
---

Basta selecionar um ou mais arquivos PDF abaixo, organizar as páginas e depois clicar em **Organizar PDF** para baixar o resultado.

<div id="org-pdf" style="max-width:760px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">📄 Organizar PDF</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Adicione um ou mais PDFs, reordene, gire e remova páginas. Tudo é feito no seu navegador.</p>
<label for="org-arquivo" id="org-zona" style="display:block;padding:24px 16px;margin-bottom:16px;text-align:center;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;cursor:pointer;color:#64748b;font-size:0.95rem;line-height:1.6;box-sizing:border-box;"><strong style="color:#3730a3;">Clique para selecionar</strong> ou arraste seus arquivos PDF até aqui</label>
<input id="org-arquivo" type="file" accept="application/pdf,.pdf" multiple style="position:absolute;width:1px;height:1px;opacity:0;overflow:hidden;">
<div id="org-contador" aria-live="polite" style="margin-bottom:12px;font-size:0.9rem;font-weight:600;color:#475569;">0 arquivos • 0 páginas • 0 removidas</div>
<div id="org-grade" style="display:grid;grid-template-columns:repeat(auto-fill,minmax(150px,1fr));gap:12px;margin-bottom:20px;"></div>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="org-baixar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Organizar PDF</button>
<button type="button" id="org-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Resetar</button>
</div>
<div id="org-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="org-resultado">adicione um PDF para começar.</span></div>
</div>
<script>
(function () {
  var PDFJS_URL = 'https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.11.174/pdf.min.js';
  var WORKER_URL = 'https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.11.174/pdf.worker.min.js';
  var PDFLIB_URL = 'https://cdnjs.cloudflare.com/ajax/libs/pdf-lib/1.17.1/pdf-lib.min.js';
  var arquivo = document.getElementById('org-arquivo');
  var zona = document.getElementById('org-zona');
  var contador = document.getElementById('org-contador');
  var grade = document.getElementById('org-grade');
  var btnBaixar = document.getElementById('org-baixar');
  var btnLimpar = document.getElementById('org-limpar');
  var caixa = document.getElementById('org-resposta');
  var resultado = document.getElementById('org-resultado');
  var files = [];
  var pages = [];
  var dragIdx = -1;
  var uid = 0;
  var ocupado = false;
  var libsPromise = null;
  function carregar(src) {
    return new Promise(function (resolve, reject) {
      var s = document.createElement('script');
      s.src = src;
      s.onload = resolve;
      s.onerror = function () { reject(new Error('Falha ao carregar ' + src)); };
      document.head.appendChild(s);
    });
  }
  function libs() {
    if (!libsPromise) {
      libsPromise = Promise.all([carregar(PDFJS_URL), carregar(PDFLIB_URL)]).then(function () {
        window.pdfjsLib.GlobalWorkerOptions.workerSrc = WORKER_URL;
      }).catch(function (e) { libsPromise = null; throw e; });
    }
    return libsPromise;
  }
  function plural(n, s, p) { return n + ' ' + (n === 1 ? s : p); }
  function neutro(msg) {
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    resultado.style.color = '#64748b';
    resultado.textContent = msg;
  }
  function info(msg) { neutro(msg); }
  function erro(msg) {
    caixa.style.borderColor = '#fca5a5';
    caixa.style.background = '#fef2f2';
    resultado.style.color = '#b91c1c';
    resultado.textContent = msg;
  }
  function ok(msg) {
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    resultado.textContent = msg;
  }
  function atualizarContador() {
    var rem = pages.filter(function (p) { return p.removida; }).length;
    contador.textContent = plural(files.length, 'arquivo', 'arquivos') + ' • ' + plural(pages.length, 'página', 'páginas') + ' • ' + plural(rem, 'removida', 'removidas');
  }
  function botao(texto, titulo, fn) {
    var b = document.createElement('button');
    b.type = 'button';
    b.textContent = texto;
    b.title = titulo;
    b.setAttribute('aria-label', titulo);
    b.style.cssText = 'flex:1;padding:6px 0;font-size:0.9rem;font-weight:600;color:#4f46e5;background:#ffffff;border:1px solid #c7d2fe;border-radius:8px;cursor:pointer;';
    b.addEventListener('click', function (e) { e.stopPropagation(); fn(); });
    return b;
  }
  function mover(i, d) {
    var j = i + d;
    if (j < 0 || j >= pages.length) { return; }
    var t = pages[i];
    pages[i] = pages[j];
    pages[j] = t;
    render();
  }
  function bordaPadrao(p) { return p.removida ? '#fca5a5' : '#c7d2fe'; }
  function render() {
    grade.textContent = '';
    pages.forEach(function (p, i) {
      var card = document.createElement('div');
      card.draggable = true;
      card.style.cssText = 'padding:8px;background:#ffffff;border:2px solid ' + bordaPadrao(p) + ';border-radius:12px;box-sizing:border-box;cursor:grab;text-align:center;' + (p.removida ? 'opacity:0.5;' : '');
      var caixaImg = document.createElement('div');
      caixaImg.style.cssText = 'position:relative;height:150px;overflow:hidden;background:#f1f5f9;border-radius:8px;margin-bottom:6px;';
      var img = document.createElement('img');
      var girado = (p.rot % 180 !== 0);
      var rw = girado ? p.h : p.w;
      var rh = girado ? p.w : p.h;
      var esc = Math.min(134 / rw, 134 / rh);
      img.src = p.thumb;
      img.alt = 'Página ' + p.num + ' de ' + p.nome;
      img.draggable = false;
      img.style.cssText = 'position:absolute;left:50%;top:50%;max-width:none;box-shadow:0 2px 8px rgba(15,23,42,0.25);width:' + p.w + 'px;height:' + p.h + 'px;transform:translate(-50%,-50%) rotate(' + p.rot + 'deg) scale(' + esc + ');';
      caixaImg.appendChild(img);
      card.appendChild(caixaImg);
      var rotulo = document.createElement('div');
      rotulo.textContent = (i + 1) + '. ' + p.nome + ' • pág. ' + p.num;
      rotulo.title = rotulo.textContent;
      rotulo.style.cssText = 'margin-bottom:6px;font-size:0.75rem;color:#475569;white-space:nowrap;overflow:hidden;text-overflow:ellipsis;';
      card.appendChild(rotulo);
      var linha = document.createElement('div');
      linha.style.cssText = 'display:flex;gap:4px;';
      linha.appendChild(botao('◀', 'Mover para antes', function () { mover(i, -1); }));
      linha.appendChild(botao('↻', 'Girar 90°', function () { p.rot = (p.rot + 90) % 360; render(); }));
      linha.appendChild(botao(p.removida ? '↺' : '✕', p.removida ? 'Restaurar página' : 'Remover página', function () { p.removida = !p.removida; render(); }));
      linha.appendChild(botao('▶', 'Mover para depois', function () { mover(i, 1); }));
      card.appendChild(linha);
      card.addEventListener('dragstart', function (e) {
        dragIdx = i;
        try { e.dataTransfer.setData('text/plain', 'org-pdf'); } catch (x) {}
        e.dataTransfer.effectAllowed = 'move';
        card.style.opacity = '0.4';
      });
      card.addEventListener('dragend', function () { dragIdx = -1; render(); });
      card.addEventListener('dragover', function (e) {
        if (dragIdx > -1) { e.preventDefault(); card.style.borderColor = '#6366f1'; }
      });
      card.addEventListener('dragleave', function () { card.style.borderColor = bordaPadrao(p); });
      card.addEventListener('drop', function (e) {
        e.preventDefault();
        e.stopPropagation();
        if (dragIdx > -1 && dragIdx !== i) {
          var item = pages.splice(dragIdx, 1)[0];
          pages.splice(i, 0, item);
        }
        dragIdx = -1;
        render();
      });
      grade.appendChild(card);
    });
    atualizarContador();
  }
  async function adicionar(lista) {
    var arr = Array.prototype.slice.call(lista).filter(function (f) {
      return f.type === 'application/pdf' || /\.pdf$/i.test(f.name);
    });
    if (!arr.length) { erro('selecione arquivos no formato PDF.'); return; }
    if (ocupado) { return; }
    ocupado = true;
    try {
      await libs();
      for (var k = 0; k < arr.length; k++) {
        info('lendo ' + arr[k].name + '...');
        var buf = await arr[k].arrayBuffer();
        var pdf = await window.pdfjsLib.getDocument({ data: new Uint8Array(buf.slice(0)) }).promise;
        var fi = files.length;
        files.push({ nome: arr[k].name, bytes: buf });
        for (var n = 1; n <= pdf.numPages; n++) {
          var pg = await pdf.getPage(n);
          var v1 = pg.getViewport({ scale: 1 });
          var vp = pg.getViewport({ scale: 200 / Math.max(v1.width, v1.height) });
          var cv = document.createElement('canvas');
          cv.width = Math.max(1, Math.round(vp.width));
          cv.height = Math.max(1, Math.round(vp.height));
          await pg.render({ canvasContext: cv.getContext('2d'), viewport: vp }).promise;
          pages.push({ id: ++uid, f: fi, idx: n - 1, num: n, nome: arr[k].name, thumb: cv.toDataURL('image/jpeg', 0.75), w: cv.width, h: cv.height, rot: 0, removida: false });
        }
        render();
      }
      ok('arquivos adicionados. Arraste os cartões (ou use ◀ ▶) para reordenar, ↻ para girar e ✕ para remover.');
    } catch (e) {
      render();
      erro('não foi possível ler o PDF. Verifique se o arquivo não está corrompido ou protegido por senha, e se sua conexão permite carregar as bibliotecas.');
    } finally {
      ocupado = false;
      arquivo.value = '';
    }
  }
  async function baixar() {
    if (!pages.length) { erro('adicione pelo menos um arquivo PDF.'); return; }
    var ativas = pages.filter(function (p) { return !p.removida; });
    if (!ativas.length) { erro('todas as páginas foram removidas. Restaure ao menos uma página.'); return; }
    if (ocupado) { return; }
    ocupado = true;
    try {
      info('gerando o novo PDF...');
      await libs();
      var L = window.PDFLib;
      var saida = await L.PDFDocument.create();
      var cache = {};
      for (var i = 0; i < ativas.length; i++) {
        var p = ativas[i];
        if (!cache[p.f]) {
          cache[p.f] = await L.PDFDocument.load(files[p.f].bytes, { ignoreEncryption: true });
        }
        var copia = (await saida.copyPages(cache[p.f], [p.idx]))[0];
        copia.setRotation(L.degrees((copia.getRotation().angle + p.rot) % 360));
        saida.addPage(copia);
      }
      var bytes = await saida.save();
      var url = URL.createObjectURL(new Blob([bytes], { type: 'application/pdf' }));
      var a = document.createElement('a');
      a.href = url;
      a.download = 'pdf-organizado.pdf';
      document.body.appendChild(a);
      a.click();
      document.body.removeChild(a);
      setTimeout(function () { URL.revokeObjectURL(url); }, 3000);
      ok('PDF organizado com ' + plural(ativas.length, 'página', 'páginas') + '. O download foi iniciado.');
    } catch (e) {
      erro('não foi possível gerar o PDF. Tente novamente com outros arquivos.');
    } finally {
      ocupado = false;
    }
  }
  function limpar() {
    files = [];
    pages = [];
    dragIdx = -1;
    arquivo.value = '';
    render();
    neutro('adicione um PDF para começar.');
  }
  arquivo.addEventListener('change', function () { adicionar(arquivo.files); });
  arquivo.addEventListener('focus', function () { zona.style.borderColor = '#6366f1'; });
  arquivo.addEventListener('blur', function () { zona.style.borderColor = '#c7d2fe'; });
  zona.addEventListener('dragover', function (e) {
    if (dragIdx === -1) { e.preventDefault(); zona.style.borderColor = '#6366f1'; }
  });
  zona.addEventListener('dragleave', function () { zona.style.borderColor = '#c7d2fe'; });
  zona.addEventListener('drop', function (e) {
    e.preventDefault();
    zona.style.borderColor = '#c7d2fe';
    if (e.dataTransfer && e.dataTransfer.files && e.dataTransfer.files.length) { adicionar(e.dataTransfer.files); }
  });
  btnBaixar.addEventListener('click', baixar);
  btnLimpar.addEventListener('click', limpar);
  libs().catch(function () {});
})();
</script>

## Como usar a ferramenta

1. Clique na área pontilhada para selecionar um ou mais arquivos PDF, ou arraste os arquivos até ela.
2. Aguarde as miniaturas de todas as páginas aparecerem. Cada cartão mostra a posição, o nome do arquivo e o número da página original.
3. Para **reordenar**, arraste um cartão e solte sobre a posição desejada. Em celulares, use os botões **◀** e **▶**.
4. Para **girar**, clique em **↻**. Cada clique gira a página 90° no sentido horário.
5. Para **remover**, clique em **✕**. A página fica esmaecida e pode ser restaurada com **↺**.
6. Clique em **Organizar PDF** para gerar e baixar o novo arquivo com as páginas na ordem escolhida.
7. Use o botão **Resetar** para limpar tudo e começar de novo.

Se você adicionar vários PDFs, as páginas de todos eles ficam na mesma lista e podem ser misturadas livremente, o que também permite juntar documentos em um só arquivo. Os arquivos são processados no seu próprio navegador e não são enviados a nenhum servidor.

## Entendendo os termos

- **PDF:** formato de documento que mantém o mesmo layout em qualquer dispositivo ou programa. A sigla vem de Portable Document Format.
- **Página:** cada folha individual de um documento PDF.
- **Organizar PDF:** alterar a ordem, a orientação ou a quantidade de páginas de um arquivo sem precisar editar o conteúdo.
- **Reordenar:** mudar a posição das páginas, por exemplo, colocar a página 5 antes da página 2.
- **Rotacionar (girar):** virar a página em múltiplos de 90° para corrigir a orientação, como uma página escaneada de lado.
- **Remover:** excluir páginas em branco ou desnecessárias do arquivo final.
- **Juntar (mesclar):** combinar páginas de dois ou mais PDFs em um único documento.
- **Miniatura:** pré-visualização reduzida de uma página, usada para identificá-la rapidamente.
- **Arrastar e soltar:** gesto de clicar em um item, mover o mouse e soltar em outro lugar para mudar sua posição.