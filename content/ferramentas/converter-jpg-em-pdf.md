---
title: "Converter JPG em PDF"
seoTitle: "Converter JPG em PDF"
description: "Converter JPG em PDF: junte imagens JPG em um arquivo PDF. Grátis e online, sem cadastro."
summary: "Junte imagens JPG em um arquivo PDF."
date: 2026-10-26
draft: false
category: "midia"
tags: ["pdf", "imagens", "conversão", "edição de pdf"]
keywords: ["converter jpg em pdf", "converter jpg em pdf online", "pdf", "imagens", "conversão"]
---

<!--sudah dikerjakan-->

Basta selecionar as imagens JPG, escolher a orientação e as margens e depois clicar em **Converter**.

<div id="conv-jpg-pdf" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🖼️ Converter JPG em PDF</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Selecione as imagens e gere um único arquivo PDF. Tudo é feito no seu navegador.</p>
<label for="jpg-arquivos" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Imagens JPG</label>
<input id="jpg-arquivos" type="file" accept=".jpg,.jpeg,image/jpeg" multiple style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px dashed #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;cursor:pointer;">
<div id="jpg-lista" style="margin-bottom:16px;"></div>
<div style="display:flex;gap:12px;flex-wrap:wrap;margin-bottom:20px;">
<div style="flex:1;min-width:150px;">
<label for="jpg-orientacao" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Orientação</label>
<select id="jpg-orientacao" style="width:100%;padding:12px 14px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<option value="retrato">Retrato</option>
<option value="paisagem">Paisagem</option>
</select>
</div>
<div style="flex:1;min-width:150px;">
<label for="jpg-margem" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Margens</label>
<select id="jpg-margem" style="width:100%;padding:12px 14px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<option value="sem">Sem Margens</option>
<option value="com">Com Margens</option>
</select>
</div>
</div>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="jpg-converter" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Converter</button>
<button type="button" id="jpg-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="jpg-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="jpg-resultado">selecione as imagens JPG e clique em "Converter".</span><div id="jpg-download" style="margin-top:12px;"></div></div>
</div>
<script>
(function () {
  var ABRE = String.fromCharCode(60, 60);
  var FECHA = String.fromCharCode(62, 62);
  var arquivos = document.getElementById('jpg-arquivos');
  var orientacao = document.getElementById('jpg-orientacao');
  var margem = document.getElementById('jpg-margem');
  var lista = document.getElementById('jpg-lista');
  var caixa = document.getElementById('jpg-resposta');
  var resultado = document.getElementById('jpg-resultado');
  var download = document.getElementById('jpg-download');
  var btnConverter = document.getElementById('jpg-converter');
  var btnLimpar = document.getElementById('jpg-limpar');
  var itens = [];
  var urlPdf = null;
  var ocupado = false;
  var TEXTO_INICIAL = 'selecione as imagens JPG e clique em "Converter".';
  var CORES = {
    neutro: ['#c7d2fe', '#ffffff', '#64748b'],
    ok: ['#86efac', '#f0fdf4', '#166534'],
    erro: ['#fca5a5', '#fef2f2', '#b91c1c']
  };
  function mensagem(texto, tipo) {
    var c = CORES[tipo];
    caixa.style.borderColor = c[0];
    caixa.style.background = c[1];
    resultado.style.color = c[2];
    resultado.textContent = texto;
  }
  function limparDownload() {
    download.textContent = '';
    if (urlPdf) { URL.revokeObjectURL(urlPdf); urlPdf = null; }
  }
  function tamanho(n) {
    return Math.max(1, Math.round(n / 1024)).toLocaleString('pt-BR') + ' KB';
  }
  function botaoMini(rotulo, titulo, desativado, acao) {
    var b = document.createElement('button');
    b.type = 'button';
    b.textContent = rotulo;
    b.title = titulo;
    b.disabled = desativado;
    b.style.cssText = 'padding:4px 9px;font-size:0.9rem;font-weight:700;color:#4f46e5;background:#ffffff;border:1px solid #c7d2fe;border-radius:8px;cursor:pointer;opacity:' + (desativado ? '0.4' : '1') + ';';
    b.addEventListener('click', acao);
    return b;
  }
  function desenharLista() {
    lista.textContent = '';
    if (itens.length === 0) { return; }
    itens.forEach(function (item, i) {
      var linha = document.createElement('div');
      linha.style.cssText = 'display:flex;align-items:center;gap:6px;padding:8px 10px;margin-bottom:6px;background:#ffffff;border:1px solid #c7d2fe;border-radius:10px;font-size:0.9rem;';
      var nome = document.createElement('span');
      nome.style.cssText = 'flex:1;min-width:0;overflow:hidden;text-overflow:ellipsis;white-space:nowrap;';
      nome.textContent = (i + 1) + '. ' + item.file.name + ' (' + tamanho(item.file.size) + ')';
      linha.appendChild(nome);
      linha.appendChild(botaoMini('↑', 'Mover para cima', i === 0, function () {
        var t = itens[i]; itens[i] = itens[i - 1]; itens[i - 1] = t;
        limparDownload(); desenharLista();
      }));
      linha.appendChild(botaoMini('↓', 'Mover para baixo', i === itens.length - 1, function () {
        var t = itens[i]; itens[i] = itens[i + 1]; itens[i + 1] = t;
        limparDownload(); desenharLista();
      }));
      linha.appendChild(botaoMini('✕', 'Remover', false, function () {
        itens.splice(i, 1);
        limparDownload(); desenharLista();
      }));
      lista.appendChild(linha);
    });
  }
  function adicionar() {
    var recebidos = Array.prototype.slice.call(arquivos.files);
    var ignorados = 0;
    recebidos.forEach(function (f) {
      if (/\.jpe?g$/i.test(f.name) || f.type === 'image/jpeg') { itens.push({ file: f }); }
      else { ignorados++; }
    });
    arquivos.value = '';
    limparDownload();
    desenharLista();
    if (ignorados !== 0) { mensagem(ignorados + ' arquivo(s) ignorado(s): use apenas imagens JPG.', 'erro'); }
    else { mensagem(itens.length + ' imagem(ns) na lista. Ajuste a ordem se precisar e clique em "Converter".', 'neutro'); }
  }
  function carregar(file) {
    return new Promise(function (resolve, reject) {
      var url = URL.createObjectURL(file);
      var img = new Image();
      img.onload = function () {
        var w = img.naturalWidth;
        var h = img.naturalHeight;
        var esc = Math.min(1, 3000 / Math.max(w, h));
        var cw = Math.max(1, Math.round(w * esc));
        var ch = Math.max(1, Math.round(h * esc));
        var cv = document.createElement('canvas');
        cv.width = cw;
        cv.height = ch;
        var ctx = cv.getContext('2d');
        ctx.fillStyle = '#ffffff';
        ctx.fillRect(0, 0, cw, ch);
        ctx.drawImage(img, 0, 0, cw, ch);
        URL.revokeObjectURL(url);
        var bin = atob(cv.toDataURL('image/jpeg', 0.92).split(',')[1]);
        var bytes = new Uint8Array(bin.length);
        for (var k = 0; k !== bin.length; k++) { bytes[k] = bin.charCodeAt(k); }
        resolve({ w: cw, h: ch, bytes: bytes });
      };
      img.onerror = function () {
        URL.revokeObjectURL(url);
        reject(new Error(file.name));
      };
      img.src = url;
    });
  }
  function montarPdf(imagens, paisagem, comMargem) {
    var pw = paisagem ? 841.89 : 595.28;
    var ph = paisagem ? 595.28 : 841.89;
    var m = comMargem ? 36 : 0;
    var partes = [];
    var pos = 0;
    var offsets = [];
    var n = imagens.length;
    var total = 2 + 3 * n;
    function f(x) { return x.toFixed(2); }
    function bytesDe(s) {
      var b = new Uint8Array(s.length);
      for (var k = 0; k !== s.length; k++) { b[k] = s.charCodeAt(k) & 255; }
      return b;
    }
    function add(x) {
      var b = (typeof x === 'string') ? bytesDe(x) : x;
      partes.push(b);
      pos += b.length;
    }
    function objeto(id, corpo) {
      offsets[id] = pos;
      add(id + ' 0 obj\n' + corpo + '\nendobj\n');
    }
    add(new Uint8Array([37, 80, 68, 70, 45, 49, 46, 52, 10, 37, 226, 227, 207, 211, 10]));
    objeto(1, ABRE + ' /Type /Catalog /Pages 2 0 R ' + FECHA);
    var kids = [];
    imagens.forEach(function (im, i) { kids.push((3 + 3 * i) + ' 0 R'); });
    objeto(2, ABRE + ' /Type /Pages /Count ' + n + ' /Kids [' + kids.join(' ') + '] ' + FECHA);
    imagens.forEach(function (im, i) {
      var idPagina = 3 + 3 * i;
      var idConteudo = idPagina + 1;
      var idImagem = idPagina + 2;
      var esc = Math.min((pw - 2 * m) / im.w, (ph - 2 * m) / im.h);
      var iw = im.w * esc;
      var ih = im.h * esc;
      var x = (pw - iw) / 2;
      var y = (ph - ih) / 2;
      var cs = 'q ' + f(iw) + ' 0 0 ' + f(ih) + ' ' + f(x) + ' ' + f(y) + ' cm /Im0 Do Q';
      objeto(idPagina, ABRE + ' /Type /Page /Parent 2 0 R /MediaBox [0 0 ' + f(pw) + ' ' + f(ph) + '] /Resources ' + ABRE + ' /XObject ' + ABRE + ' /Im0 ' + idImagem + ' 0 R ' + FECHA + ' ' + FECHA + ' /Contents ' + idConteudo + ' 0 R ' + FECHA);
      objeto(idConteudo, ABRE + ' /Length ' + cs.length + ' ' + FECHA + '\nstream\n' + cs + '\nendstream');
      offsets[idImagem] = pos;
      add(idImagem + ' 0 obj\n' + ABRE + ' /Type /XObject /Subtype /Image /Width ' + im.w + ' /Height ' + im.h + ' /ColorSpace /DeviceRGB /BitsPerComponent 8 /Filter /DCTDecode /Length ' + im.bytes.length + ' ' + FECHA + '\nstream\n');
      add(im.bytes);
      add('\nendstream\nendobj\n');
    });
    var inicioXref = pos;
    var xref = 'xref\n0 ' + (total + 1) + '\n0000000000 65535 f \n';
    for (var id = 1; id !== total + 1; id++) {
      xref += ('0000000000' + offsets[id]).slice(-10) + ' 00000 n \n';
    }
    xref += 'trailer\n' + ABRE + ' /Size ' + (total + 1) + ' /Root 1 0 R ' + FECHA + '\nstartxref\n' + inicioXref + '\n%%EOF';
    add(xref);
    return new Blob(partes, { type: 'application/pdf' });
  }
  async function converter() {
    if (ocupado) { return; }
    if (itens.length === 0) { mensagem('selecione ao menos uma imagem JPG.', 'erro'); return; }
    ocupado = true;
    btnConverter.disabled = true;
    btnConverter.style.opacity = '0.6';
    limparDownload();
    try {
      var imagens = [];
      for (var i = 0; i !== itens.length; i++) {
        mensagem('processando imagem ' + (i + 1) + ' de ' + itens.length + '...', 'neutro');
        imagens.push(await carregar(itens[i].file));
      }
      var blob = montarPdf(imagens, orientacao.value === 'paisagem', margem.value === 'com');
      urlPdf = URL.createObjectURL(blob);
      mensagem('PDF criado com ' + imagens.length + ' página(s) (' + tamanho(blob.size) + ').', 'ok');
      var link = document.createElement('a');
      link.href = urlPdf;
      link.download = 'imagens.pdf';
      link.textContent = '⬇ Baixar PDF';
      link.style.cssText = 'display:inline-block;padding:11px 18px;font-size:1rem;font-weight:700;color:#ffffff;text-decoration:none;background:linear-gradient(135deg,#4f46e5,#6366f1);border-radius:10px;box-shadow:0 4px 12px rgba(79,70,229,0.35);';
      download.appendChild(link);
    } catch (e) {
      mensagem('não foi possível ler a imagem ' + (e && e.message ? e.message : '') + '. Verifique se o arquivo é um JPG válido.', 'erro');
    } finally {
      ocupado = false;
      btnConverter.disabled = false;
      btnConverter.style.opacity = '1';
    }
  }
  function limpar() {
    itens = [];
    arquivos.value = '';
    limparDownload();
    desenharLista();
    mensagem(TEXTO_INICIAL, 'neutro');
  }
  arquivos.addEventListener('change', adicionar);
  btnConverter.addEventListener('click', converter);
  btnLimpar.addEventListener('click', limpar);
  [orientacao, margem].forEach(function (el) {
    el.addEventListener('change', limparDownload);
    el.addEventListener('focus', function () { el.style.borderColor = '#6366f1'; });
    el.addEventListener('blur', function () { el.style.borderColor = '#c7d2fe'; });
  });
})();
</script>

