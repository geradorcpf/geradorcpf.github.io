---
title: "Color Picker"
seoTitle: "Color Picker: online e grátis"
description: "Color Picker: escolha uma cor e copie os códigos HEX, RGB e HSL. Grátis e online, sem cadastro."
summary: "Escolha uma cor e copie os códigos HEX, RGB e HSL."
date: 2026-10-24
draft: false
category: "dev"
tags: ["cores", "css", "design", "desenvolvimento"]
keywords: ["color picker", "color picker online", "cores", "css", "design"]
---
<!--sudah dikerjakan-->

Não sabe qual é o código da cor que você precisa? Clique na caixa de cor abaixo, escolha a cor desejada e os códigos **HEX**, **RGB**, **HSL** e **decimal** são atualizados na hora. Depois é só copiar.

<div id="color-picker-tool" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🎨 Color Picker</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Escolha uma cor e copie os códigos na hora.</p>
<label for="cp-seletor" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Escolha a cor</label>
<div style="display:flex;gap:10px;align-items:stretch;margin-bottom:6px;">
<input id="cp-seletor" type="color" value="#4f46e5" style="width:64px;min-width:64px;height:48px;padding:3px;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;cursor:pointer;box-sizing:border-box;">
<input id="cp-hex-entrada" type="text" placeholder="Ex.: #4F46E5" autocomplete="off" spellcheck="false" maxlength="7" aria-label="Código HEX da cor" style="flex:1;min-width:0;padding:12px 14px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
</div>
<div id="cp-erro" aria-live="polite" style="min-height:20px;margin-bottom:10px;font-size:0.85rem;color:#b91c1c;"></div>
<div id="cp-previa" style="height:90px;margin-bottom:20px;background:#4f46e5;border:2px solid #c7d2fe;border-radius:12px;box-sizing:border-box;"></div>
<div id="cp-resposta" aria-live="polite" style="padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;">
<strong style="color:#3730a3;">Resposta:</strong>
<div style="display:flex;align-items:center;gap:10px;margin-top:10px;flex-wrap:wrap;">
<span style="width:72px;font-weight:600;color:#3730a3;">HEX</span>
<span id="cp-saida-hex" style="flex:1;min-width:120px;font-family:ui-monospace,SFMono-Regular,Menlo,Consolas,monospace;color:#166534;font-weight:700;"></span>
<button type="button" class="cp-copiar" data-alvo="cp-saida-hex" style="padding:6px 12px;font-size:0.85rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:8px;cursor:pointer;">Copiar</button>
</div>
<div style="display:flex;align-items:center;gap:10px;margin-top:10px;flex-wrap:wrap;">
<span style="width:72px;font-weight:600;color:#3730a3;">RGB</span>
<span id="cp-saida-rgb" style="flex:1;min-width:120px;font-family:ui-monospace,SFMono-Regular,Menlo,Consolas,monospace;color:#166534;font-weight:700;"></span>
<button type="button" class="cp-copiar" data-alvo="cp-saida-rgb" style="padding:6px 12px;font-size:0.85rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:8px;cursor:pointer;">Copiar</button>
</div>
<div style="display:flex;align-items:center;gap:10px;margin-top:10px;flex-wrap:wrap;">
<span style="width:72px;font-weight:600;color:#3730a3;">HSL</span>
<span id="cp-saida-hsl" style="flex:1;min-width:120px;font-family:ui-monospace,SFMono-Regular,Menlo,Consolas,monospace;color:#166534;font-weight:700;"></span>
<button type="button" class="cp-copiar" data-alvo="cp-saida-hsl" style="padding:6px 12px;font-size:0.85rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:8px;cursor:pointer;">Copiar</button>
</div>
<div style="display:flex;align-items:center;gap:10px;margin-top:10px;flex-wrap:wrap;">
<span style="width:72px;font-weight:600;color:#3730a3;">Decimal</span>
<span id="cp-saida-dec" style="flex:1;min-width:120px;font-family:ui-monospace,SFMono-Regular,Menlo,Consolas,monospace;color:#166534;font-weight:700;"></span>
<button type="button" class="cp-copiar" data-alvo="cp-saida-dec" style="padding:6px 12px;font-size:0.85rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:8px;cursor:pointer;">Copiar</button>
</div>
</div>
<div style="display:flex;gap:10px;flex-wrap:wrap;margin-top:20px;">
<button type="button" id="cp-link" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Copiar link da cor</button>
<button type="button" id="cp-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
</div>
<script>
(function () {
  var seletor = document.getElementById('cp-seletor');
  var campoHex = document.getElementById('cp-hex-entrada');
  var previa = document.getElementById('cp-previa');
  var msgErro = document.getElementById('cp-erro');
  var saidaHex = document.getElementById('cp-saida-hex');
  var saidaRgb = document.getElementById('cp-saida-rgb');
  var saidaHsl = document.getElementById('cp-saida-hsl');
  var saidaDec = document.getElementById('cp-saida-dec');
  var corPadrao = '#4f46e5';
  var corAtual = corPadrao;
  function normalizar(valor) {
    var t = String(valor).trim().replace('#', '').toLowerCase();
    if (/^[0-9a-f]{3}$/.test(t)) {
      t = t.charAt(0) + t.charAt(0) + t.charAt(1) + t.charAt(1) + t.charAt(2) + t.charAt(2);
    }
    if (!/^[0-9a-f]{6}$/.test(t)) { return null; }
    return '#' + t;
  }
  function paraRgb(hex) {
    return {
      r: parseInt(hex.substr(1, 2), 16),
      g: parseInt(hex.substr(3, 2), 16),
      b: parseInt(hex.substr(5, 2), 16)
    };
  }
  function paraHsl(c) {
    var r = c.r / 255;
    var g = c.g / 255;
    var b = c.b / 255;
    var max = Math.max(r, g, b);
    var min = Math.min(r, g, b);
    var l = (max + min) / 2;
    var d = max - min;
    var h = 0;
    var s = 0;
    if (d !== 0) {
      s = l > 0.5 ? d / (2 - max - min) : d / (max + min);
      if (max === r) { h = (g - b) / d + (g > b ? 0 : 6); }
      else if (max === g) { h = (b - r) / d + 2; }
      else { h = (r - g) / d + 4; }
      h = h * 60;
    }
    return { h: Math.round(h) % 360, s: Math.round(s * 100), l: Math.round(l * 100) };
  }
  function atualizar(hex, origem) {
    var rgb = paraRgb(hex);
    var hsl = paraHsl(rgb);
    corAtual = hex;
    seletor.value = hex;
    if (origem !== 'texto') { campoHex.value = hex.toUpperCase(); }
    previa.style.background = hex;
    saidaHex.textContent = hex.toUpperCase();
    saidaRgb.textContent = 'rgb(' + rgb.r + ', ' + rgb.g + ', ' + rgb.b + ')';
    saidaHsl.textContent = 'hsl(' + hsl.h + ', ' + hsl.s + '%, ' + hsl.l + '%)';
    saidaDec.textContent = String(rgb.r * 65536 + rgb.g * 256 + rgb.b);
    msgErro.textContent = '';
    campoHex.style.borderColor = '#c7d2fe';
  }
  function copiar(texto, botao, rotulo) {
    function feito() {
      botao.textContent = 'Copiado!';
      setTimeout(function () { botao.textContent = rotulo; }, 1500);
    }
    function alternativa() {
      var area = document.createElement('textarea');
      area.value = texto;
      area.style.position = 'fixed';
      area.style.opacity = '0';
      document.body.appendChild(area);
      area.select();
      try { document.execCommand('copy'); feito(); } catch (e) { botao.textContent = 'Erro ao copiar'; }
      document.body.removeChild(area);
    }
    if (navigator.clipboard && navigator.clipboard.writeText) {
      navigator.clipboard.writeText(texto).then(feito, alternativa);
    } else {
      alternativa();
    }
  }
  seletor.addEventListener('input', function () { atualizar(seletor.value.toLowerCase(), 'seletor'); });
  campoHex.addEventListener('input', function () {
    var hex = normalizar(campoHex.value);
    if (hex) {
      atualizar(hex, 'texto');
    } else if (campoHex.value.trim() !== '') {
      msgErro.textContent = 'informe um código HEX válido, como #4F46E5 ou #FFF.';
      campoHex.style.borderColor = '#fca5a5';
    } else {
      msgErro.textContent = '';
      campoHex.style.borderColor = '#c7d2fe';
    }
  });
  campoHex.addEventListener('blur', function () {
    var hex = normalizar(campoHex.value);
    campoHex.value = (hex || corAtual).toUpperCase();
    msgErro.textContent = '';
    campoHex.style.borderColor = '#c7d2fe';
  });
  campoHex.addEventListener('focus', function () { campoHex.style.borderColor = '#6366f1'; });
  Array.prototype.forEach.call(document.querySelectorAll('#color-picker-tool .cp-copiar'), function (botao) {
    botao.addEventListener('click', function () {
      var alvo = document.getElementById(botao.getAttribute('data-alvo'));
      copiar(alvo.textContent, botao, 'Copiar');
    });
  });
  document.getElementById('cp-link').addEventListener('click', function () {
    var base = window.location.href.split('#')[0].split('?')[0];
    copiar(base + '?cor=' + corAtual.replace('#', ''), this, 'Copiar link da cor');
  });
  document.getElementById('cp-limpar').addEventListener('click', function () {
    atualizar(corPadrao, 'limpar');
    campoHex.focus();
  });
  var inicial = corPadrao;
  try {
    var param = new URLSearchParams(window.location.search).get('cor');
    if (param && normalizar(param)) { inicial = normalizar(param); }
  } catch (e) { inicial = corPadrao; }
  atualizar(inicial, 'inicio');
})();
</script>

