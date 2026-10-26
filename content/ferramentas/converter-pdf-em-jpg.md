---
title: "Converter PDF em JPG"
seoTitle: "Converter PDF em JPG"
description: "Converter PDF em JPG: transforme as páginas de um PDF em imagens JPG. Grátis e online, sem cadastro."
summary: "Transforme as páginas de um PDF em imagens JPG."
date: 2026-10-26
draft: false
category: "midia"
tags: ["pdf", "imagens", "conversão", "edição de pdf"]
keywords: ["converter pdf em jpg", "converter pdf em jpg online", "pdf", "imagens", "conversão"]
---

<!--sudah dikerjakan-->

Basta selecionar o arquivo PDF abaixo e depois clicar em **Converter para JPG**.

<div id="conv-pdf-jpg" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">📄 Converter PDF em JPG</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Escolha um PDF e receba cada página como imagem JPG.</p>
<label for="pj-arquivo" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Arquivo PDF</label>
<input id="pj-arquivo" type="file" accept="application/pdf,.pdf" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<label for="pj-qualidade" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Qualidade da imagem</label>
<select id="pj-qualidade" style="width:100%;padding:12px 14px;margin-bottom:20px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<option value="1.5">Normal (mais rápida)</option>
<option value="2" selected>Alta (recomendada)</option>
<option value="3">Máxima (arquivos maiores)</option>
</select>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="pj-converter" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Converter para JPG</button>
<button type="button" id="pj-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="pj-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="pj-resultado">selecione um PDF e clique em "Converter para JPG".</span></div>
<div id="pj-lista" style="display:grid;grid-template-columns:repeat(auto-fill,minmax(130px,1fr));gap:12px;margin-top:16px;"></div>
<button type="button" id="pj-zip" style="display:none;width:100%;margin-top:16px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Baixar todas as imagens (ZIP)</button>
</div>
<script>
(function () {
  var URL_PDFJS = 'https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.11.174/pdf.min.js';
  var URL_WORKER = 'https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.11.174/pdf.worker.min.js';
  var URL_ZIP = 'https://cdnjs.cloudflare.com/ajax/libs/jszip/3.10.1/jszip.min.js';
  var arquivo = document.getElementById('pj-arquivo');
  var qualidade = document.getElementById('pj-qualidade');
  var btnConverter = document.getElementById('pj-converter');
  var btnLimpar = document.getElementById('pj-limpar');
  var btnZip = document.getElementById('pj-zip');
  var caixa = document.getElementById('pj-resposta');
  var resultado = document.getElementById('pj-resultado');
  var lista = document.getElementById('pj-lista');
  var imagens = [];
  var ocupado = false;
  var promessas = {};
  function carregar(url) {
    if (promessas[url]) { return promessas[url]; }
    promessas[url] = new Promise(function (resolve, reject) {
      var s = document.createElement('script');
      s.src = url;
      s.onload = function () { resolve(); };
      s.onerror = function () { delete promessas[url]; reject(new Error('Falha ao carregar biblioteca.')); };
      document.head.appendChild(s);
    });
    return promessas[url];
  }
  function aviso(tipo, msg) {
    var cores = {
      ok: ['#86efac', '#f0fdf4', '#166534'],
      erro: ['#fca5a5', '#fef2f2', '#b91c1c'],
      info: ['#c7d2fe', '#ffffff', '#64748b']
    };
    var c = cores[tipo] || cores.info;
    caixa.style.borderColor = c[0];
    caixa.style.background = c[1];
    resultado.style.color = c[2];
    resultado.textContent = msg;
  }
  function limparLista() {
    imagens.forEach(function (img) { URL.revokeObjectURL(img.url); });
    imagens = [];
    lista.innerHTML = '';
    btnZip.style.display = 'none';
  }
  function baixar(url, nome) {
    var a = document.createElement('a');
    a.href = url;
    a.download = nome;
    document.body.appendChild(a);
    a.click();
    document.body.removeChild(a);
  }
  function adicionar(blob, nome, n) {
    var url = URL.createObjectURL(blob);
    imagens.push({ nome: nome, blob: blob, url: url });
    var item = document.createElement('div');
    item.style.cssText = 'padding:8px;background:#ffffff;border:1px solid #c7d2fe;border-radius:12px;text-align:center;box-sizing:border-box;';
    var img = document.createElement('img');
    img.src = url;
    img.alt = 'Página ' + n;
    img.style.cssText = 'width:100%;height:auto;border-radius:8px;border:1px solid #e2e8f0;display:block;margin-bottom:8px;';
    var legenda = document.createElement('div');
    legenda.textContent = 'Página ' + n;
    legenda.style.cssText = 'font-size:0.85rem;font-weight:600;color:#3730a3;margin-bottom:6px;';
    var link = document.createElement('button');
    link.type = 'button';
    link.textContent = 'Baixar JPG';
    link.style.cssText = 'width:100%;padding:8px 10px;font-size:0.85rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:8px;cursor:pointer;';
    link.addEventListener('click', function () { baixar(url, nome); });
    item.appendChild(img);
    item.appendChild(legenda);
    item.appendChild(link);
    lista.appendChild(item);
  }
  function paginas(pdf, n, escala, base) {
    if (n > pdf.numPages) { return Promise.resolve(); }
    return pdf.getPage(n).then(function (page) {
      var vp = page.getViewport({ scale: escala });
      var canvas = document.createElement('canvas');
      canvas.width = Math.floor(vp.width);
      canvas.height = Math.floor(vp.height);
      var ctx = canvas.getContext('2d');
      ctx.fillStyle = '#ffffff';
      ctx.fillRect(0, 0, canvas.width, canvas.height);
      return page.render({ canvasContext: ctx, viewport: vp }).promise.then(function () {
        return new Promise(function (resolve, reject) {
          canvas.toBlob(function (blob) {
            if (blob) { resolve(blob); } else { reject(new Error('Falha ao gerar a imagem.')); }
          }, 'image/jpeg', 0.92);
        });
      });
    }).then(function (blob) {
      adicionar(blob, base + '-pagina-' + n + '.jpg', n);
      aviso('info', 'convertendo... página ' + n + ' de ' + pdf.numPages + '.');
      return paginas(pdf, n + 1, escala, base);
    });
  }
  function converter() {
    if (ocupado) { return; }
    var f = arquivo.files && arquivo.files[0];
    if (!f) { aviso('erro', 'selecione um arquivo PDF.'); return; }
    if (f.type !== 'application/pdf' && !/\.pdf$/i.test(f.name)) { aviso('erro', 'o arquivo selecionado não é um PDF.'); return; }
    var escala = parseFloat(qualidade.value) || 2;
    var base = f.name.replace(/\.pdf$/i, '') || 'pdf';
    ocupado = true;
    btnConverter.disabled = true;
    limparLista();
    aviso('info', 'carregando o conversor...');
    carregar(URL_PDFJS).then(function () {
      window.pdfjsLib.GlobalWorkerOptions.workerSrc = URL_WORKER;
      return f.arrayBuffer();
    }).then(function (buf) {
      return window.pdfjsLib.getDocument({ data: new Uint8Array(buf) }).promise;
    }).then(function (pdf) {
      return paginas(pdf, 1, escala, base).then(function () {
        var total = pdf.numPages;
        aviso('ok', 'conversão concluída: ' + total + (total === 1 ? ' página convertida em JPG.' : ' páginas convertidas em JPG.'));
        if (total > 1) { btnZip.style.display = 'block'; }
      });
    }).catch(function (e) {
      limparLista();
      var nome = e && e.name ? e.name : '';
      if (nome === 'PasswordException') {
        aviso('erro', 'este PDF está protegido por senha.');
      } else if (nome === 'InvalidPDFException') {
        aviso('erro', 'não foi possível ler este PDF. O arquivo pode estar corrompido.');
      } else {
        aviso('erro', 'não foi possível converter o PDF. Verifique sua conexão e tente novamente.');
      }
    }).then(function () {
      ocupado = false;
      btnConverter.disabled = false;
    });
  }
  function baixarZip() {
    if (!imagens.length) { return; }
    btnZip.disabled = true;
    btnZip.textContent = 'Gerando ZIP...';
    carregar(URL_ZIP).then(function () {
      var zip = new window.JSZip();
      imagens.forEach(function (img) { zip.file(img.nome, img.blob); });
      return zip.generateAsync({ type: 'blob' });
    }).then(function (conteudo) {
      var url = URL.createObjectURL(conteudo);
      baixar(url, 'imagens-pdf-em-jpg.zip');
      setTimeout(function () { URL.revokeObjectURL(url); }, 10000);
    }).catch(function () {
      aviso('erro', 'não foi possível gerar o ZIP. Baixe as imagens uma a uma.');
    }).then(function () {
      btnZip.disabled = false;
      btnZip.textContent = 'Baixar todas as imagens (ZIP)';
    });
  }
  function limpar() {
    limparLista();
    arquivo.value = '';
    qualidade.value = '2';
    aviso('info', 'selecione um PDF e clique em "Converter para JPG".');
  }
  btnConverter.addEventListener('click', converter);
  btnLimpar.addEventListener('click', limpar);
  btnZip.addEventListener('click', baixarZip);
  [arquivo, qualidade].forEach(function (el) {
    el.addEventListener('focus', function () { el.style.borderColor = '#6366f1'; });
    el.addEventListener('blur', function () { el.style.borderColor = '#c7d2fe'; });
  });
})();
</script>

