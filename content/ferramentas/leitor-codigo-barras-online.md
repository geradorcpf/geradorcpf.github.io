---
title: "Leitor de Código de Barras Online"
seoTitle: "Leitor de Código de Barras Online"
description: "Leitor de Código de Barras Online: leia códigos de barras pela câmera ou por imagem. Grátis e online, sem cadastro."
summary: "Leia códigos de barras pela câmera ou por imagem."
date: 2026-11-04
draft: false
category: "midia"
tags: ["código de barras", "leitor", "códigos"]
keywords: ["leitor de código de barras online", "código de barras", "leitor", "códigos"]
---

Basta clicar em **Usar Câmera** ou **Enviar Imagem** abaixo para ler um código de barras ou QR Code na hora.

<div id="leitor-barras" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">📷 Leitor de Código de Barras Online</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Use a câmera ou envie uma imagem e veja o conteúdo do código.</p>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="lcb-camera" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Usar Câmera</button>
<button type="button" id="lcb-fechar" style="display:none;flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Fechar</button>
<label for="lcb-arquivo" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;text-align:center;box-sizing:border-box;">Enviar Imagem</label>
<input id="lcb-arquivo" type="file" accept="image/*" style="display:none;">
</div>
<div id="lcb-area-video" style="display:none;margin-top:16px;">
<video id="lcb-video" playsinline muted style="width:100%;max-height:320px;border-radius:12px;background:#000000;border:2px solid #c7d2fe;box-sizing:border-box;"></video>
</div>
<img id="lcb-preview" alt="Imagem enviada" style="display:none;max-width:100%;max-height:260px;margin-top:16px;border:2px solid #c7d2fe;border-radius:12px;box-sizing:border-box;">
<div id="lcb-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="lcb-resultado">clique em "Usar Câmera" ou "Enviar Imagem".</span></div>
</div>
<script>
(function () {
  var btnCamera = document.getElementById('lcb-camera');
  var btnFechar = document.getElementById('lcb-fechar');
  var arquivo = document.getElementById('lcb-arquivo');
  var areaVideo = document.getElementById('lcb-area-video');
  var video = document.getElementById('lcb-video');
  var preview = document.getElementById('lcb-preview');
  var caixa = document.getElementById('lcb-resposta');
  var resultado = document.getElementById('lcb-resultado');
  var canvas = document.createElement('canvas');
  var stream = null;
  var rodando = false;
  var detector = null;
  var usarNativo = ('BarcodeDetector' in window);
  var zxingPromise = null;
  function nomeFormato(f) {
    return String(f).replace(/_(\d)/g, '-$1').replace(/_/g, ' ').toUpperCase();
  }
  function info(msg) {
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    resultado.style.color = '#64748b';
    resultado.textContent = msg;
  }
  function erro(msg) {
    caixa.style.borderColor = '#fca5a5';
    caixa.style.background = '#fef2f2';
    resultado.style.color = '#b91c1c';
    resultado.textContent = msg;
  }
  function sucesso(formato, texto) {
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    resultado.textContent = '';
    var linhaFormato = document.createElement('span');
    linhaFormato.style.display = 'block';
    linhaFormato.style.fontSize = '0.85rem';
    linhaFormato.style.color = '#475569';
    linhaFormato.textContent = 'Formato: ' + nomeFormato(formato);
    var linhaTexto = document.createElement('span');
    linhaTexto.style.display = 'block';
    linhaTexto.style.fontWeight = '700';
    linhaTexto.style.fontSize = '1.15rem';
    linhaTexto.style.wordBreak = 'break-all';
    linhaTexto.textContent = texto;
    resultado.appendChild(linhaFormato);
    resultado.appendChild(linhaTexto);
  }
  function getDetector() {
    if (!detector) { detector = new window.BarcodeDetector(); }
    return detector;
  }
  function carregarZXing() {
    if (zxingPromise) { return zxingPromise; }
    zxingPromise = new Promise(function (ok, falha) {
      if (window.ZXing) { ok(); return; }
      var s = document.createElement('script');
      s.src = 'https://cdn.jsdelivr.net/npm/@zxing/library@0.21.3/umd/index.min.js';
      s.onload = function () { if (window.ZXing) { ok(); } else { zxingPromise = null; falha('carga'); } };
      s.onerror = function () { zxingPromise = null; falha('carga'); };
      document.head.appendChild(s);
    });
    return zxingPromise;
  }
  function detectarNativo(fonte) {
    return getDetector().detect(fonte).then(function (r) {
      return r.length > 0 ? { formato: r[0].format, texto: r[0].rawValue } : null;
    });
  }
  function detectarZXing(url) {
    return carregarZXing().then(function () {
      return new window.ZXing.BrowserMultiFormatReader().decodeFromImageUrl(url);
    }).then(function (res) {
      return { formato: window.ZXing.BarcodeFormat[res.getBarcodeFormat()], texto: res.getText() };
    });
  }
  function lerImagem(file) {
    fechar(true);
    var url = URL.createObjectURL(file);
    preview.src = url;
    preview.style.display = 'block';
    info('lendo a imagem...');
    var passo1 = usarNativo ? createImageBitmap(file).then(detectarNativo).catch(function () { return null; }) : Promise.resolve(null);
    passo1.then(function (achado) {
      return achado ? achado : detectarZXing(url);
    }).then(function (r) {
      sucesso(r.formato, r.texto);
    }).catch(function (e) {
      if (e === 'carga') {
        erro('não foi possível carregar o leitor. Verifique sua conexão e tente novamente.');
      } else {
        erro('nenhum código foi encontrado. Tente uma imagem mais nítida, com o código inteiro visível.');
      }
    });
  }
  function lerFrame() {
    if (usarNativo) {
      return detectarNativo(video).catch(function () { usarNativo = false; return null; });
    }
    canvas.width = video.videoWidth;
    canvas.height = video.videoHeight;
    canvas.getContext('2d').drawImage(video, 0, 0, canvas.width, canvas.height);
    return detectarZXing(canvas.toDataURL('image/jpeg', 0.85)).catch(function (e) {
      if (e === 'carga') { throw e; }
      return null;
    });
  }
  function varrer() {
    if (!rodando) { return; }
    if (video.readyState >= 2) {
      lerFrame().then(function (r) {
        if (!rodando) { return; }
        if (r) {
          fechar(true);
          sucesso(r.formato, r.texto);
        } else {
          setTimeout(varrer, 300);
        }
      }).catch(function (e) {
        if (!rodando) { return; }
        if (e === 'carga') {
          fechar(true);
          erro('não foi possível carregar o leitor. Verifique sua conexão e tente novamente.');
        } else {
          setTimeout(varrer, 300);
        }
      });
    } else {
      setTimeout(varrer, 200);
    }
  }
  function abrirCamera() {
    if (!navigator.mediaDevices || !navigator.mediaDevices.getUserMedia) {
      erro('este navegador não permite o uso da câmera. Use a opção "Enviar Imagem".');
      return;
    }
    preview.style.display = 'none';
    info('abrindo a câmera...');
    navigator.mediaDevices.getUserMedia({ video: { facingMode: 'environment' }, audio: false }).then(function (s) {
      stream = s;
      video.srcObject = s;
      areaVideo.style.display = 'block';
      btnCamera.style.display = 'none';
      btnFechar.style.display = 'block';
      return video.play();
    }).then(function () {
      rodando = true;
      info('aponte a câmera para o código e mantenha-o parado e bem iluminado.');
      varrer();
    }).catch(function () {
      fechar(true);
      erro('não foi possível acessar a câmera. Verifique a permissão do navegador.');
    });
  }
  function fechar(silencioso) {
    rodando = false;
    if (stream) {
      stream.getTracks().forEach(function (t) { t.stop(); });
      stream = null;
    }
    video.srcObject = null;
    areaVideo.style.display = 'none';
    btnFechar.style.display = 'none';
    btnCamera.style.display = 'block';
    if (!silencioso) { info('câmera fechada.'); }
  }
  btnCamera.addEventListener('click', abrirCamera);
  btnFechar.addEventListener('click', function () { fechar(false); });
  arquivo.addEventListener('change', function () {
    var f = arquivo.files[0];
    if (f) { lerImagem(f); }
    arquivo.value = '';
  });
  window.addEventListener('pagehide', function () { fechar(true); });
})();
</script>