## Como usar a ferramenta

1. Clique na **caixa de cor** (à esquerda) para abrir o seletor e escolha a cor desejada. Os códigos são atualizados na hora, ao lado da pré-visualização.
2. Se você já sabe o código, digite o **HEX** no campo de texto, com ou sem `#`. Também funciona com 3 dígitos (por exemplo, `#FFF`).
3. Confira a cor na **pré-visualização** e nos códigos **HEX**, **RGB**, **HSL** e **Decimal**.
4. Clique em **Copiar** ao lado do código que você quer usar no seu CSS, design ou projeto.
5. Clique em **Copiar link da cor** para compartilhar. Quando o link for aberto, a página já mostra a cor escolhida.
6. Use o botão **Limpar** para voltar à cor inicial e começar de novo.

## Entendendo os termos

- **Color Picker:** ferramenta que permite escolher uma cor visualmente e obter o seu código, parecida com o conta-gotas de editores de imagem.
- **Código de cor:** conjunto de letras e números que identifica uma cor de forma exata, para que ela seja reproduzida igual em qualquer tela ou programa.
- **HEX (hexadecimal):** código de 6 dígitos precedido por `#`, como `#4F46E5`. Cada par de dígitos representa a quantidade de vermelho, verde e azul. É o formato mais usado em CSS.
- **RGB:** sigla de Red, Green e Blue (vermelho, verde e azul). A cor é formada pela mistura dos três canais, cada um de 0 a 255, como `rgb(79, 70, 229)`.
- **HSL:** sigla de Hue, Saturation e Lightness (matiz, saturação e luminosidade). Descreve a cor de um jeito mais intuitivo, como `hsl(243, 75%, 59%)`.
- **Matiz (Hue):** a "cor pura" na roda de cores, medida em graus de 0° a 360° (0° é vermelho, 120° é verde e 240° é azul).
- **Saturação (Saturation):** intensidade da cor, de 0% (cinza) a 100% (cor totalmente viva).
- **Luminosidade (Lightness):** quão clara ou escura é a cor, de 0% (preto) a 100% (branco).
- **Decimal:** o mesmo código HEX escrito como um único número inteiro. Por exemplo, `#FFFFFF` equivale a `16777215`.
- **Canal de cor:** cada uma das três partes (vermelho, verde e azul) que compõem uma cor no sistema RGB e no HEX.
- **Pré-visualização:** área colorida que mostra como a cor escolhida aparece na tela.
- **Link da cor:** endereço da página com a cor escolhida guardada, usado para enviar a mesma cor para outra pessoa.