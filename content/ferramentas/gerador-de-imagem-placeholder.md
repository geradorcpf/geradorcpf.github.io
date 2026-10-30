---
title: "Gerador de Imagem Placeholder"
seoTitle: "Gerador de Imagem Placeholder"
description: "Gerador de Imagem Placeholder: gere imagens de espaço reservado no tamanho e cor desejados. Grátis e online, sem cadastro."
summary: "Gere imagens de espaço reservado no tamanho e cor desejados."
date: 2026-10-30
draft: false
category: "dev"
tags: ["placeholder", "imagens", "design", "dados de teste"]
keywords: ["gerador de imagem placeholder", "gerador de imagem placeholder online", "placeholder", "imagens", "design"]
---

Basta escolher o tamanho, as cores e o formato abaixo e depois clicar em **Gerar Imagem**.

<div id="gerador-placeholder" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🖼️ Gerador de Imagem Placeholder</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Defina as opções e gere uma imagem de teste na hora.</p>
<label for="ph-formato" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Extensão do Arquivo</label>
<select id="ph-formato" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;cursor:pointer;">
<option value="png" selected>.png</option>
<option value="jpg">.jpg</option>
<option value="gif">.gif</option>
</select>
<div style="display:flex;gap:12px;flex-wrap:wrap;">
<div style="flex:1;min-width:140px;">
<label for="ph-cor-fundo" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Cor do Fundo</label>
<input id="ph-cor-fundo" type="color" value="#cccccc" style="width:100%;height:46px;padding:4px;margin-bottom:16px;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;box-sizing:border-box;outline:none;cursor:pointer;">
</div>
<div style="flex:1;min-width:140px;">
<label for="ph-cor-texto" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Cor do Texto</label>
<input id="ph-cor-texto" type="color" value="#969696" style="width:100%;height:46px;padding:4px;margin-bottom:16px;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;box-sizing:border-box;outline:none;cursor:pointer;">
</div>
</div>
<label for="ph-texto" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Texto</label>
<input id="ph-texto" type="text" placeholder="Vazio = mostra largura x altura" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<label for="ph-tamanho-texto" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Tamanho do Texto</label>
<select id="ph-tamanho-texto" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;cursor:pointer;"></select>
<label for="ph-tamanhos" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Larguras Comuns</label>
<select id="ph-tamanhos" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;cursor:pointer;">
<option value="320x240">320x240</option>
<option value="640x480" selected>640x480</option>
<option value="800x600">800x600</option>
<option value="1024x768">1024x768</option>
<option value="1600x1200">1600x1200</option>
<option value="custom">Personalizado</option>
</select>
<div style="display:flex;gap:12px;flex-wrap:wrap;">
<div style="flex:1;min-width:140px;">
<label for="ph-largura" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Largura (px)</label>
<input id="ph-largura" type="text" inputmode="numeric" value="640" placeholder="Ex.: 640" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:20px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
</div>
<div style="flex:1;min-width:140px;">
<label for="ph-altura" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Altura (px)</label>
<input id="ph-altura" type="text" inputmode="numeric" value="480" placeholder="Ex.: 480" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:20px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
</div>
</div>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="ph-gerar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Gerar Imagem</button>
<button type="button" id="ph-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="ph-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="ph-resultado">defina as opções e clique em "Gerar Imagem".</span>
<canvas id="ph-canvas" width="1" height="1" style="display:none;max-width:100%;height:auto;margin-top:14px;border:1px solid #c7d2fe;border-radius:8px;"></canvas>
<button type="button" id="ph-baixar" style="display:none;width:100%;margin-top:14px;padding:13px 18px;font-size:1rem;font-weight:700;color:#4f46e5;background:#ffffff;border:2px solid #6366f1;border-radius:10px;cursor:pointer;">Baixar Imagem</button>
</div>
</div>
<script>
(function () {
  var MAX = 2000;
  var formato = document.getElementById('ph-formato');
  var corFundo = document.getElementById('ph-cor-fundo');
  var corTexto = document.getElementById('ph-cor-texto');
  var texto = document.getElementById('ph-texto');
  var tamTexto = document.getElementById('ph-tamanho-texto');
  var tamanhos = document.getElementById('ph-tamanhos');
  var largura = document.getElementById('ph-largura');
  var altura = document.getElementById('ph-altura');
  var caixa = document.getElementById('ph-resposta');
  var resultado = document.getElementById('ph-resultado');
  var tela = document.getElementById('ph-canvas');
  var btnBaixar = document.getElementById('ph-baixar');
  var atual = null;
  var pow2 = [];
  var n;
  for (n = 0; 25 > n; n += 1) { pow2.push(Math.pow(2, n)); }
  var optAuto = document.createElement('option');
  optAuto.value = 'auto';
  optAuto.textContent = 'Automático';
  tamTexto.appendChild(optAuto);
  for (n = 2; 52 > n; n += 2) {
    var opt = document.createElement('option');
    opt.value = String(n);
    opt.textContent = n + ' px';
    tamTexto.appendChild(opt);
  }
  function inteiro(v) {
    var t = String(v).trim();
    if (!/^[0-9]+$/.test(t)) { return NaN; }
    return Number(t);
  }
  function rgb(hex) {
    return [parseInt(hex.substr(1, 2), 16), parseInt(hex.substr(3, 2), 16), parseInt(hex.substr(5, 2), 16)];
  }
  function esconderSaida() {
    atual = null;
    tela.style.display = 'none';
    btnBaixar.style.display = 'none';
  }
  function erro(msg) {
    esconderSaida();
    caixa.style.borderColor = '#fca5a5';
    caixa.style.background = '#fef2f2';
    resultado.style.color = '#b91c1c';
    resultado.textContent = msg;
  }
  function sucesso(blob, nome, w, h, ext) {
    atual = { blob: blob, nome: nome };
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    resultado.textContent = 'imagem ' + ext.toUpperCase() + ' de ' + w + ' × ' + h + ' px gerada (' + (blob.size / 1024).toFixed(1) + ' KB). Clique em "Baixar Imagem" para salvar.';
    tela.style.display = 'block';
    btnBaixar.style.display = 'block';
  }
  function lzw(idx) {
    var out = [];
    var cur = 0;
    var bits = 0;
    var size = 9;
    var next = 258;
    var dict = {};
    function emitir(code) {
      cur += code * pow2[bits];
      bits += size;
      while (bits >= 8) {
        out.push(cur % 256);
        cur = Math.floor(cur / 256);
        bits -= 8;
      }
      if (next >= pow2[size]) {
        if (12 > size) { size += 1; }
      }
    }
    emitir(256);
    var prefixo = idx[0];
    var i, k, chave;
    for (i = 1; idx.length > i; i += 1) {
      k = idx[i];
      chave = prefixo * 256 + k;
      if (dict[chave] !== undefined) {
        prefixo = dict[chave];
      } else {
        emitir(prefixo);
        if (4096 > next) {
          dict[chave] = next;
          next += 1;
        } else {
          emitir(256);
          dict = {};
          next = 258;
          size = 9;
        }
        prefixo = k;
      }
    }
    emitir(prefixo);
    emitir(257);
    if (bits > 0) { out.push(cur % 256); }
    return out;
  }
  function criarGif(w, h, dados, fundo, frente) {
    var pal = [];
    var i, j;
    for (i = 0; 256 > i; i += 1) {
      for (j = 0; 3 > j; j += 1) {
        pal.push(Math.round(fundo[j] + (frente[j] - fundo[j]) * i / 255));
      }
    }
    var canal = 0;
    var maior = 0;
    var d;
    for (j = 0; 3 > j; j += 1) {
      d = Math.abs(frente[j] - fundo[j]);
      if (d > maior) { maior = d; canal = j; }
    }
    var total = w * h;
    var idx = new Uint8Array(total);
    var p, t;
    if (maior > 0) {
      for (p = 0; total > p; p += 1) {
        t = (dados[p * 4 + canal] - fundo[canal]) / (frente[canal] - fundo[canal]);
        if (0 > t) { t = 0; }
        if (t > 1) { t = 1; }
        idx[p] = Math.round(t * 255);
      }
    }
    var lw = w % 256, hw = Math.floor(w / 256), lh = h % 256, hh = Math.floor(h / 256);
    var out = [71, 73, 70, 56, 57, 97, lw, hw, lh, hh, 247, 0, 0];
    for (i = 0; pal.length > i; i += 1) { out.push(pal[i]); }
    out.push(44, 0, 0, 0, 0, lw, hw, lh, hh, 0, 8);
    var comp = lzw(idx);
    var m, tam;
    for (i = 0; comp.length > i; i += 255) {
      tam = Math.min(255, comp.length - i);
      out.push(tam);
      for (m = 0; tam > m; m += 1) { out.push(comp[i + m]); }
    }
    out.push(0, 59);
    return new Uint8Array(out);
  }
  function gerar() {
    var w = inteiro(largura.value);
    var h = inteiro(altura.value);
    if (isNaN(w)) { erro('informe uma largura válida (número inteiro).'); return; }
    if (isNaN(h)) { erro('informe uma altura válida (número inteiro).'); return; }
    if (1 > w) { erro('a largura deve ser maior que zero.'); return; }
    if (1 > h) { erro('a altura deve ser maior que zero.'); return; }
    if (w > MAX) { erro('a largura máxima é ' + MAX + ' px.'); return; }
    if (h > MAX) { erro('a altura máxima é ' + MAX + ' px.'); return; }
    var ext = formato.value;
    var cF = corFundo.value;
    var cT = corTexto.value;
    tela.width = w;
    tela.height = h;
    var ctx = tela.getContext('2d');
    ctx.fillStyle = cF;
    ctx.fillRect(0, 0, w, h);
    var txt = texto.value.trim();
    if (txt === '') { txt = w + ' x ' + h; }
    var tamanho = Math.max(8, Math.round(Math.min(w, h) / 8));
    if (tamTexto.value !== 'auto') { tamanho = Number(tamTexto.value); }
    ctx.textAlign = 'center';
    ctx.textBaseline = 'middle';
    ctx.font = 'bold ' + tamanho + 'px Arial, Helvetica, sans-serif';
    var largTxt = ctx.measureText(txt).width;
    if (largTxt > w * 0.92) {
      tamanho = Math.max(1, Math.floor(tamanho * w * 0.92 / largTxt));
      ctx.font = 'bold ' + tamanho + 'px Arial, Helvetica, sans-serif';
    }
    ctx.fillStyle = cT;
    ctx.fillText(txt, w / 2, h / 2);
    var nome = 'placeholder-' + w + 'x' + h + '.' + ext;
    if (ext === 'gif') {
      var dados = ctx.getImageData(0, 0, w, h).data;
      var bytes = criarGif(w, h, dados, rgb(cF), rgb(cT));
      sucesso(new Blob([bytes], { type: 'image/gif' }), nome, w, h, ext);
    } else {
      var tipo = 'image/png';
      if (ext === 'jpg') { tipo = 'image/jpeg'; }
      tela.toBlob(function (blob) {
        if (!blob) { erro('não foi possível gerar a imagem neste navegador.'); return; }
        sucesso(blob, nome, w, h, ext);
      }, tipo, 0.92);
    }
  }
  function baixar() {
    if (!atual) { return; }
    var url = URL.createObjectURL(atual.blob);
    var a = document.createElement('a');
    a.href = url;
    a.download = atual.nome;
    document.body.appendChild(a);
    a.click();
    document.body.removeChild(a);
    setTimeout(function () { URL.revokeObjectURL(url); }, 1500);
  }
  function limpar() {
    formato.value = 'png';
    corFundo.value = '#cccccc';
    corTexto.value = '#969696';
    texto.value = '';
    tamTexto.value = 'auto';
    tamanhos.value = '640x480';
    largura.value = '640';
    altura.value = '480';
    esconderSaida();
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    resultado.style.color = '#64748b';
    resultado.textContent = 'defina as opções e clique em "Gerar Imagem".';
  }
  tamanhos.addEventListener('change', function () {
    if (tamanhos.value !== 'custom') {
      var partes = tamanhos.value.split('x');
      largura.value = partes[0];
      altura.value = partes[1];
    }
  });
  largura.addEventListener('input', function () { tamanhos.value = 'custom'; });
  altura.addEventListener('input', function () { tamanhos.value = 'custom'; });
  document.getElementById('ph-gerar').addEventListener('click', gerar);
  document.getElementById('ph-limpar').addEventListener('click', limpar);
  btnBaixar.addEventListener('click', baixar);
  [texto, largura, altura].forEach(function (el) {
    el.addEventListener('keydown', function (e) { if (e.key === 'Enter') { gerar(); } });
  });
  Array.prototype.forEach.call(document.querySelectorAll('#gerador-placeholder input, #gerador-placeholder select'), function (el) {
    el.addEventListener('focus', function () { el.style.borderColor = '#6366f1'; });
    el.addEventListener('blur', function () { el.style.borderColor = '#c7d2fe'; });
  });
})();
</script>