## Como usar o conversor

1. Clique em **Arquivo PDF** e escolha o documento que você quer converter.
2. Em **Qualidade da imagem**, selecione Normal, Alta ou Máxima. Quanto maior a qualidade, mais nítida a imagem e maior o arquivo.
3. Clique em **Converter para JPG** e aguarde. Cada página do PDF vira uma imagem JPG.
4. Use **Baixar JPG** para salvar uma página específica ou **Baixar todas as imagens (ZIP)** para levar todas de uma vez.
5. Clique em **Limpar** para remover as imagens e converter outro arquivo.

A conversão acontece no seu próprio navegador: o PDF não é enviado para nenhum servidor. PDFs protegidos por senha não podem ser convertidos.

## Entendendo os termos

- **PDF:** formato de documento que mantém texto, imagens e layout iguais em qualquer dispositivo.
- **JPG (ou JPEG):** formato de imagem muito usado na web e em celulares, com bom equilíbrio entre qualidade e tamanho do arquivo.
- **Conversão:** processo de transformar um arquivo de um formato em outro, aqui de PDF para JPG.
- **Página:** cada folha do PDF. O conversor gera uma imagem JPG para cada página.
- **Qualidade da imagem:** define o nível de detalhe da imagem gerada. Qualidade maior deixa textos e desenhos mais nítidos.
- **Pixel:** menor ponto de uma imagem. Quanto mais pixels, maior a resolução e o tamanho do arquivo.
- **ZIP:** arquivo compactado que reúne várias imagens em um único download.
- **Navegador:** programa que você usa para acessar sites, como Chrome, Firefox, Edge ou Safari.