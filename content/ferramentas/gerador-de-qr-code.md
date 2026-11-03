---
title: "Gerador de QR Code"
seoTitle: "Gerador de QR Code"
description: "Gerador de QR Code: crie QR Codes de links e textos e baixe a imagem. Grátis e online, sem cadastro."
summary: "Crie QR Codes de links e textos e baixe a imagem."
date: 2026-11-03
draft: false
category: "midia"
tags: ["qr code", "códigos", "links", "gerador"]
keywords: ["gerador de qr code", "gerador de qr code online", "qr code", "códigos", "links"]
---
<!--INI SUDAH DIKERJAKAN-->

Escolha o tamanho da imagem, digite um texto ou cole um link abaixo e clique em **Gerar QR Code**.

<div id="qr-gerador" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🔳 Gerador de QR Code</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Escolha o tamanho, digite o texto ou cole um link e gere o QR Code.</p>
<label for="qr-tamanho" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Tamanho da imagem</label>
<select id="qr-tamanho" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<option value="100">Pequeno (100x100)</option>
<option value="300" selected>Médio (300x300)</option>
<option value="500">Grande (500x500)</option>
</select>
<label for="qr-texto" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Texto ou URL</label>
<textarea id="qr-texto" rows="4" placeholder="Ex.: https://www.exemplo.com.br" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:20px;font-size:1rem;font-family:inherit;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;resize:vertical;"></textarea>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="qr-gerar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Gerar QR Code</button>
<button type="button" id="qr-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="qr-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="qr-resultado">preencha o texto e clique em "Gerar QR Code".</span>
<div id="qr-saida" style="display:none;margin-top:14px;text-align:center;">
<canvas id="qr-canvas" width="300" height="300" style="max-width:100%;height:auto;border:1px solid #c7d2fe;border-radius:8px;background:#ffffff;image-rendering:pixelated;"></canvas>
<div style="margin-top:12px;"><button type="button" id="qr-baixar" style="padding:12px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">⬇ Baixar imagem (PNG)</button></div>
</div>
</div>
</div>
<script>
(function () {
  var ECC_PER_BLOCK = [
    [-1,7,10,15,20,26,18,20,24,30,18,20,24,26,30,22,24,28,30,28,28,28,28,30,30,26,28,30,30,30,30,30,30,30,30,30,30,30,30,30,30],
    [-1,10,16,26,18,24,16,18,22,22,26,30,22,22,24,24,28,28,26,26,26,26,28,28,28,28,28,28,28,28,28,28,28,28,28,28,28,28,28,28,28],
    [-1,13,22,18,26,18,24,18,22,20,24,28,26,24,20,30,24,28,28,26,30,28,30,30,30,30,28,30,30,30,30,30,30,30,30,30,30,30,30,30,30],
    [-1,17,28,22,16,22,28,26,26,24,28,24,28,22,24,24,30,28,28,26,28,30,24,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30]
  ];
  var NUM_BLOCKS = [
    [-1,1,1,1,1,1,2,2,2,2,4,4,4,4,4,6,6,6,6,7,8,8,9,9,10,12,12,12,13,14,15,16,17,18,19,19,20,21,22,24,25],
    [-1,1,1,1,2,2,4,4,4,5,5,5,8,9,9,10,10,11,13,14,16,17,17,18,20,21,23,25,26,28,29,31,33,35,37,38,40,43,45,47,49],
    [-1,1,1,2,2,4,4,6,6,8,8,8,10,12,16,12,17,16,18,21,20,23,23,25,27,29,34,34,35,38,40,43,45,48,51,53,56,59,62,65,68],
    [-1,1,1,2,4,4,6,6,8,8,11,11,16,16,16,18,16,19,21,25,25,25,34,30,32,35,37,40,42,45,48,51,54,57,60,63,66,70,74,77,81]
  ];
  var FORMAT_BITS = [1, 0, 3, 2];
  function rawModules(v) {
    var r = (16 * v + 128) * v + 64;
    if (v >= 2) {
      var n = Math.floor(v / 7) + 2;
      r -= (25 * n - 10) * n - 55;
      if (v >= 7) { r -= 36; }
    }
    return r;
  }
  function dataCodewords(v, e) {
    return Math.floor(rawModules(v) / 8) - ECC_PER_BLOCK[e][v] * NUM_BLOCKS[e][v];
  }
  function gfMul(x, y) {
    var z = 0;
    for (var i = 7; i >= 0; i--) {
      z = (z << 1) ^ ((z >>> 7) * 0x11D);
      z ^= ((y >>> i) & 1) * x;
    }
    return z;
  }
  function rsDivisor(deg) {
    var r = [], i, j;
    for (i = 0; i < deg - 1; i++) { r.push(0); }
    r.push(1);
    var root = 1;
    for (i = 0; i < deg; i++) {
      for (j = 0; j < r.length; j++) {
        r[j] = gfMul(r[j], root);
        if (j + 1 < r.length) { r[j] ^= r[j + 1]; }
      }
      root = gfMul(root, 2);
    }
    return r;
  }
  function rsRemainder(data, div) {
    var r = div.map(function () { return 0; });
    data.forEach(function (b) {
      var f = b ^ r.shift();
      r.push(0);
      div.forEach(function (c, i) { r[i] ^= gfMul(c, f); });
    });
    return r;
  }
  function utf8Bytes(text) {
    var s = unescape(encodeURIComponent(text)), out = [];
    for (var i = 0; i < s.length; i++) { out.push(s.charCodeAt(i)); }
    return out;
  }
  function penalty(m, size) {
    var x, y, k, run, p = 0, dark = 0;
    var pa = [1,0,1,1,1,0,1,0,0,0,0], pb = [0,0,0,0,1,0,1,1,1,0,1];
    function match(get, pat) {
      for (var i = 0; i < 11; i++) { if (get(i) !== pat[i]) { return false; } }
      return true;
    }
    for (y = 0; y < size; y++) {
      for (x = 0; x < size; x++) {
        if (m[y][x]) { dark++; }
        if (x + 1 < size && y + 1 < size && m[y][x] === m[y][x + 1] && m[y][x] === m[y + 1][x] && m[y][x] === m[y + 1][x + 1]) { p += 3; }
      }
    }
    for (k = 0; k < 2; k++) {
      for (y = 0; y < size; y++) {
        run = 1;
        for (x = 1; x <= size; x++) {
          var cur = x < size ? (k ? m[x][y] : m[y][x]) : null;
          var prev = k ? m[x - 1][y] : m[y][x - 1];
          if (cur === prev) { run++; } else { if (run >= 5) { p += run - 2; } run = 1; }
        }
        for (x = 0; x + 11 <= size; x++) {
          var g = (function (xx, yy, kk) { return function (i) { return (kk ? m[xx + i][yy] : m[yy][xx + i]) ? 1 : 0; }; })(x, y, k);
          if (match(g, pa) || match(g, pb)) { p += 40; }
        }
      }
    }
    var total = size * size;
    p += (Math.ceil(Math.abs(dark * 20 - total * 10) / total) - 1) * 10;
    return p;
  }
  function qrEncode(text, ecl) {
    var bytes = utf8Bytes(text), ver, i, j, bits = [];
    function put(val, len) { for (var b = len - 1; b >= 0; b--) { bits.push((val >>> b) & 1); } }
    for (ver = 1; ver <= 40; ver++) {
      var cc = ver <= 9 ? 8 : 16;
      if (4 + cc + bytes.length * 8 <= dataCodewords(ver, ecl) * 8) { break; }
    }
    if (ver > 40) { throw new Error('Texto muito longo para um QR Code.'); }
    put(4, 4);
    put(bytes.length, ver <= 9 ? 8 : 16);
    bytes.forEach(function (b) { put(b, 8); });
    var cap = dataCodewords(ver, ecl) * 8;
    put(0, Math.min(4, cap - bits.length));
    while (bits.length % 8 !== 0) { bits.push(0); }
    for (var pad = 0xEC; bits.length < cap; pad ^= 0xEC ^ 0x11) { put(pad, 8); }
    var data = [];
    for (i = 0; i < bits.length; i += 8) {
      var v = 0;
      for (j = 0; j < 8; j++) { v = (v << 1) | bits[i + j]; }
      data.push(v);
    }
    var nb = NUM_BLOCKS[ecl][ver], eccLen = ECC_PER_BLOCK[ecl][ver];
    var raw = Math.floor(rawModules(ver) / 8), nShort = nb - raw % nb, shortLen = Math.floor(raw / nb);
    var blocks = [], div = rsDivisor(eccLen), k = 0;
    for (i = 0; i < nb; i++) {
      var dl = shortLen - eccLen + (i < nShort ? 0 : 1);
      var dat = data.slice(k, k + dl);
      k += dl;
      var ecc = rsRemainder(dat, div);
      if (i < nShort) { dat.push(0); }
      blocks.push(dat.concat(ecc));
    }
    var all = [];
    for (i = 0; i < blocks[0].length; i++) {
      for (j = 0; j < blocks.length; j++) {
        if (i !== shortLen - eccLen || j >= nShort) { all.push(blocks[j][i]); }
      }
    }
    var size = ver * 4 + 17, m = [], fn = [];
    for (i = 0; i < size; i++) {
      m.push([]); fn.push([]);
      for (j = 0; j < size; j++) { m[i].push(false); fn[i].push(false); }
    }
    function setFn(x, y, d) { m[y][x] = d; fn[y][x] = true; }
    function bit(n, i) { return ((n >>> i) & 1) !== 0; }
    function formatBits(mask) {
      var d = (FORMAT_BITS[ecl] << 3) | mask, r = d, t;
      for (t = 0; t < 10; t++) { r = (r << 1) ^ ((r >>> 9) * 0x537); }
      var f = ((d << 10) | r) ^ 0x5412;
      for (t = 0; t <= 5; t++) { setFn(8, t, bit(f, t)); }
      setFn(8, 7, bit(f, 6)); setFn(8, 8, bit(f, 7)); setFn(7, 8, bit(f, 8));
      for (t = 9; t < 15; t++) { setFn(14 - t, 8, bit(f, t)); }
      for (t = 0; t < 8; t++) { setFn(size - 1 - t, 8, bit(f, t)); }
      for (t = 8; t < 15; t++) { setFn(8, size - 15 + t, bit(f, t)); }
      setFn(8, size - 8, true);
    }
    for (i = 0; i < size; i++) { setFn(6, i, i % 2 === 0); setFn(i, 6, i % 2 === 0); }
    function finder(cx, cy) {
      for (var dy = -4; dy <= 4; dy++) {
        for (var dx = -4; dx <= 4; dx++) {
          var d = Math.max(Math.abs(dx), Math.abs(dy)), xx = cx + dx, yy = cy + dy;
          if (xx >= 0 && xx < size && yy >= 0 && yy < size) { setFn(xx, yy, d !== 2 && d !== 4); }
        }
      }
    }
    finder(3, 3); finder(size - 4, 3); finder(3, size - 4);
    var pos = [];
    if (ver > 1) {
      var na = Math.floor(ver / 7) + 2;
      var step = ver === 32 ? 26 : Math.floor((ver * 8 + na * 3 + 5) / (na * 4 - 4)) * 2;
      pos = [6];
      for (var ps = size - 7; pos.length < na; ps -= step) { pos.splice(1, 0, ps); }
    }
    for (i = 0; i < pos.length; i++) {
      for (j = 0; j < pos.length; j++) {
        if ((i === 0 && j === 0) || (i === 0 && j === pos.length - 1) || (i === pos.length - 1 && j === 0)) { continue; }
        for (var ay = -2; ay <= 2; ay++) {
          for (var ax = -2; ax <= 2; ax++) { setFn(pos[i] + ax, pos[j] + ay, Math.max(Math.abs(ax), Math.abs(ay)) !== 1); }
        }
      }
    }
    formatBits(0);
    if (ver >= 7) {
      var vr = ver, t2;
      for (t2 = 0; t2 < 12; t2++) { vr = (vr << 1) ^ ((vr >>> 11) * 0x1F25); }
      var vb = (ver << 12) | vr;
      for (t2 = 0; t2 < 18; t2++) {
        var a = size - 11 + t2 % 3, b2 = Math.floor(t2 / 3);
        setFn(a, b2, bit(vb, t2)); setFn(b2, a, bit(vb, t2));
      }
    }
    var n = 0;
    for (var right = size - 1; right >= 1; right -= 2) {
      if (right === 6) { right = 5; }
      for (var vert = 0; vert < size; vert++) {
        for (j = 0; j < 2; j++) {
          var x = right - j, up = ((right + 1) & 2) === 0, y = up ? size - 1 - vert : vert;
          if (!fn[y][x] && n < all.length * 8) {
            m[y][x] = bit(all[n >>> 3], 7 - (n & 7));
            n++;
          }
        }
      }
    }
    function applyMask(mask) {
      for (var y = 0; y < size; y++) {
        for (var x = 0; x < size; x++) {
          var inv;
          switch (mask) {
            case 0: inv = (x + y) % 2 === 0; break;
            case 1: inv = y % 2 === 0; break;
            case 2: inv = x % 3 === 0; break;
            case 3: inv = (x + y) % 3 === 0; break;
            case 4: inv = (Math.floor(x / 3) + Math.floor(y / 2)) % 2 === 0; break;
            case 5: inv = x * y % 2 + x * y % 3 === 0; break;
            case 6: inv = (x * y % 2 + x * y % 3) % 2 === 0; break;
            default: inv = ((x + y) % 2 + x * y % 3) % 2 === 0;
          }
          if (!fn[y][x] && inv) { m[y][x] = !m[y][x]; }
        }
      }
    }
    var best = 0, bestScore = Infinity;
    for (var mk = 0; mk < 8; mk++) {
      formatBits(mk);
      applyMask(mk);
      var sc = penalty(m, size);
      applyMask(mk);
      if (sc < bestScore) { bestScore = sc; best = mk; }
    }
    formatBits(best);
    applyMask(best);
    return m;
  }
  var tamanho = document.getElementById('qr-tamanho');
  var texto = document.getElementById('qr-texto');
  var resultado = document.getElementById('qr-resultado');
  var caixa = document.getElementById('qr-resposta');
  var saida = document.getElementById('qr-saida');
  var canvas = document.getElementById('qr-canvas');
  function erro(msg) {
    saida.style.display = 'none';
    caixa.style.borderColor = '#fca5a5';
    caixa.style.background = '#fef2f2';
    resultado.style.color = '#b91c1c';
    resultado.textContent = msg;
  }
  function gerar() {
    var t = texto.value;
    if (t.trim() === '') { erro('digite um texto ou cole uma URL para gerar o QR Code.'); return; }
    var m;
    try { m = qrEncode(t, 1); } catch (e) { erro('o texto é muito longo para caber em um QR Code. Use um texto menor.'); return; }
    var n = m.length;
    var total = n + 8;
    var alvo = parseInt(tamanho.value, 10);
    var cel = Math.max(1, Math.floor(alvo / total));
    var dim = Math.max(alvo, cel * total);
    var ctx = canvas.getContext('2d');
    canvas.width = dim;
    canvas.height = dim;
    ctx.fillStyle = '#ffffff';
    ctx.fillRect(0, 0, dim, dim);
    ctx.fillStyle = '#000000';
    var ini = Math.floor((dim - cel * n) / 2);
    for (var y = 0; y < n; y++) {
      for (var x = 0; x < n; x++) {
        if (m[y][x]) { ctx.fillRect(ini + x * cel, ini + y * cel, cel, cel); }
      }
    }
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    resultado.textContent = 'QR Code gerado com sucesso (' + dim + 'x' + dim + ' px).' + (dim > alvo ? ' A imagem foi ampliada para que o QR Code continue legível.' : '');
    saida.style.display = 'block';
  }
  function baixar() {
    var a = document.createElement('a');
    a.href = canvas.toDataURL('image/png');
    a.download = 'qrcode.png';
    document.body.appendChild(a);
    a.click();
    document.body.removeChild(a);
  }
  function limpar() {
    texto.value = '';
    tamanho.value = '300';
    saida.style.display = 'none';
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    resultado.style.color = '#64748b';
    resultado.textContent = 'preencha o texto e clique em "Gerar QR Code".';
    texto.focus();
  }
  document.getElementById('qr-gerar').addEventListener('click', gerar);
  document.getElementById('qr-baixar').addEventListener('click', baixar);
  document.getElementById('qr-limpar').addEventListener('click', limpar);
  texto.addEventListener('keydown', function (e) { if (e.key === 'Enter' && (e.ctrlKey || e.metaKey)) { gerar(); } });
  [tamanho, texto].forEach(function (el) {
    el.addEventListener('focus', function () { el.style.borderColor = '#6366f1'; });
    el.addEventListener('blur', function () { el.style.borderColor = '#c7d2fe'; });
  });
})();
</script>