## Como usar o gerador

1. Escolha a **Extensão do Arquivo** da imagem: PNG, JPG ou GIF.
2. Defina a **Cor do Fundo** e a **Cor do Texto** clicando nos seletores de cor.
3. Se quiser, digite um **Texto** para aparecer no centro da imagem. Deixando vazio, o gerador mostra a largura e a altura (por exemplo, `640 x 480`).
4. Escolha o **Tamanho do Texto** ou mantenha a opção Automático, que ajusta o texto ao tamanho da imagem.
5. Selecione uma das **Larguras Comuns** ou escolha Personalizado e digite a **Largura** e a **Altura** em pixels (de 1 a 2000).
6. Clique em **Gerar Imagem** (ou pressione Enter) para ver a prévia.
7. Clique em **Baixar Imagem** para salvar o arquivo no seu dispositivo.
8. Use o botão **Limpar** para voltar às opções iniciais.

A imagem é criada no próprio navegador, sem enviar nenhum dado para servidores.

## Entendendo os termos

- **Imagem placeholder:** imagem de espaço reservado, usada para ocupar o lugar de uma imagem final enquanto um site, app ou layout ainda está em desenvolvimento.
- **Extensão do arquivo:** formato em que a imagem é salva. O **PNG** mantém boa qualidade e é o mais indicado para cores lisas e textos, o **JPG** gera arquivos mais leves e o **GIF** é um formato antigo com até 256 cores.
- **Cor do fundo:** cor que preenche toda a imagem.
- **Cor do texto:** cor usada nas letras escritas no centro da imagem. Escolha uma cor com bom contraste em relação ao fundo.
- **Texto:** frase exibida no centro da imagem. Se ficar em branco, a imagem mostra as próprias dimensões.
- **Tamanho do texto:** altura das letras, em pixels. No modo Automático, o tamanho é calculado conforme as dimensões da imagem.
- **Larguras comuns:** tamanhos prontos e muito usados em testes, como 320x240, 640x480, 800x600, 1024x768 e 1600x1200.
- **Personalizado:** opção para informar qualquer largura e altura que você precisar.
- **Largura:** medida horizontal da imagem, em pixels.
- **Altura:** medida vertical da imagem, em pixels.
- **Pixel (px):** menor ponto de uma imagem digital. Quanto mais pixels, maior é a imagem e o arquivo gerado.