---
title: "Tela Branca"
seoTitle: "Tela Branca"
description: "Tela Branca: tela branca em tela cheia para testar monitores e iluminar. Grátis e online, sem cadastro."
summary: "Tela branca em tela cheia para testar monitores e iluminar."
date: 2026-11-11
draft: false
category: "util"
tags: ["tela", "diagnóstico", "produtividade"]
keywords: ["tela branca", "tela branca online", "tela", "diagnóstico", "produtividade"]
---

Basta clicar em **Abrir Tela Branca** abaixo para ocupar toda a tela com a cor branca. Para fechar, clique na tela ou pressione **ESC**.

<div id="tela-branca-tool" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🖥️ Tela Branca</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Abra em tela cheia, personalize a cor ou baixe a imagem em PNG.</p>
<div id="tb-preview" title="Clique para abrir em tela cheia" style="width:100%;height:96px;margin-bottom:6px;background:#ffffff;border:2px solid #c7d2fe;border-radius:12px;cursor:pointer;box-sizing:border-box;"></div>
<p style="margin:0 0 18px;font-size:0.85rem;color:#64748b;text-align:center;">Clique na prévia para abrir em tela cheia</p>
<div style="display:flex;gap:10px;flex-wrap:wrap;margin-bottom:22px;">
<button type="button" id="tb-abrir" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Abrir Tela Branca</button>
<button type="button" id="tb-redefinir" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Redefinir Padrão</button>
</div>
<h3 style="margin:0 0 12px;font-size:1.05rem;color:#3730a3;">Personalizar Cor</h3>
<label for="tb-lum" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Luminosidade: <span id="tb-lum-txt">100%</span></label>
<input id="tb-lum" type="range" min="0" max="100" value="100" style="width:100%;margin:0 0 16px;accent-color:#4f46e5;cursor:pointer;box-sizing:border-box;">
<label for="tb-seletor" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Seletor de Cor</label>
<input id="tb-seletor" type="color" value="#ffffff" style="width:100%;height:44px;padding:4px;margin-bottom:16px;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;cursor:pointer;box-sizing:border-box;">
<label for="tb-hex" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Hex Code</label>
<input id="tb-hex" type="text" maxlength="7" placeholder="Ex.: FFFFFF" autocomplete="off" value="FFFFFF" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<div style="display:flex;gap:10px;margin-bottom:22px;">
<div style="flex:1;min-width:0;">
<label for="tb-r" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">R</label>
<input id="tb-r" type="text" inputmode="numeric" maxlength="3" value="255" autocomplete="off" style="width:100%;padding:12px 14px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
</div>
<div style="flex:1;min-width:0;">
<label for="tb-g" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">G</label>
<input id="tb-g" type="text" inputmode="numeric" maxlength="3" value="255" autocomplete="off" style="width:100%;padding:12px 14px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
</div>
<div style="flex:1;min-width:0;">
<label for="tb-b" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">B</label>
<input id="tb-b" type="text" inputmode="numeric" maxlength="3" value="255" autocomplete="off" style="width:100%;padding:12px 14px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
</div>
</div>
<h3 style="margin:0 0 12px;font-size:1.05rem;color:#3730a3;">Baixar Imagem PNG</h3>
<label for="tb-res" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Resolução</label>
<select id="tb-res" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<option value="854x480">480p</option>
<option value="1280x720">720p</option>
<option value="1920x1080" selected>1080p</option>
<option value="2560x1440">1440p (2K)</option>
<option value="3840x2160">2160p (4K)</option>
<option value="7680x4320">4320p (8K)</option>
<option value="custom">Personalizado</option>
</select>
<div style="display:flex;gap:10px;align-items:flex-end;margin-bottom:20px;">
<div style="flex:1;min-width:0;">
<label for="tb-w" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Largura (px)</label>
<input id="tb-w" type="text" inputmode="numeric" maxlength="4" value="1920" autocomplete="off" style="width:100%;padding:12px 14px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
</div>
<div style="padding-bottom:12px;font-weight:700;color:#64748b;">×</div>
<div style="flex:1;min-width:0;">
<label for="tb-h" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Altura (px)</label>
<input id="tb-h" type="text" inputmode="numeric" maxlength="4" value="1080" autocomplete="off" style="width:100%;padding:12px 14px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
</div>
</div>
<button type="button" id="tb-baixar" style="width:100%;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Baixar PNG</button>
<div id="tb-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Status:</strong> <span id="tb-status">ajuste a cor se quiser e clique em "Abrir Tela Branca".</span></div>
</div>
<script>
(function () {
  var r = 255, g = 255, b = 255, lum = 100, aberto = false;
  function el(id) { return document.getElementById(id); }
  var preview = el('tb-preview');
  var slider = el('tb-lum');
  var lumTxt = el('tb-lum-txt');
  var seletor = el('tb-seletor');
  var hexInp = el('tb-hex');
  var rInp = el('tb-r');
  var gInp = el('tb-g');
  var bInp = el('tb-b');
  var resSel = el('tb-res');
  var wInp = el('tb-w');
  var hInp = el('tb-h');
  var caixa = el('tb-resposta');
  var status = el('tb-status');
  var overlay = document.createElement('div');
  overlay.style.cssText = 'position:fixed;top:0;left:0;width:100%;height:100%;z-index:2147483647;display:none;cursor:pointer;';
  document.body.appendChild(overlay);
  function clamp(n, min, max) { return Math.min(max, Math.max(min, n)); }
  function hex2(n) { var h = n.toString(16); return h.length === 1 ? '0' + h : h; }
  function toHex(a, c, d) { return hex2(a) + hex2(c) + hex2(d); }
  function efetiva() {
    var f = lum / 100;
    return [Math.round(r * f), Math.round(g * f), Math.round(b * f)];
  }
  function corCss() {
    var c = efetiva();
    return 'rgb(' + c[0] + ',' + c[1] + ',' + c[2] + ')';
  }
  function ok(msg) {
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    status.style.color = '#166534';
    status.textContent = msg;
  }
  function erro(msg) {
    caixa.style.borderColor = '#fca5a5';
    caixa.style.background = '#fef2f2';
    status.style.color = '#b91c1c';
    status.textContent = msg;
  }
  function neutro(msg) {
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    status.style.color = '#64748b';
    status.textContent = msg;
  }
  function atualizar(origem) {
    if (origem !== 'hex') { hexInp.value = toHex(r, g, b).toUpperCase(); }
    if (origem !== 'rgb') { rInp.value = r; gInp.value = g; bInp.value = b; }
    seletor.value = '#' + toHex(r, g, b);
    slider.value = lum;
    lumTxt.textContent = lum + '%';
    preview.style.background = corCss();
    if (aberto) { overlay.style.background = corCss(); }
  }
  function aplicarHex(texto, origem) {
    var v = String(texto).trim().replace('#', '');
    if (v.length === 3) { v = v.charAt(0) + v.charAt(0) + v.charAt(1) + v.charAt(1) + v.charAt(2) + v.charAt(2); }
    if (/^[0-9a-fA-F]{6}$/.test(v)) {
      r = parseInt(v.substr(0, 2), 16);
      g = parseInt(v.substr(2, 2), 16);
      b = parseInt(v.substr(4, 2), 16);
      atualizar(origem);
      return true;
    }
    return false;
  }
  function abrir() {
    aberto = true;
    overlay.style.background = corCss();
    overlay.style.display = 'block';
    try {
      if (overlay.requestFullscreen) {
        var p = overlay.requestFullscreen();
        if (p) { p.catch(function () {}); }
      }
    } catch (e) {}
  }
  function fechar() {
    if (!aberto) { return; }
    aberto = false;
    overlay.style.display = 'none';
    try {
      if (document.fullscreenElement) {
        var p = document.exitFullscreen();
        if (p) { p.catch(function () {}); }
      }
    } catch (e) {}
  }
  function redefinir() {
    r = 255; g = 255; b = 255; lum = 100;
    resSel.value = '1920x1080';
    wInp.value = '1920';
    hInp.value = '1080';
    atualizar('');
    neutro('cor redefinida para branco (#FFFFFF) com 100% de luminosidade.');
  }
  function baixar() {
    var w = parseInt(wInp.value, 10);
    var h = parseInt(hInp.value, 10);
    if (isNaN(w) || isNaN(h)) { erro('informe largura e altura válidas em pixels.'); return; }
    if (w > 7680 || h > 7680) { erro('o tamanho máximo é de 7680 px por lado.'); return; }
    if (w === 0 || h === 0) { erro('largura e altura devem ser maiores que zero.'); return; }
    var canvas = document.createElement('canvas');
    canvas.width = w;
    canvas.height = h;
    var ctx = canvas.getContext('2d');
    if (!ctx) { erro('seu navegador não conseguiu gerar a imagem.'); return; }
    ctx.fillStyle = corCss();
    ctx.fillRect(0, 0, w, h);
    var c = efetiva();
    var branco = (c[0] === 255) && (c[1] === 255) && (c[2] === 255);
    var nome = (branco ? 'tela-branca' : 'tela-' + toHex(c[0], c[1], c[2])) + '-' + w + 'x' + h + '.png';
    canvas.toBlob(function (blob) {
      if (!blob) { erro('não foi possível gerar o PNG. Tente uma resolução menor.'); return; }
      var url = URL.createObjectURL(blob);
      var a = document.createElement('a');
      a.href = url;
      a.download = nome;
      document.body.appendChild(a);
      a.click();
      document.body.removeChild(a);
      setTimeout(function () { URL.revokeObjectURL(url); }, 1000);
      ok('imagem ' + nome + ' gerada com sucesso.');
    }, 'image/png');
  }
  el('tb-abrir').addEventListener('click', abrir);
  preview.addEventListener('click', abrir);
  overlay.addEventListener('click', fechar);
  el('tb-redefinir').addEventListener('click', redefinir);
  el('tb-baixar').addEventListener('click', baixar);
  document.addEventListener('keydown', function (e) {
    if (e.key === 'Escape') { fechar(); }
  });
  document.addEventListener('fullscreenchange', function () {
    if (!document.fullscreenElement) { fechar(); }
  });
  slider.addEventListener('input', function () {
    lum = clamp(parseInt(slider.value, 10) || 0, 0, 100);
    atualizar('lum');
  });
  seletor.addEventListener('input', function () { aplicarHex(seletor.value, ''); });
  hexInp.addEventListener('input', function () { aplicarHex(hexInp.value, 'hex'); });
  hexInp.addEventListener('blur', function () { atualizar(''); });
  function lerRgb(origem) {
    var nr = parseInt(rInp.value, 10);
    var ng = parseInt(gInp.value, 10);
    var nb = parseInt(bInp.value, 10);
    if (isNaN(nr) || isNaN(ng) || isNaN(nb)) { return; }
    r = clamp(nr, 0, 255);
    g = clamp(ng, 0, 255);
    b = clamp(nb, 0, 255);
    atualizar(origem);
  }
  [rInp, gInp, bInp].forEach(function (inp) {
    inp.addEventListener('input', function () { lerRgb('rgb'); });
    inp.addEventListener('blur', function () { atualizar(''); });
  });
  resSel.addEventListener('change', function () {
    if (resSel.value === 'custom') { return; }
    var partes = resSel.value.split('x');
    wInp.value = partes[0];
    hInp.value = partes[1];
  });
  [wInp, hInp].forEach(function (inp) {
    inp.addEventListener('input', function () { resSel.value = 'custom'; });
  });
  [hexInp, rInp, gInp, bInp, wInp, hInp, resSel].forEach(function (inp) {
    inp.addEventListener('focus', function () { inp.style.borderColor = '#6366f1'; });
    inp.addEventListener('blur', function () { inp.style.borderColor = '#c7d2fe'; });
  });
  atualizar('');
})();
</script>

