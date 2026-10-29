---
title: "Gerador de Código de Barras em Lote"
seoTitle: "Gerador de Código de Barras em Lote"
description: "Gerador de Código de Barras em Lote: crie vários códigos de barras de uma só vez. Grátis e online, sem cadastro."
summary: "Crie vários códigos de barras de uma só vez."
date: 2026-10-29
draft: false
category: "midia"
tags: ["código de barras", "códigos", "gerador"]
keywords: ["gerador de código de barras em lote", "gerador de código de barras em lote online", "código de barras", "códigos", "gerador"]
---
<!--INI SUDAH DIKERJAKAN-->

Basta escolher o tipo, digitar os valores (um por linha) e depois clicar em **Gerar Códigos**.

<div id="calc-barras-lote" style="max-width:560px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🏷️ Gerador de Código de Barras em Lote</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Informe os valores e gere vários códigos de uma só vez.</p>
<label for="blt-tipo" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Tipo</label>
<select id="blt-tipo" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<option value="code128">Code 128</option>
<option value="code39">Code 39</option>
<option value="ean13">EAN-13</option>
<option value="ean8">EAN-8</option>
<option value="upca">UPC-A</option>
<option value="isbn">ISBN-10 / ISBN-13</option>
<option value="itf">Interleaved 2 of 5</option>
<option value="std25">Standard 2 of 5</option>
<option value="codabar">Codabar</option>
<option value="msi">MSI Plessey</option>
<option value="code11">Code 11</option>
</select>
<div style="display:flex;gap:12px;flex-wrap:wrap;">
<div style="flex:1;min-width:140px;">
<label for="blt-rot" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Rotação</label>
<select id="blt-rot" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<option value="0">0°</option>
<option value="90">90°</option>
<option value="180">180°</option>
<option value="270">270°</option>
</select>
</div>
<div style="flex:1;min-width:140px;">
<label for="blt-fonte" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Fonte</label>
<select id="blt-fonte" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<option value="arial">Arial</option>
<option value="nenhuma">Sem Texto</option>
</select>
</div>
</div>
<div style="display:flex;gap:12px;flex-wrap:wrap;">
<div style="flex:1;min-width:140px;">
<label for="blt-altura" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Altura</label>
<input id="blt-altura" type="text" inputmode="numeric" value="80" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
</div>
<div style="flex:1;min-width:140px;">
<label for="blt-tamanho" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Tamanho</label>
<input id="blt-tamanho" type="text" inputmode="numeric" value="2" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
</div>
<div style="flex:1;min-width:140px;">
<label for="blt-margem" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Margem</label>
<input id="blt-margem" type="text" inputmode="numeric" value="10" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
</div>
</div>
<label for="blt-valores" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Valores</label>
<textarea id="blt-valores" rows="6" placeholder="Um valor por linha" autocomplete="off" spellcheck="false" style="width:100%;padding:12px 14px;margin-bottom:10px;font-size:1rem;font-family:ui-monospace,SFMono-Regular,Menlo,Consolas,monospace;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;resize:vertical;"></textarea>
<button type="button" id="blt-seq-abrir" style="margin-bottom:16px;padding:10px 16px;font-size:0.95rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Números sequenciais</button>
<div id="blt-seq" style="display:none;margin-bottom:16px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;">
<strong style="display:block;margin-bottom:12px;color:#3730a3;">Números Sequenciais</strong>
<div style="display:flex;gap:12px;flex-wrap:wrap;">
<div style="flex:1;min-width:120px;">
<label for="blt-seq-ini" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Primeiro</label>
<input id="blt-seq-ini" type="text" inputmode="numeric" placeholder="Ex.: 1000000" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:12px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
</div>
<div style="flex:1;min-width:120px;">
<label for="blt-seq-fim" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Último</label>
<input id="blt-seq-fim" type="text" inputmode="numeric" placeholder="Ex.: 1000009" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:12px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
</div>
</div>
<div style="display:flex;gap:12px;flex-wrap:wrap;">
<div style="flex:1;min-width:120px;">
<label for="blt-seq-pre" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Prefixo</label>
<input id="blt-seq-pre" type="text" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:12px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
</div>
<div style="flex:1;min-width:120px;">
<label for="blt-seq-suf" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Sufixo</label>
<input id="blt-seq-suf" type="text" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:12px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
</div>
</div>
<div id="blt-seq-msg" aria-live="polite" style="margin-bottom:10px;font-size:0.9rem;color:#b91c1c;"></div>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="blt-seq-inserir" style="flex:1;min-width:120px;padding:11px 16px;font-size:0.95rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Inserir</button>
<button type="button" id="blt-seq-fechar" style="padding:11px 16px;font-size:0.95rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Fechar</button>
</div>
</div>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="blt-gerar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Gerar Códigos</button>
<button type="button" id="blt-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="blt-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="blt-resultado">preencha os campos e clique em "Gerar Códigos".</span></div>
<div id="blt-saida" style="margin-top:16px;display:grid;gap:12px;"></div>
</div>
<script>
(function () {
  var NS = 'http://www.w3.org/2000/svg';
  function $(id) { return document.getElementById(id); }
  var tipo = $('blt-tipo'), rot = $('blt-rot'), fonte = $('blt-fonte');
  var altura = $('blt-altura'), tamanho = $('blt-tamanho'), margem = $('blt-margem');
  var valores = $('blt-valores'), saida = $('blt-saida');
  var caixa = $('blt-resposta'), resultado = $('blt-resultado');
  var seq = $('blt-seq'), seqMsg = $('blt-seq-msg');
  /* ---------- utilitários ---------- */
  function dg(pat) {
    var out = '', bar = true, i, k, w;
    for (i = 0; pat.length > i; i++) {
      w = parseInt(pat.charAt(i), 10);
      for (k = 0; w > k; k++) { out += bar ? '1' : '0'; }
      bar = !bar;
    }
    return out;
  }
  function wd(pat, wide) {
    var out = '', bar = true, i, k, w, c;
    for (i = 0; pat.length > i; i++) {
      c = pat.charAt(i);
      w = (c === 'w' || c === '1') ? wide : 1;
      for (k = 0; w > k; k++) { out += bar ? '1' : '0'; }
      bar = !bar;
    }
    return out;
  }
  function inteiro(v) {
    var t = String(v).trim();
    if (!/^\d+$/.test(t)) { return NaN; }
    return parseInt(t, 10);
  }
  function simples(bits, texto) { return { bits: bits, text: texto, groups: null, firstOut: '', lastOut: '' }; }
  /* ---------- Code 128 (conjuntos B e C) ---------- */
  var C128 = ('212222 222122 222221 121223 121322 131222 122213 122312 132212 221213 ' +
    '221312 231212 112232 122132 122231 113222 123122 123221 223211 221132 ' +
    '221231 213212 223112 312131 311222 321122 321221 312212 322112 322211 ' +
    '212123 212321 232121 111323 131123 131321 112313 132113 132311 211313 ' +
    '231113 231311 112133 112331 132131 113123 113321 133121 313121 211331 ' +
    '231131 213113 213311 213131 311123 311321 331121 312113 312311 332111 ' +
    '314111 221411 431111 111224 111422 121124 121421 141122 141221 112214 ' +
    '112412 122114 122411 142112 142211 241211 221114 413111 241112 134111 ' +
    '111242 121142 121241 114212 124112 124211 411212 421112 421211 212141 ' +
    '214121 412121 111143 111341 131141 114113 114311 411113 411311 113141 ' +
    '114131 311141 411131 211412 211214 211232 2331112').split(' ');
  function enc128(s) {
    var codes = [], i, c, soma;
    if (/^\d+$/.test(s) && s.length % 2 === 0) {
      codes.push(105);
      for (i = 0; s.length > i; i += 2) { codes.push(parseInt(s.substr(i, 2), 10)); }
    } else {
      codes.push(104);
      for (i = 0; s.length > i; i++) {
        c = s.charCodeAt(i);
        if (32 > c || c > 126) { throw new Error('caractere não suportado no Code 128.'); }
        codes.push(c - 32);
      }
    }
    soma = codes[0];
    for (i = 1; codes.length > i; i++) { soma += codes[i] * i; }
    codes.push(soma % 103);
    codes.push(106);
    return simples(codes.map(function (n) { return dg(C128[n]); }).join(''), s);
  }
  /* ---------- Code 39 ---------- */
  var C39 = {
    '0': 'nnnwwnwnn', '1': 'wnnwnnnnw', '2': 'nnwwnnnnw', '3': 'wnwwnnnnn', '4': 'nnnwwnnnw',
    '5': 'wnnwwnnnn', '6': 'nnwwwnnnn', '7': 'nnnwnnwnw', '8': 'wnnwnnwnn', '9': 'nnwwnnwnn',
    'A': 'wnnnnwnnw', 'B': 'nnwnnwnnw', 'C': 'wnwnnwnnn', 'D': 'nnnnwwnnw', 'E': 'wnnnwwnnn',
    'F': 'nnwnwwnnn', 'G': 'nnnnnwwnw', 'H': 'wnnnnwwnn', 'I': 'nnwnnwwnn', 'J': 'nnnnwwwnn',
    'K': 'wnnnnnnww', 'L': 'nnwnnnnww', 'M': 'wnwnnnnwn', 'N': 'nnnnwnnww', 'O': 'wnnnwnnwn',
    'P': 'nnwnwnnwn', 'Q': 'nnnnnnwww', 'R': 'wnnnnnwwn', 'S': 'nnwnnnwwn', 'T': 'nnnnwnwwn',
    'U': 'wwnnnnnnw', 'V': 'nwwnnnnnw', 'W': 'wwwnnnnnn', 'X': 'nwnnwnnnw', 'Y': 'wwnnwnnnn',
    'Z': 'nwwnwnnnn', '-': 'nwnnnnwnw', '.': 'wwnnnnwnn', ' ': 'nwwnnnwnn', '$': 'nwnwnwnnn',
    '/': 'nwnwnnnwn', '+': 'nwnnnwnwn', '%': 'nnnwnwnwn', '*': 'nwnnwnwnn'
  };
  function enc39(s) {
    var u = s.toUpperCase(), full = '*' + u + '*', bits = '', i, ch;
    for (i = 0; full.length > i; i++) {
      ch = full.charAt(i);
      if (!Object.prototype.hasOwnProperty.call(C39, ch) || (ch === '*' && i !== 0 && i !== full.length - 1)) {
        throw new Error('caractere não suportado no Code 39 (use A-Z, 0-9 e - . $ / + % espaço).');
      }
      bits += wd(C39[ch], 3) + (full.length - 1 === i ? '' : '0');
    }
    return simples(bits, u);
  }
  /* ---------- 2 of 5 ---------- */
  var W5 = ['nnwwn', 'wnnnw', 'nwnnw', 'wwnnn', 'nnwnw', 'wnwnn', 'nwwnn', 'nnnww', 'wnnwn', 'nwnwn'];
  function soDigitos(s) {
    if (!/^\d+$/.test(s)) { throw new Error('use apenas dígitos (0-9).'); }
  }
  function encItf(s) {
    var bits = '1010', i, k, a, b;
    soDigitos(s);
    if (s.length % 2 === 1) { s = '0' + s; }
    for (i = 0; s.length > i; i += 2) {
      a = W5[parseInt(s.charAt(i), 10)];
      b = W5[parseInt(s.charAt(i + 1), 10)];
      for (k = 0; 5 > k; k++) {
        bits += (a.charAt(k) === 'w' ? '111' : '1') + (b.charAt(k) === 'w' ? '000' : '0');
      }
    }
    return simples(bits + '11101', s);
  }
  function encStd25(s) {
    var bits = wd('wnwnnn', 3), i, k, p;
    soDigitos(s);
    for (i = 0; s.length > i; i++) {
      p = W5[parseInt(s.charAt(i), 10)];
      for (k = 0; 5 > k; k++) { bits += (p.charAt(k) === 'w' ? '111' : '1') + '0'; }
    }
    return simples(bits + wd('wnnnw', 3), s);
  }
  /* ---------- Codabar ---------- */
  var CB = {
    '0': 'nnnnnww', '1': 'nnnnwwn', '2': 'nnnwnnw', '3': 'wwnnnnn', '4': 'nnwnnwn',
    '5': 'wnnnnwn', '6': 'nwnnnnw', '7': 'nwnnwnn', '8': 'nwwnnnn', '9': 'wnnwnnn',
    '-': 'nnnwwnn', '$': 'nnwwnnn', ':': 'wnnnwnw', '/': 'wnwnnnw', '.': 'wnwnwnn',
    '+': 'nnwnwnw', 'A': 'nnwwnwn', 'B': 'nwnwnnw', 'C': 'nnnwnww', 'D': 'nnnwwwn'
  };
  function encCodabar(s) {
    var u = s.toUpperCase(), bits = '', i, ch;
    if (!/^[A-D]/.test(u)) { u = 'A' + u + 'A'; }
    for (i = 0; u.length > i; i++) {
      ch = u.charAt(i);
      if (!Object.prototype.hasOwnProperty.call(CB, ch)) {
        throw new Error('caractere não suportado no Codabar (use 0-9 e - $ : / . +).');
      }
      bits += wd(CB[ch], 3) + (u.length - 1 === i ? '' : '0');
    }
    return simples(bits, u);
  }
  /* ---------- MSI ---------- */
  function encMsi(s) {
    var bits = '110', i, b, k;
    soDigitos(s);
    for (i = 0; s.length > i; i++) {
      b = ('0000' + parseInt(s.charAt(i), 10).toString(2)).slice(-4);
      for (k = 0; 4 > k; k++) { bits += b.charAt(k) === '1' ? '110' : '100'; }
    }
    return simples(bits + '1001', s);
  }
  /* ---------- Code 11 ---------- */
  var C11 = {
    '0': '00001', '1': '10001', '2': '01001', '3': '11000', '4': '00101', '5': '10100',
    '6': '01100', '7': '00011', '8': '10010', '9': '10000', '-': '00100'
  };
  function encCode11(s) {
    var bits = wd('00110', 3) + '0', i, ch;
    for (i = 0; s.length > i; i++) {
      ch = s.charAt(i);
      if (!Object.prototype.hasOwnProperty.call(C11, ch)) { throw new Error('use apenas dígitos (0-9) e hífen.'); }
      bits += wd(C11[ch], 3) + '0';
    }
    return simples(bits + wd('00110', 3), s);
  }
  /* ---------- EAN / UPC / ISBN ---------- */
  var L = ['0001101', '0011001', '0010011', '0111101', '0100011', '0110001', '0101111', '0111011', '0110111', '0001011'];
  var PAR = ['LLLLLL', 'LLGLGG', 'LLGGLG', 'LLGGGL', 'LGLLGG', 'LGGLLG', 'LGGGLL', 'LGLGLG', 'LGLGGL', 'LGGLGL'];
  function comp(s) {
    var o = '', i;
    for (i = 0; s.length > i; i++) { o += s.charAt(i) === '1' ? '0' : '1'; }
    return o;
  }
  function codigoR(d) { return comp(L[d]); }
  function codigoG(d) { return comp(L[d]).split('').reverse().join(''); }
  function dv(s) {
    var soma = 0, i, pos;
    for (i = 0; s.length > i; i++) {
      pos = s.length - i;
      soma += parseInt(s.charAt(i), 10) * (pos % 2 === 1 ? 3 : 1);
    }
    return (10 - soma % 10) % 10;
  }
  function lerEan(s, len) {
    var c;
    s = s.replace(/[\s-]/g, '');
    soDigitos(s);
    if (s.length === len - 1) {
      s += dv(s);
    } else if (s.length === len) {
      c = dv(s.substr(0, len - 1));
      if (String(c) !== s.charAt(len - 1)) { throw new Error('dígito verificador inválido (o correto é ' + c + ').'); }
    } else {
      throw new Error('informe ' + (len - 1) + ' ou ' + len + ' dígitos.');
    }
    return s;
  }
  function bits13(d) {
    var par = PAR[parseInt(d.charAt(0), 10)], bits = '101', i, n;
    for (i = 1; 7 > i; i++) {
      n = parseInt(d.charAt(i), 10);
      bits += par.charAt(i - 1) === 'L' ? L[n] : codigoG(n);
    }
    bits += '01010';
    for (i = 7; 13 > i; i++) { bits += codigoR(parseInt(d.charAt(i), 10)); }
    return bits + '101';
  }
  function encEan13(s) {
    var d = lerEan(s, 13);
    return { bits: bits13(d), text: d, firstOut: d.charAt(0), lastOut: '',
      groups: [{ t: d.substr(1, 6), from: 3, to: 45 }, { t: d.substr(7, 6), from: 50, to: 92 }] };
  }
  function encUpcA(s) {
    var d = lerEan(s, 12);
    return { bits: bits13('0' + d), text: d, firstOut: d.charAt(0), lastOut: d.charAt(11),
      groups: [{ t: d.substr(1, 5), from: 10, to: 45 }, { t: d.substr(6, 5), from: 50, to: 85 }] };
  }
  function encEan8(s) {
    var d = lerEan(s, 8), bits = '101', i;
    for (i = 0; 4 > i; i++) { bits += L[parseInt(d.charAt(i), 10)]; }
    bits += '01010';
    for (i = 4; 8 > i; i++) { bits += codigoR(parseInt(d.charAt(i), 10)); }
    return { bits: bits + '101', text: d, firstOut: '', lastOut: '',
      groups: [{ t: d.substr(0, 4), from: 3, to: 31 }, { t: d.substr(4, 4), from: 36, to: 64 }] };
  }
  function encIsbn(s) {
    var u = s.replace(/[\s-]/g, '').toUpperCase(), d;
    if (/^\d{9}[\dX]$/.test(u)) {
      d = '978' + u.substr(0, 9);
      d += dv(d);
    } else {
      d = lerEan(u, 13);
    }
    if (d.substr(0, 3) !== '978' && d.substr(0, 3) !== '979') { throw new Error('o ISBN deve começar com 978 ou 979.'); }
    return encEan13(d);
  }
  var ENC = {
    code128: enc128, code39: enc39, ean13: encEan13, ean8: encEan8, upca: encUpcA, isbn: encIsbn,
    itf: encItf, std25: encStd25, codabar: encCodabar, msi: encMsi, code11: encCode11
  };
  /* ---------- desenho em SVG ---------- */
  function mk(name, attrs, parent) {
    var n = document.createElementNS(NS, name), k;
    for (k in attrs) {
      if (Object.prototype.hasOwnProperty.call(attrs, k)) { n.setAttribute(k, attrs[k]); }
    }
    if (parent) { parent.appendChild(n); }
    return n;
  }
  function desenhar(enc, o) {
    var size = o.tamanho, bits = enc.bits, fs = Math.max(11, size * 6);
    var extra = Math.round(fs * 0.8) + 4;
    var padL = o.margem + (enc.firstOut ? extra : 0);
    var padR = o.margem + (enc.lastOut ? extra : 0);
    var barsW = bits.length * size;
    var W = padL + barsW + padR;
    var H = o.margem + o.altura + (o.texto ? fs + 6 : 0) + o.margem;
    var troca = (o.rotacao === 90 || o.rotacao === 270);
    var ow = troca ? H : W, oh = troca ? W : H;
    var svg = mk('svg', { width: ow, height: oh, viewBox: '0 0 ' + ow + ' ' + oh });
    var g, i = 0, j, ty, t;
    svg.style.display = 'block';
    svg.style.maxWidth = '100%';
    svg.style.height = 'auto';
    mk('rect', { x: 0, y: 0, width: ow, height: oh, fill: '#ffffff' }, svg);
    g = mk('g', {}, svg);
    if (o.rotacao === 90) { g.setAttribute('transform', 'translate(' + H + ',0) rotate(90)'); }
    if (o.rotacao === 180) { g.setAttribute('transform', 'translate(' + W + ',' + H + ') rotate(180)'); }
    if (o.rotacao === 270) { g.setAttribute('transform', 'translate(0,' + W + ') rotate(270)'); }
    while (bits.length > i) {
      if (bits.charAt(i) === '1') {
        j = i;
        while (bits.length > j && bits.charAt(j) === '1') { j++; }
        mk('rect', { x: padL + i * size, y: o.margem, width: (j - i) * size, height: o.altura, fill: '#000000' }, g);
        i = j;
      } else {
        i++;
      }
    }
    if (o.texto) {
      ty = o.margem + o.altura + fs + 1;
      t = function (x, ancora, str, esp) {
        var n = mk('text', { x: x, y: ty, 'text-anchor': ancora, 'font-family': 'Arial, Helvetica, sans-serif',
          'font-size': fs, 'letter-spacing': esp, fill: '#000000' }, g);
        n.textContent = str;
      };
      if (enc.groups) {
        enc.groups.forEach(function (gp) { t(padL + ((gp.from + gp.to) / 2) * size, 'middle', gp.t, Math.round(size * 1.5)); });
        if (enc.firstOut) { t(padL - 3, 'end', enc.firstOut, 0); }
        if (enc.lastOut) { t(padL + barsW + 3, 'start', enc.lastOut, 0); }
      } else {
        t(padL + barsW / 2, 'middle', enc.text, 0);
      }
    }
    return svg;
  }
  /* ---------- interface ---------- */
  function aviso(texto, tipoAviso) {
    caixa.style.borderColor = tipoAviso === 'ok' ? '#86efac' : (tipoAviso === 'erro' ? '#fca5a5' : '#c7d2fe');
    caixa.style.background = tipoAviso === 'ok' ? '#f0fdf4' : (tipoAviso === 'erro' ? '#fef2f2' : '#ffffff');
    resultado.style.color = tipoAviso === 'ok' ? '#166534' : (tipoAviso === 'erro' ? '#b91c1c' : '#64748b');
    resultado.textContent = texto;
  }
  function esvaziar() {
    while (saida.firstChild) { saida.removeChild(saida.firstChild); }
  }
  function cartao(codigo, svg, erro) {
    var c = document.createElement('div'), a, nome;
    c.style.cssText = 'padding:12px;border-radius:12px;text-align:center;overflow-x:auto;box-sizing:border-box;' +
      (erro ? 'background:#fef2f2;border:2px solid #fca5a5;color:#b91c1c;text-align:left;' : 'background:#ffffff;border:2px solid #c7d2fe;');
    if (erro) {
      c.textContent = '"' + codigo + '": ' + erro;
    } else {
      svg.style.margin = '0 auto';
      c.appendChild(svg);
      nome = 'codigo-' + codigo.replace(/[^A-Za-z0-9_-]/g, '_') + '.svg';
      a = document.createElement('a');
      a.textContent = 'Baixar SVG';
      a.download = nome;
      a.href = 'data:image/svg+xml;charset=utf-8,' + encodeURIComponent(new XMLSerializer().serializeToString(svg));
      a.style.cssText = 'display:inline-block;margin-top:10px;padding:8px 14px;font-size:0.9rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;text-decoration:none;';
      c.appendChild(a);
    }
    saida.appendChild(c);
  }
  function gerar() {
    var h = inteiro(altura.value), s = inteiro(tamanho.value), m = inteiro(margem.value);
    var linhas, ok = 0, falhas = 0, op;
    esvaziar();
    if (isNaN(h) || 10 > h || h > 500) { aviso('a altura deve ser um número entre 10 e 500.', 'erro'); return; }
    if (isNaN(s) || 1 > s || s > 10) { aviso('o tamanho deve ser um número entre 1 e 10.', 'erro'); return; }
    if (isNaN(m) || m > 100) { aviso('a margem deve ser um número entre 0 e 100.', 'erro'); return; }
    linhas = valores.value.split(/\r?\n/).map(function (v) { return v.trim(); }).filter(function (v) { return v !== ''; });
    if (linhas.length === 0) { aviso('informe pelo menos um valor.', 'erro'); return; }
    if (linhas.length > 1000) { aviso('o máximo é 1000 códigos por vez.', 'erro'); return; }
    op = { altura: h, tamanho: s, margem: m, rotacao: parseInt(rot.value, 10), texto: fonte.value !== 'nenhuma' };
    linhas.forEach(function (v) {
      try {
        cartao(v, desenhar(ENC[tipo.value](v), op), '');
        ok++;
      } catch (e) {
        cartao(v, null, e.message);
        falhas++;
      }
    });
    if (ok === 0) {
      aviso('nenhum código foi gerado. Verifique os valores informados.', 'erro');
    } else {
      aviso(ok + ' código(s) gerado(s)' + (falhas > 0 ? ' e ' + falhas + ' valor(es) inválido(s).' : '.'), 'ok');
    }
  }
  function limpar() {
    valores.value = '';
    esvaziar();
    aviso('preencha os campos e clique em "Gerar Códigos".', '');
    valores.focus();
  }
  function inserirSequencia() {
    var ini = $('blt-seq-ini').value.trim(), fim = $('blt-seq-fim').value.trim();
    var a = inteiro(ini), b = inteiro(fim), pre = $('blt-seq-pre').value, suf = $('blt-seq-suf').value;
    var largura, out = [], n, s;
    if (isNaN(a) || isNaN(b)) { seqMsg.textContent = 'informe números inteiros em "Primeiro" e "Último".'; return; }
    if (a > b) { seqMsg.textContent = 'o último deve ser maior ou igual ao primeiro.'; return; }
    if (b - a >= 1000) { seqMsg.textContent = 'o máximo é 1000 códigos por vez.'; return; }
    largura = (ini.length > 1 && ini.charAt(0) === '0') ? ini.length : 0;
    n = a;
    while (b >= n) {
      s = String(n);
      while (largura > s.length) { s = '0' + s; }
      out.push(pre + s + suf);
      n++;
    }
    valores.value = out.join('\n');
    seqMsg.textContent = '';
    seq.style.display = 'none';
  }
  valores.value = '1000000\n1000001\n1000002';
  $('blt-gerar').addEventListener('click', gerar);
  $('blt-limpar').addEventListener('click', limpar);
  $('blt-seq-abrir').addEventListener('click', function () {
    seq.style.display = seq.style.display === 'none' ? 'block' : 'none';
  });
  $('blt-seq-fechar').addEventListener('click', function () { seq.style.display = 'none'; seqMsg.textContent = ''; });
  $('blt-seq-inserir').addEventListener('click', inserirSequencia);
  ['blt-tipo', 'blt-rot', 'blt-fonte', 'blt-altura', 'blt-tamanho', 'blt-margem', 'blt-valores',
    'blt-seq-ini', 'blt-seq-fim', 'blt-seq-pre', 'blt-seq-suf'].forEach(function (id) {
    var el = $(id);
    el.addEventListener('focus', function () { el.style.borderColor = '#6366f1'; });
    el.addEventListener('blur', function () { el.style.borderColor = '#c7d2fe'; });
  });
})();
</script>