## Como usar o gerador

1. Escolha o **Tamanho da imagem**: Pequeno (100x100), Médio (300x300) ou Grande (500x500).
2. Digite um texto ou cole uma URL no campo **Texto ou URL**.
3. Clique em **Gerar QR Code** (ou pressione Ctrl + Enter dentro do campo de texto) para ver o resultado.
4. Clique em **Baixar imagem (PNG)** para salvar o QR Code no seu dispositivo.
5. Use o botão **Limpar** para apagar tudo e criar um novo QR Code.

Antes de imprimir ou publicar, teste o código apontando a câmera do celular para a tela. Quanto maior o texto, mais denso fica o desenho do QR Code, por isso prefira o tamanho Médio ou Grande para textos longos.

## Entendendo os termos

- **QR Code:** código de barras em formato de quadrado (Quick Response Code) que guarda textos, links, números de telefone e outras informações e pode ser lido pela câmera do celular.
- **Tamanho da imagem:** dimensão da imagem gerada, medida em pixels. Quanto maior, mais nítido o QR Code fica ao ser impresso ou ampliado.
- **Pixel (px):** menor ponto de uma imagem digital. Um tamanho de 300x300 significa 300 pixels de largura por 300 de altura.
- **Texto ou URL:** conteúdo que ficará dentro do QR Code. Pode ser uma frase, um número ou o endereço de um site.
- **URL:** endereço de uma página na internet, como `https://www.exemplo.com.br`.
- **Gerar QR Code:** botão que transforma o texto digitado em uma imagem de QR Code.
- **PNG:** formato de imagem usado no download, com boa qualidade e fundo nítido.
- **Escanear:** ler o QR Code com a câmera do celular ou com um aplicativo leitor, para abrir o link ou ver a informação guardada.
- **Margem de segurança:** borda branca ao redor do QR Code, necessária para que os leitores reconheçam o desenho com facilidade.