## Como usar a ferramenta

1. Clique em **Abrir Tela Branca** (ou na prévia) para exibir a tela branca em tela cheia.
2. Para fechar, clique em qualquer ponto da tela ou pressione **ESC**.
3. Se quiser outra cor, use o **Seletor de Cor**, digite o **Hex Code** ou informe os valores de **R**, **G** e **B**. A prévia muda na hora.
4. Ajuste a **Luminosidade** com o controle deslizante para escurecer a cor e reduzir o brilho da tela.
5. Para salvar a imagem, escolha uma **Resolução** (ou digite largura e altura) e clique em **Baixar PNG**.
6. Use **Redefinir Padrão** para voltar ao branco puro com 100% de luminosidade.

Tudo funciona direto no navegador, sem cadastro e sem enviar nada para servidores. O tamanho máximo da imagem é de 7680 px por lado.

## Entendendo os termos

- **Tela branca:** tela totalmente preenchida com a cor branca (#FFFFFF), usada para testar o display e como fonte de luz.
- **Tela cheia:** modo em que a página ocupa todo o monitor, escondendo barras, abas e menus do navegador.
- **ESC:** tecla Esc do teclado, usada para sair do modo de tela cheia.
- **Luminosidade:** intensidade da cor exibida. Em 100% a cor aparece como escolhida; valores menores escurecem a cor em direção ao preto.
- **Seletor de cor:** paleta visual em que você clica para escolher uma cor sem precisar digitar códigos.
- **Hex Code:** código hexadecimal de seis dígitos que representa uma cor, como #FFFFFF (branco) ou #000000 (preto).
- **RGB:** sistema que mistura Vermelho (R), Verde (G) e Azul (B), cada um com valor de 0 a 255.
- **Pixel:** menor ponto de uma tela ou imagem. A tela é formada por milhões deles.
- **Pixel morto:** pixel que não acende ou fica travado em uma cor. Fica mais fácil de ver em uma tela branca.
- **Resolução:** quantidade de pixels da imagem, em largura × altura, como 1920 × 1080 (1080p).
- **PNG:** formato de imagem sem perda de qualidade, bom para salvar cores sólidas com precisão.
- **Redefinir Padrão:** botão que devolve a cor ao branco e a luminosidade a 100%.