## Como usar o leitor

1. Para ler com a câmera, clique em **Usar Câmera** e permita o acesso quando o navegador pedir.
2. Aponte a câmera para o código e mantenha-o inteiro na tela, parado e bem iluminado. A leitura é automática e a câmera fecha sozinha quando o código é reconhecido.
3. Para ler uma imagem salva (foto ou captura de tela), clique em **Enviar Imagem** e escolha o arquivo.
4. Veja o formato e o conteúdo do código no campo **Resposta**.
5. Clique em **Fechar** a qualquer momento para desligar a câmera.

A leitura acontece no próprio navegador, sem enviar a imagem para nenhum servidor. Para usar a câmera, a página precisa estar aberta em conexão segura (HTTPS).

## Entendendo os termos

- **Código de barras:** representação visual de dados em barras ou padrões que uma máquina consegue ler, usada em produtos, boletos e etiquetas.
- **Código 1D:** código linear, formado por barras verticais de larguras diferentes, como o EAN-13 e o Code 128.
- **Código 2D:** código que guarda dados em duas dimensões, como quadrados ou pontos, e comporta mais informação, como o QR Code.
- **QR Code:** código 2D quadrado que pode guardar links, textos e outros dados e é lido por câmeras de celular.
- **EAN-13:** formato de 13 dígitos usado na maioria dos produtos vendidos no comércio.
- **Code 128:** formato linear compacto que codifica letras, números e símbolos, comum em logística e etiquetas de envio.
- **Code 39:** formato linear que codifica letras maiúsculas, números e alguns símbolos, usado em crachás e controle de estoque.
- **PDF-417:** código 2D em formato de pilha de barras, usado em documentos, ingressos e cartões de embarque.
- **Data Matrix:** código 2D quadrado e pequeno, usado para marcar peças, eletrônicos e medicamentos.
- **Decodificar:** converter o desenho do código no texto ou número que ele guarda.
- **Permissão da câmera:** autorização que o navegador pede para usar a câmera do aparelho; sem ela, só é possível ler por imagem.