## Como usar a ferramenta

1. Escolha o **Tipo** de código de barras (por exemplo, Code 128 ou EAN-13).
2. Ajuste, se quiser, a **Rotação**, a **Fonte**, a **Altura**, o **Tamanho** e a **Margem**.
3. Digite os **Valores** no campo de texto, um por linha. Para criar uma lista numerada automaticamente, clique em **Números sequenciais**, preencha os campos e clique em **Inserir**.
4. Clique em **Gerar Códigos** para ver todos os códigos de barras de uma vez.
5. Use o link **Baixar SVG** abaixo de cada código para salvar a imagem, ou o botão **Limpar** para recomeçar.

Valores inválidos para o tipo escolhido aparecem em vermelho, com a explicação do problema, sem impedir a geração dos demais. Cada geração aceita até 1000 valores.

## Entendendo os termos

- **Código de barras:** representação de números ou textos em barras de larguras diferentes, que pode ser lida por um leitor óptico.
- **Lote:** conjunto de vários códigos gerados de uma só vez, a partir de uma lista de valores.
- **Tipo:** padrão (simbologia) usado para codificar o valor, que define quais caracteres são aceitos e como as barras são desenhadas.
- **Code 128:** tipo versátil que aceita letras, números e símbolos, muito usado em logística e etiquetas.
- **Code 39:** tipo que aceita letras maiúsculas, números e alguns símbolos (- . $ / + % e espaço).
- **EAN-13:** tipo com 13 dígitos usado nos produtos de varejo. O último dígito é o dígito verificador.
- **EAN-8:** versão curta do EAN-13, com 8 dígitos, usada em embalagens pequenas.
- **UPC-A:** tipo com 12 dígitos, usado principalmente nos Estados Unidos e no Canadá.
- **ISBN:** número internacional que identifica livros, gerado como EAN-13 iniciado em 978 ou 979 (também aceita ISBN-10).
- **Interleaved 2 of 5:** tipo que aceita só dígitos, em quantidade par (um zero é adicionado à esquerda se o total for ímpar).
- **Standard 2 of 5:** tipo numérico mais simples, que aceita apenas dígitos.
- **Codabar:** tipo que aceita dígitos e alguns símbolos, com letras A a D no início e no fim, comum em bibliotecas e bancos de sangue.
- **MSI Plessey:** tipo numérico usado em controle de estoque e prateleiras.
- **Code 11:** tipo que aceita dígitos e hífen, usado em telecomunicações.
- **Dígito verificador:** último dígito calculado a partir dos outros, usado para detectar erros de leitura. Se você informar um dígito a menos nos tipos EAN, UPC e ISBN, ele é calculado automaticamente.
- **Rotação:** ângulo de giro do código (0°, 90°, 180° ou 270°).
- **Fonte:** define se o texto do valor aparece abaixo das barras (Arial) ou não (Sem Texto).
- **Altura:** altura das barras, em pixels.
- **Tamanho:** largura de cada módulo (a barra mais fina), em pixels. Quanto maior, mais largo o código.
- **Margem:** espaço em branco ao redor do código, em pixels.
- **Valores:** lista dos textos ou números que serão convertidos em códigos, um por linha.
- **Números sequenciais:** recurso que preenche a lista de valores automaticamente, do primeiro ao último número.
- **Prefixo e Sufixo:** textos adicionados antes e depois de cada número da sequência (por exemplo, `PED-` e `-BR`).
- **SVG:** formato de imagem vetorial, que pode ser ampliado sem perder qualidade e é ideal para impressão.