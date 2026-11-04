---
title: "Juntar PDF"
seoTitle: "Juntar PDF"
description: "Juntar PDF: una vários arquivos PDF em um só. Grátis e online, sem cadastro."
summary: "Una vários arquivos PDF em um só."
date: 2026-11-04
draft: false
category: "midia"
tags: ["pdf", "edição de pdf", "juntar"]
keywords: ["juntar pdf", "juntar pdf online", "pdf", "edição de pdf", "juntar"]
---

Basta selecionar (ou arrastar) os arquivos PDF abaixo, organizar a ordem e depois clicar em **Juntar PDF**.

<div id="juntar-pdf" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">📄 Juntar PDF</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Escolha os arquivos, defina a ordem e baixe um único PDF.</p>
<input id="pdf-arquivos" type="file" accept="application/pdf,.pdf" multiple style="display:none;">
<div id="pdf-zona" role="button" tabindex="0" aria-label="Selecionar arquivos PDF" style="padding:22px 16px;margin-bottom:16px;text-align:center;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:0.95rem;line-height:1.5;cursor:pointer;box-sizing:border-box;outline:none;">
<strong style="color:#3730a3;">Clique para selecionar</strong> ou arraste os PDFs até aqui
</div>
<div id="pdf-lista" style="display:none;margin-bottom:8px;"></div>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="pdf-juntar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Juntar PDF</button>
<button type="button" id="pdf-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="pdf-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="pdf-resultado">selecione os arquivos PDF e clique em "Juntar PDF".</span></div>
</div>
<script>
(function () {
  var LIBS = [
    'https://cdnjs.cloudflare.com/ajax/libs/pdf-lib/1.17.1/pdf-lib.min.js',
    'https://cdn.jsdelivr.net/npm/pdf-lib@1.17.1/dist/pdf-lib.min.js'
  ];
  var entrada = document.getElementById('pdf-arquivos');
  var zona = document.getElementById('pdf-zona');
  var lista = document.getElementById('pdf-lista');
  var botaoJuntar = document.getElementById('pdf-juntar');
  var botaoLimpar = document.getElementById('pdf-limpar');
  var caixa = document.getElementById('pdf-resposta');
  var resultado = document.getElementById('pdf-resultado');
  var MSG_INICIAL = 'selecione os arquivos PDF e clique em "Juntar PDF".';
  var STYLE_ICONE = 'width:32px;height:32px;padding:0;font-size:0.95rem;font-weight:700;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:8px;cursor:pointer;flex:none;';
  var arquivos = [];
  var urlAtual = null;
  var promessaLib = null;
  var ocupado = false;
  function criar(tag, css, texto) {
    var e = document.createElement(tag);
    if (css) { e.style.cssText = css; }
    if (texto !== undefined) { e.textContent = texto; }
    return e;
  }
  function tamanho(bytes) {
    if (bytes >= 1048576) { return (bytes / 1048576).toLocaleString('pt-BR', { maximumFractionDigits: 2 }) + ' MB'; }
    return Math.max(1, Math.round(bytes / 1024)).toLocaleString('pt-BR') + ' KB';
  }
  function estado(tipo, mensagem) {
    var cores = {
      neutro: ['#c7d2fe', '#ffffff', '#64748b', 'dashed'],
      ok: ['#86efac', '#f0fdf4', '#166534', 'solid'],
      erro: ['#fca5a5', '#fef2f2', '#b91c1c', 'solid']
    };
    var c = cores[tipo];
    caixa.style.borderColor = c[0];
    caixa.style.background = c[1];
    caixa.style.borderStyle = c[3];
    resultado.style.color = c[2];
    resultado.textContent = mensagem;
  }
  function carregarLib() {
    if (window.PDFLib) { return Promise.resolve(window.PDFLib); }
    if (promessaLib) { return promessaLib; }
    promessaLib = new Promise(function (resolve, reject) {
      var i = 0;
      function tentar() {
        if (i === LIBS.length) { promessaLib = null; reject(new Error('LIB')); return; }
        var s = document.createElement('script');
        s.src = LIBS[i];
        i += 1;
        s.onload = function () {
          if (window.PDFLib) { resolve(window.PDFLib); } else { tentar(); }
        };
        s.onerror = function () {
          if (s.parentNode) { s.parentNode.removeChild(s); }
          tentar();
        };
        document.head.appendChild(s);
      }
      tentar();
    });
    return promessaLib;
  }
  function revogarUrl() {
    if (urlAtual) { URL.revokeObjectURL(urlAtual); urlAtual = null; }
  }
  function desenhar() {
    while (lista.firstChild) { lista.removeChild(lista.firstChild); }
    if (arquivos.length === 0) { lista.style.display = 'none'; return; }
    lista.style.display = 'block';
    arquivos.forEach(function (f, i) {
      var linha = criar('div', 'display:flex;align-items:center;gap:8px;padding:10px 12px;margin-bottom:8px;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;box-sizing:border-box;');
      var num = criar('span', 'flex:none;width:24px;height:24px;border-radius:50%;background:#e0e7ff;color:#3730a3;font-size:0.8rem;font-weight:700;display:flex;align-items:center;justify-content:center;', String(i + 1));
      var nome = criar('span', 'flex:1;min-width:0;overflow:hidden;text-overflow:ellipsis;white-space:nowrap;font-size:0.9rem;font-weight:600;', f.name);
      nome.title = f.name;
      var tam = criar('span', 'flex:none;font-size:0.8rem;color:#64748b;', tamanho(f.size));
      var subir = criar('button', STYLE_ICONE, '↑');
      var descer = criar('button', STYLE_ICONE, '↓');
      var remover = criar('button', STYLE_ICONE, '✕');
      subir.type = 'button';
      descer.type = 'button';
      remover.type = 'button';
      subir.setAttribute('aria-label', 'Mover para cima');
      descer.setAttribute('aria-label', 'Mover para baixo');
      remover.setAttribute('aria-label', 'Remover arquivo');
      if (i === 0) { subir.disabled = true; subir.style.opacity = '0.4'; subir.style.cursor = 'default'; }
      if (i === arquivos.length - 1) { descer.disabled = true; descer.style.opacity = '0.4'; descer.style.cursor = 'default'; }
      subir.addEventListener('click', function () { mover(i, -1); });
      descer.addEventListener('click', function () { mover(i, 1); });
      remover.addEventListener('click', function () { arquivos.splice(i, 1); aposMudanca(); });
      linha.appendChild(num);
      linha.appendChild(nome);
      linha.appendChild(tam);
      linha.appendChild(subir);
      linha.appendChild(descer);
      linha.appendChild(remover);
      lista.appendChild(linha);
    });
  }
  function mover(i, delta) {
    var j = i + delta;
    if (0 > j || j > arquivos.length - 1) { return; }
    var tmp = arquivos[i];
    arquivos[i] = arquivos[j];
    arquivos[j] = tmp;
    aposMudanca();
  }
  function aposMudanca() {
    revogarUrl();
    desenhar();
    estado('neutro', arquivos.length === 0 ? MSG_INICIAL : arquivos.length + ' arquivo(s) na lista. Ajuste a ordem e clique em "Juntar PDF".');
  }
  function adicionar(selecao) {
    var itens = Array.prototype.slice.call(selecao);
    var ignorados = 0;
    itens.forEach(function (f) {
      var ehPdf = f.type === 'application/pdf' || /\.pdf$/i.test(f.name);
      if (ehPdf) { arquivos.push(f); } else { ignorados += 1; }
    });
    aposMudanca();
    if (ignorados > 0) {
      estado('erro', ignorados + ' arquivo(s) ignorado(s): só são aceitos arquivos PDF.');
    }
    carregarLib().catch(function () {});
  }
  function juntar() {
    if (ocupado) { return; }
    if (2 > arquivos.length) { estado('erro', 'selecione pelo menos 2 arquivos PDF para juntar.'); return; }
    ocupado = true;
    botaoJuntar.disabled = true;
    botaoJuntar.style.opacity = '0.7';
    estado('neutro', 'juntando os arquivos, aguarde...');
    var paginas = 0;
    carregarLib().then(function (lib) {
      return lib.PDFDocument.create().then(function (saida) {
        var cadeia = Promise.resolve();
        arquivos.forEach(function (f) {
          cadeia = cadeia.then(function () {
            return f.arrayBuffer().then(function (buf) {
              return lib.PDFDocument.load(buf).catch(function () {
                throw new Error('ARQ:' + f.name);
              });
            }).then(function (doc) {
              return saida.copyPages(doc, doc.getPageIndices()).then(function (copias) {
                copias.forEach(function (p) { saida.addPage(p); });
              });
            });
          });
        });
        return cadeia.then(function () {
          paginas = saida.getPageCount();
          return saida.save();
        });
      });
    }).then(function (bytes) {
      revogarUrl();
      urlAtual = URL.createObjectURL(new Blob([bytes], { type: 'application/pdf' }));
      estado('ok', 'PDF criado com ' + paginas + ' página(s), a partir de ' + arquivos.length + ' arquivos.');
      var link = criar('a', 'display:inline-block;margin-top:12px;padding:11px 18px;font-size:0.95rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border-radius:10px;text-decoration:none;box-shadow:0 4px 12px rgba(79,70,229,0.35);', 'Baixar PDF unido');
      link.href = urlAtual;
      link.download = 'pdf-unido.pdf';
      resultado.appendChild(criar('br'));
      resultado.appendChild(link);
    }).catch(function (err) {
      var msg = String(err && err.message ? err.message : '');
      if (msg.indexOf('ARQ:') === 0) {
        estado('erro', 'não foi possível ler "' + msg.slice(4) + '". O arquivo pode estar protegido por senha ou corrompido.');
      } else if (msg === 'LIB') {
        estado('erro', 'não foi possível carregar o componente de PDF. Verifique sua conexão e tente novamente.');
      } else {
        estado('erro', 'ocorreu um erro ao juntar os arquivos. Tente novamente.');
      }
    }).then(function () {
      ocupado = false;
      botaoJuntar.disabled = false;
      botaoJuntar.style.opacity = '1';
    });
  }
  function limpar() {
    arquivos = [];
    entrada.value = '';
    revogarUrl();
    desenhar();
    estado('neutro', MSG_INICIAL);
  }
  zona.addEventListener('click', function () { entrada.click(); });
  zona.addEventListener('keydown', function (e) {
    if (e.key === 'Enter' || e.key === ' ') { e.preventDefault(); entrada.click(); }
  });
  zona.addEventListener('focus', function () { zona.style.borderColor = '#6366f1'; });
  zona.addEventListener('blur', function () { zona.style.borderColor = '#c7d2fe'; });
  zona.addEventListener('dragover', function (e) {
    e.preventDefault();
    zona.style.borderColor = '#6366f1';
    zona.style.background = '#eef2ff';
  });
  zona.addEventListener('dragleave', function () {
    zona.style.borderColor = '#c7d2fe';
    zona.style.background = '#ffffff';
  });
  zona.addEventListener('drop', function (e) {
    e.preventDefault();
    zona.style.borderColor = '#c7d2fe';
    zona.style.background = '#ffffff';
    if (e.dataTransfer && e.dataTransfer.files) { adicionar(e.dataTransfer.files); }
  });
  entrada.addEventListener('change', function () {
    adicionar(entrada.files);
    entrada.value = '';
  });
  botaoJuntar.addEventListener('click', juntar);
  botaoLimpar.addEventListener('click', limpar);
})();
</script>