## Como usar o conversor

1. Clique em **Imagens JPG** e selecione uma ou mais imagens do seu dispositivo.
2. Confira a lista: use os botões **↑** e **↓** para mudar a ordem das páginas e **✕** para remover uma imagem.
3. Escolha a **Orientação** da página: **Retrato** ou **Paisagem**.
4. Escolha as **Margens**: **Sem Margens** ou **Com Margens**.
5. Clique em **Converter** e, quando o PDF ficar pronto, clique em **Baixar PDF**.
6. Use o botão **Limpar** para apagar a lista e começar uma nova conversão.

Cada imagem vira uma página do PDF, na mesma ordem da lista. A conversão acontece no seu próprio navegador: as imagens não são enviadas para nenhum servidor.

## Entendendo os termos

- **JPG (ou JPEG):** formato de imagem muito comum em fotos e capturas, que reduz o tamanho do arquivo com compressão.
- **PDF:** formato de documento que mantém o mesmo visual em qualquer dispositivo, ideal para compartilhar e imprimir.
- **Conversão:** processo de transformar um arquivo de um formato em outro, aqui de imagens JPG em um único PDF.
- **Orientação:** direção da página do PDF, que pode ser em pé (retrato) ou deitada (paisagem).
- **Retrato:** página vertical, mais alta do que larga. Boa para fotos em pé e documentos escaneados.
- **Paisagem:** página horizontal, mais larga do que alta. Boa para fotos deitadas e capturas de tela.
- **Margens:** espaço em branco entre a borda da página e a imagem.
- **Sem Margens:** a imagem ocupa o máximo possível da página, sem espaço em branco nas bordas.
- **Com Margens:** a imagem fica centralizada, com um espaço livre ao redor, como em um documento impresso.
- **Página A4:** tamanho padrão do PDF gerado (210 × 297 mm). A imagem é ajustada para caber inteira na página, sem distorcer.