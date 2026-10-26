---
title: "Converter Imagem em Texto"
seoTitle: "Converter Imagem em Texto"
description: "Converter Imagem em Texto: extraia o texto de uma imagem com OCR. Grátis e online, sem cadastro."
summary: "Extraia o texto de uma imagem com OCR."
date: 2026-10-26
draft: false
category: "midia"
tags: ["imagens", "ocr", "texto"]
keywords: ["converter imagem em texto", "converter imagem em texto online", "imagens", "ocr", "texto"]
---
<!--sudah dikerjakan-->

Basta escolher a imagem com texto abaixo, selecionar o idioma e depois clicar em **Converter em Texto**.

<div id="calc-imagem-texto" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🖼️ Converter Imagem em Texto</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Envie uma imagem e extraia o texto com OCR, direto no navegador.</p>
<label for="img-arquivo" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Imagem com texto</label>
<input id="img-arquivo" type="file" accept=".jpg,.jpeg,.png,.bmp,.pbm,image/jpeg,image/png,image/bmp" style="width:100%;padding:12px 14px;margin-bottom:6px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;cursor:pointer;">
<p style="margin:0 0 16px;font-size:0.8rem;color:#64748b;">Formatos aceitos: JPG, PNG, BMP e PBM.</p>
<div id="img-previa-box" style="display:none;margin-bottom:16px;padding:10px;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;text-align:center;">
<img id="img-previa" alt="Prévia da imagem enviada" style="max-width:100%;max-height:240px;border-radius:6px;">
</div>
<label for="img-idioma" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Idioma do texto</label>
<select id="img-idioma" style="width:100%;padding:12px 14px;margin-bottom:20px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<option value="por">Português</option>
<option value="eng">Inglês</option>
<option value="spa">Espanhol</option>
</select>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="img-converter" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Converter em Texto</button>
<button type="button" id="img-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="img-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="img-status">escolha uma imagem e clique em "Converter em Texto".</span></div>
<label for="img-texto" style="display:block;margin:20px 0 6px;font-weight:600;font-size:0.95rem;">Resultado</label>
<textarea id="img-texto" rows="8" placeholder="O texto extraído aparecerá aqui." style="width:100%;padding:12px 14px;margin-bottom:12px;font-size:1rem;font-family:inherit;line-height:1.5;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;resize:vertical;"></textarea>
<button type="button" id="img-copiar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Copiar texto</button>
</div>
<script>
(function () {
  var LIB_URL = 'https://cdn.jsdelivr.net/npm/tesseract.js@5.1.1/dist/tesseract.min.js';
  var arquivo = document.getElementById('img-arquivo');
  var idioma = document.getElementById('img-idioma');
  var previa = document.getElementById('img-previa');
  var previaBox = document.getElementById('img-previa-box');
  var texto = document.getElementById('img-texto');
  var status = document.getElementById('img-status');
  var caixa = document.getElementById('img-resposta');
  var btnConverter = document.getElementById('img-converter');
  var btnLimpar = document.getElementById('img-limpar');
  var btnCopiar = document.getElementById('img-copiar');
  var urlPrevia = null;
  var ocupado = false;
  function mostrar(tipo, msg) {
    var cores = {
      neutro: ['#c7d2fe', '#ffffff', '#64748b'],
      info: ['#a5b4fc', '#eef2ff', '#3730a3'],
      ok: ['#86efac', '#f0fdf4', '#166534'],
      erro: ['#fca5a5', '#fef2f2', '#b91c1c']
    };
    var c = cores[tipo] || cores.neutro;
    caixa.style.borderColor = c[0];
    caixa.style.background = c[1];
    status.style.color = c[2];
    status.textContent = msg;
  }
  function carregarLib() {
    return new Promise(function (resolve, reject) {
      if (window.Tesseract) { resolve(window.Tesseract); return; }
      var s = document.createElement('script');
      s.src = LIB_URL;
      s.async = true;
      s.onload = function () {
        if (window.Tesseract) { resolve(window.Tesseract); } else { reject(new Error('lib')); }
      };
      s.onerror = function () { reject(new Error('lib')); };
      document.head.appendChild(s);
    });
  }
  function atualizarPrevia() {
    if (urlPrevia) { URL.revokeObjectURL(urlPrevia); urlPrevia = null; }
    var f = arquivo.files && arquivo.files[0];
    if (!f) { previaBox.style.display = 'none'; previa.removeAttribute('src'); return; }
    urlPrevia = URL.createObjectURL(f);
    previa.onerror = function () { previaBox.style.display = 'none'; };
    previa.onload = function () { previaBox.style.display = 'block'; };
    previa.src = urlPrevia;
  }
  function converter() {
    if (ocupado) { return; }
    var f = arquivo.files && arquivo.files[0];
    if (!f) { mostrar('erro', 'escolha uma imagem nos formatos JPG, PNG, BMP ou PBM.'); return; }
    if (!/\.(jpe?g|png|bmp|pbm)$/i.test(f.name)) { mostrar('erro', 'formato não aceito. Use JPG, PNG, BMP ou PBM.'); return; }
    if (f.size > 10 * 1024 * 1024) { mostrar('erro', 'a imagem deve ter no máximo 10 MB.'); return; }
    ocupado = true;
    btnConverter.disabled = true;
    btnConverter.style.opacity = '0.6';
    texto.value = '';
    mostrar('info', 'carregando o leitor de texto (OCR)...');
    var worker = null;
    carregarLib().then(function (T) {
      mostrar('info', 'preparando o idioma selecionado...');
      return T.createWorker(idioma.value, 1, {
        logger: function (m) {
          if (m && m.status === 'recognizing text') {
            mostrar('info', 'reconhecendo o texto... ' + Math.round(m.progress * 100) + '%');
          }
        }
      });
    }).then(function (w) {
      worker = w;
      return worker.recognize(f);
    }).then(function (r) {
      var t = String((r && r.data && r.data.text) || '').trim();
      if (t === '') {
        mostrar('erro', 'nenhum texto foi encontrado na imagem. Tente uma imagem mais nítida ou outro idioma.');
      } else {
        texto.value = t;
        mostrar('ok', 'texto extraído com sucesso!');
      }
    }).catch(function (e) {
      if (e && e.message === 'lib') {
        mostrar('erro', 'não foi possível carregar o leitor de OCR. Verifique sua conexão e tente novamente.');
      } else {
        mostrar('erro', 'não foi possível ler esta imagem. Tente outro arquivo ou formato.');
      }
    }).then(function () {
      if (worker) { try { worker.terminate(); } catch (e) {} }
      ocupado = false;
      btnConverter.disabled = false;
      btnConverter.style.opacity = '1';
    });
  }
  function copiar() {
    if (texto.value === '') { mostrar('erro', 'não há texto para copiar.'); return; }
    function fallback() {
      texto.select();
      try { document.execCommand('copy'); mostrar('ok', 'texto copiado!'); } catch (e) { mostrar('erro', 'não foi possível copiar. Selecione o texto e copie manualmente.'); }
    }
    if (navigator.clipboard && navigator.clipboard.writeText) {
      navigator.clipboard.writeText(texto.value).then(function () { mostrar('ok', 'texto copiado!'); }, fallback);
    } else {
      fallback();
    }
  }
  function limpar() {
    arquivo.value = '';
    texto.value = '';
    idioma.value = 'por';
    atualizarPrevia();
    mostrar('neutro', 'escolha uma imagem e clique em "Converter em Texto".');
  }
  btnConverter.addEventListener('click', converter);
  btnLimpar.addEventListener('click', limpar);
  btnCopiar.addEventListener('click', copiar);
  arquivo.addEventListener('change', atualizarPrevia);
  [arquivo, idioma, texto].forEach(function (el) {
    el.addEventListener('focus', function () { el.style.borderColor = '#6366f1'; });
    el.addEventListener('blur', function () { el.style.borderColor = '#c7d2fe'; });
  });
})();
</script>