## Como usar a ferramenta

1. Clique na área pontilhada para escolher os arquivos PDF no seu dispositivo, ou arraste-os até ela. Você pode selecionar vários de uma vez e adicionar mais arquivos depois.
2. Confira a lista: o número à esquerda mostra a posição de cada arquivo no PDF final.
3. Use os botões **↑** e **↓** para mudar a ordem e o botão **✕** para tirar um arquivo da lista.
4. Clique em **Juntar PDF** (são necessários pelo menos 2 arquivos).
5. Quando a mensagem de sucesso aparecer, clique em **Baixar PDF unido** para salvar o arquivo final.
6. Use o botão **Limpar** para esvaziar a lista e começar uma nova junção.

A junção é feita no seu próprio navegador: os arquivos não são enviados para nenhum servidor. PDFs protegidos por senha precisam ser desbloqueados antes de serem unidos.

## Entendendo os termos

- **PDF:** formato de documento (Portable Document Format) que mantém texto, imagens e layout iguais em qualquer dispositivo.
- **Juntar PDF:** unir dois ou mais arquivos PDF em um único documento, também chamado de mesclar ou combinar PDF.
- **Ordem dos arquivos:** sequência em que os PDFs aparecem na lista. É a mesma ordem das páginas no arquivo final.
- **Página:** cada folha de um documento PDF. O arquivo final contém todas as páginas dos arquivos originais, na ordem escolhida.
- **Arrastar e soltar:** forma de adicionar arquivos clicando sobre eles, arrastando até a área da ferramenta e soltando o botão do mouse.
- **PDF protegido por senha:** arquivo criptografado que exige senha para abrir. Ele precisa ser desbloqueado antes de ser juntado.
- **Tamanho do arquivo:** espaço que o arquivo ocupa, exibido em KB ou MB. O PDF final tem tamanho próximo à soma dos arquivos originais.
- **Download:** ato de salvar o arquivo gerado no seu dispositivo, neste caso o `pdf-unido.pdf`.