## Como usar a ferramenta

1. Clique em **Imagem com texto** e escolha o arquivo no seu dispositivo (JPG, PNG, BMP ou PBM).
2. Confira a prévia da imagem que aparece abaixo do campo.
3. Selecione o **Idioma do texto** que está na imagem: Português, Inglês ou Espanhol.
4. Clique em **Converter em Texto** e aguarde o progresso chegar a 100%.
5. Leia o texto no campo **Resultado** e use **Copiar texto** para levá-lo para outro lugar.
6. Use o botão **Limpar** para apagar tudo e converter uma nova imagem.

A leitura é feita no próprio navegador. Na primeira conversão, o leitor de OCR e os dados do idioma são baixados, então a primeira vez pode demorar um pouco mais. Imagens nítidas, com boa iluminação e texto reto, dão os melhores resultados.

## Entendendo os termos

- **OCR:** sigla de Reconhecimento Óptico de Caracteres. Tecnologia que identifica letras e números em uma imagem e os transforma em texto que pode ser editado e copiado.
- **Imagem com texto:** foto, captura de tela ou digitalização que contém palavras, como um documento, uma placa ou uma página de livro.
- **JPG:** formato de imagem comum em fotos, com arquivos leves e compressão que pode reduzir a qualidade.
- **PNG:** formato de imagem sem perda de qualidade, muito usado em capturas de tela e ideal para textos nítidos.
- **BMP:** formato de imagem simples e sem compressão, que gera arquivos grandes.
- **PBM:** formato de imagem em preto e branco, muito simples, usado principalmente em ferramentas técnicas.
- **Idioma do texto:** língua em que o texto da imagem foi escrito. Escolher o idioma certo ajuda o OCR a reconhecer acentos e palavras corretamente.
- **Resultado:** texto extraído da imagem, que você pode revisar, editar e copiar.
- **Prévia:** miniatura da imagem escolhida, usada para conferir se o arquivo é o correto antes de converter.