---
title: "Gerador de Código de Barras"
seoTitle: "Gerador de Código de Barras"
description: "Gerador de Código de Barras: crie códigos de barras nos formatos mais usados. Grátis e online, sem cadastro."
summary: "Crie códigos de barras nos formatos mais usados."
date: 2026-10-29
draft: false
category: "midia"
tags: ["código de barras", "códigos", "gerador"]
keywords: ["gerador de código de barras", "gerador de código de barras online", "código de barras", "códigos", "gerador"]
---

Basta escolher o tipo, digitar o código abaixo e clicar em **Gerar Imagem**.

<div id="gerador-barras" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">📊 Gerador de Código de Barras</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Escolha o tipo, digite o código e gere a imagem na hora.</p>
<label for="cb-tipo" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Tipo</label>
<select id="cb-tipo" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<option value="codabar">Codabar</option>
<option value="code11">Code 11</option>
<option value="code39">Code 39</option>
<option value="code39ext">Code 39 Extended</option>
<option value="code93">Code 93</option>
<option value="code128" selected>Code 128</option>
<option value="ean8">EAN-8</option>
<option value="ean13">EAN-13</option>
<option value="gs1128">GS1-128 (EAN-128)</option>
<option value="itf">Interleaved 2 of 5</option>
<option value="isbn">ISBN-10 / ISBN-13</option>
<option value="msi">MSI Plessey</option>
<option value="postnet">PostNet</option>
<option value="std25">Standard 2 of 5</option>
<option value="upca">UPC-A</option>
<option value="upce">UPC-E</option>
<option value="upcext2">UPC Extension 2 Digits</option>
<option value="upcext5">UPC Extension 5 Digits</option>
</select>
<div style="display:flex;gap:12px;flex-wrap:wrap;">
<div style="flex:1;min-width:140px;">
<label for="cb-tamanho" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Tamanho</label>
<select id="cb-tamanho" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<option value="1">1</option>
<option value="2" selected>2</option>
<option value="3">3</option>
<option value="4">4</option>
<option value="5">5</option>
<option value="6">6</option>
<option value="7">7</option>
<option value="8">8</option>
<option value="9">9</option>
</select>
</div>
<div style="flex:1;min-width:140px;">
<label for="cb-rotacao" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Rotação</label>
<select id="cb-rotacao" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<option value="0">0°</option>
<option value="90">90°</option>
<option value="180">180°</option>
<option value="270">270°</option>
</select>
</div>
</div>
<div style="display:flex;gap:12px;flex-wrap:wrap;">
<div style="flex:1;min-width:140px;">
<label for="cb-fonte" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Fonte</label>
<select id="cb-fonte" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<option value="arial">Arial</option>
<option value="nenhuma">Sem Texto</option>
</select>
</div>
<div style="flex:1;min-width:140px;">
<label for="cb-altura" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Altura (px)</label>
<input id="cb-altura" type="text" inputmode="numeric" value="60" placeholder="Ex.: 60" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
</div>
</div>
<label for="cb-codigo" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Código</label>
<input id="cb-codigo" type="text" placeholder="Ex.: Código 128" autocomplete="off" spellcheck="false" style="width:100%;padding:12px 14px;margin-bottom:6px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<p id="cb-dica" style="margin:0 0 20px;font-size:0.82rem;color:#64748b;">Qualquer caractere ASCII imprimível (sem acentos).</p>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="cb-gerar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Gerar Imagem</button>
<button type="button" id="cb-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="cb-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resultado:</strong> <span id="cb-resultado">preencha os campos e clique em "Gerar Imagem".</span></div>
</div>
<script>
(function () {
  var tipo = document.getElementById('cb-tipo');
  var tamanho = document.getElementById('cb-tamanho');
  var rotacao = document.getElementById('cb-rotacao');
  var fonte = document.getElementById('cb-fonte');
  var altura = document.getElementById('cb-altura');
  var codigo = document.getElementById('cb-codigo');
  var dica = document.getElementById('cb-dica');
  var resultado = document.getElementById('cb-resultado');
  var caixa = document.getElementById('cb-resposta');
  var DICAS = {
    codabar: ['A40156B', 'números e os símbolos - $ : / . + (início e fim opcionais: A, B, C ou D).'],
    code11: ['123-45', 'números e hífen. Os dígitos verificadores são adicionados automaticamente.'],
    code39: ['CODE39', 'letras maiúsculas, números, espaço e os símbolos - . $ / + %.'],
    code39ext: ['Code 39 Ext', 'todos os caracteres ASCII, inclusive letras minúsculas e símbolos.'],
    code93: ['CODE93', 'letras maiúsculas, números, espaço e os símbolos - . $ / + %. Os dígitos verificadores são adicionados automaticamente.'],
    code128: ['Código 128', 'qualquer caractere ASCII imprimível (sem acentos).'],
    ean8: ['9638507', '7 ou 8 dígitos. O dígito verificador é calculado automaticamente.'],
    ean13: ['789123456789', '12 ou 13 dígitos. O dígito verificador é calculado automaticamente.'],
    gs1128: ['(01)12345678901231(17)251231', 'use o formato (IA)dados, por exemplo (01)GTIN(17)validade.'],
    itf: ['12345670', 'somente números, em quantidade par (se for ímpar, um zero é adicionado à esquerda).'],
    isbn: ['978-85-359-0277-8', 'ISBN-10 ou ISBN-13, com ou sem hífens.'],
    msi: ['1234567', 'somente números. O dígito verificador (módulo 10) é adicionado automaticamente.'],
    postnet: ['12345', 'CEP americano (ZIP) com 5, 9 ou 11 dígitos. O dígito verificador é adicionado automaticamente.'],
    std25: ['1234567890', 'somente números.'],
    upca: ['03600029145', '11 ou 12 dígitos. O dígito verificador é calculado automaticamente.'],
    upce: ['0123456', '6, 7 ou 8 dígitos. O sistema numérico (primeiro dígito) deve ser 0 ou 1.'],
    upcext2: ['12', 'exatamente 2 dígitos.'],
    upcext5: ['52495', 'exatamente 5 dígitos.']
  };
  var NUM = ['ean8', 'ean13', 'upca', 'upce', 'upcext2', 'upcext5', 'itf', 'msi', 'std25', 'postnet'];
  function inr(c, a, b) { return c > a - 1 ? b + 1 > c : false; }
  function W(s) {
    var o = '', bar = true, i;
    for (i = 0; i !== s.length; i++) { o += (bar ? '1' : '0').repeat(Number(s.charAt(i))); bar = !bar; }
    return o;
  }
  function nw(p) { return p.replace(/n/g, '1').replace(/w/g, '3'); }
  function dig(s) { if (!/^[0-9]+$/.test(s)) { throw new Error('use apenas números (0 a 9).'); } }
  function chk(d) {
    var s = 0, i, n = d.length;
    for (i = 0; i !== n; i++) { s += Number(d.charAt(n - 1 - i)) * (i % 2 === 0 ? 3 : 1); }
    return (10 - s % 10) % 10;
  }
  function fixchk(s, n, nome) {
    if (s.length === n) { return s + chk(s); }
    if (s.length === n + 1) {
      if (Number(s.charAt(n)) !== chk(s.slice(0, n))) { throw new Error('dígito verificador inválido. O correto é ' + chk(s.slice(0, n)) + '.'); }
      return s;
    }
    throw new Error('o ' + nome + ' precisa de ' + n + ' ou ' + (n + 1) + ' dígitos.');
  }
  function modck(a, max, mod) {
    var sum = 0, j;
    for (j = 0; j !== a.length; j++) { sum += a[j] * ((a.length - 1 - j) % max + 1); }
    return sum % mod;
  }
  var L = ['0001101', '0011001', '0010011', '0111101', '0100011', '0110001', '0101111', '0111011', '0110111', '0001011'];
  function R(d) { return L[d].replace(/[01]/g, function (c) { return c === '1' ? '0' : '1'; }); }
  function G(d) { return R(d).split('').reverse().join(''); }
  function enc(set, d) { d = Number(d); return set === 'L' ? L[d] : (set === 'G' ? G(d) : R(d)); }
  var PAR = ['LLLLLL', 'LLGLGG', 'LLGGLG', 'LLGGGL', 'LGLLGG', 'LGGLLG', 'LGGGLL', 'LGLGLG', 'LGLGGL', 'LGGLGL'];
  function ean13(s) {
    dig(s);
    s = fixchk(s, 12, 'EAN-13');
    var par = PAR[Number(s.charAt(0))], m = '101', i;
    for (i = 1; i !== 7; i++) { m += enc(par.charAt(i - 1), s.charAt(i)); }
    m += '01010';
    for (i = 7; i !== 13; i++) { m += enc('R', s.charAt(i)); }
    return { mods: m + '101', text: s.charAt(0) + ' ' + s.slice(1, 7) + ' ' + s.slice(7) };
  }
  function ean8(s) {
    dig(s);
    s = fixchk(s, 7, 'EAN-8');
    var m = '101', i;
    for (i = 0; i !== 4; i++) { m += enc('L', s.charAt(i)); }
    m += '01010';
    for (i = 4; i !== 8; i++) { m += enc('R', s.charAt(i)); }
    return { mods: m + '101', text: s.slice(0, 4) + ' ' + s.slice(4) };
  }
  function upca(s) {
    dig(s);
    s = fixchk(s, 11, 'UPC-A');
    return { mods: ean13('0' + s).mods, text: s.charAt(0) + ' ' + s.slice(1, 6) + ' ' + s.slice(6, 11) + ' ' + s.charAt(11) };
  }
  function isbn(s) {
    s = s.replace(/[\s-]/g, '');
    var t, f;
    if (s.length === 9 || s.length === 10) {
      if (!/^[0-9]+$/.test(s.slice(0, 9))) { throw new Error('ISBN-10 inválido.'); }
      t = '978' + s.slice(0, 9);
    } else if (s.length === 12 || s.length === 13) {
      dig(s);
      f = s.slice(0, 3);
      if (f !== '978') { if (f !== '979') { throw new Error('o ISBN-13 deve começar com 978 ou 979.'); } }
      t = s;
    } else {
      throw new Error('informe um ISBN-10 ou um ISBN-13.');
    }
    return ean13(t);
  }
  function upce(s) {
    dig(s);
    var ns, d, x, last, a, c, pe, m = '101', i;
    if (s.length === 6) { ns = 0; d = s; }
    else if (s.length === 7 || s.length === 8) { ns = Number(s.charAt(0)); d = s.slice(1, 7); }
    else { throw new Error('o UPC-E precisa de 6, 7 ou 8 dígitos.'); }
    if (ns !== 0) { if (ns !== 1) { throw new Error('o primeiro dígito do UPC-E deve ser 0 ou 1.'); } }
    x = d.split('');
    last = Number(x[5]);
    if (last === 0 || last === 1 || last === 2) { a = x[0] + x[1] + x[5] + '0000' + x[2] + x[3] + x[4]; }
    else if (last === 3) { a = x[0] + x[1] + x[2] + '00000' + x[3] + x[4]; }
    else if (last === 4) { a = x[0] + x[1] + x[2] + x[3] + '00000' + x[4]; }
    else { a = x[0] + x[1] + x[2] + x[3] + x[4] + '0000' + x[5]; }
    c = chk(String(ns) + a);
    if (s.length === 8) {
      if (Number(s.charAt(7)) !== c) { throw new Error('dígito verificador inválido. O correto é ' + c + '.'); }
    }
    pe = ['EEEOOO', 'EEOEOO', 'EEOOEO', 'EEOOOE', 'EOEEOO', 'EOOEEO', 'EOOOEE', 'EOEOEO', 'EOEOOE', 'EOOEOE'][c];
    if (ns === 1) { pe = pe.replace(/[EO]/g, function (z) { return z === 'E' ? 'O' : 'E'; }); }
    for (i = 0; i !== 6; i++) { m += enc(pe.charAt(i) === 'O' ? 'L' : 'G', d.charAt(i)); }
    return { mods: m + '010101', text: ns + ' ' + d + ' ' + c };
  }
  function ext(s, n) {
    if (!/^[0-9]+$/.test(s)) { throw new Error('use apenas números (0 a 9).'); }
    if (s.length !== n) { throw new Error('informe exatamente ' + n + ' dígitos.'); }
    var par, c, m = '1011', i;
    if (n === 2) { par = ['LL', 'LG', 'GL', 'GG'][Number(s) % 4]; }
    else {
      c = (3 * (Number(s.charAt(0)) + Number(s.charAt(2)) + Number(s.charAt(4))) + 9 * (Number(s.charAt(1)) + Number(s.charAt(3)))) % 10;
      par = ['GGLLL', 'GLGLL', 'GLLGL', 'GLLLG', 'LGGLL', 'LLGGL', 'LLLGG', 'LGLGL', 'LGLLG', 'LLGLG'][c];
    }
    for (i = 0; i !== n; i++) {
      if (i !== 0) { m += '01'; }
      m += enc(par.charAt(i), s.charAt(i));
    }
    return { mods: m, text: s };
  }
  var P128 = '212222 222122 222221 121223 121322 131222 122213 122312 132212 221213 221312 231212 112232 122132 122231 113222 123122 123221 223211 221132 221231 213212 223112 312131 311222 321122 321221 312212 322112 322211 212123 212321 232121 111323 131123 131321 112313 132113 132311 211313 231113 231311 112133 112331 132131 113123 113321 133121 313121 211331 231131 213113 213311 213131 311123 311321 331121 312113 312311 332111 314111 221411 431111 111224 111422 121124 121421 141122 141221 112214 112412 122114 122411 142112 142211 241211 221114 413111 241112 134111 111242 121142 121241 114212 124112 124211 411212 421112 421211 212141 214121 412121 111143 111341 131141 114113 114311 411113 411311 113141 114131 311141 411131 211412 211214 211232 2331112'.split(' ');
  function c128(items) {
    var vals = [], i = 0, p0 = 0, set, run, sum, k;
    function digits(p) {
      var n = 0;
      while (p + n !== items.length ? /^[0-9]$/.test(items[p + n]) : false) { n++; }
      return n;
    }
    while (p0 !== items.length ? items[p0] === 'F1' : false) { p0++; }
    set = digits(p0) > 1 ? 'C' : 'B';
    vals.push(set === 'C' ? 105 : 104);
    while (i !== items.length) {
      if (items[i] === 'F1') { vals.push(102); i++; continue; }
      run = digits(i);
      if (set === 'C') {
        if (run > 1) { vals.push(Number(items[i] + items[i + 1])); i += 2; }
        else { vals.push(100); set = 'B'; }
      } else {
        if (run > 3) { vals.push(99); set = 'C'; }
        else { vals.push(items[i].charCodeAt(0) - 32); i++; }
      }
    }
    sum = vals[0];
    for (k = 1; k !== vals.length; k++) { sum += vals[k] * k; }
    vals.push(sum % 103);
    vals.push(106);
    return vals.map(function (v) { return W(P128[v]); }).join('');
  }
  function code128(s) {
    if (!/^[\x20-\x7e]+$/.test(s)) { throw new Error('use apenas caracteres ASCII imprimíveis (sem acentos).'); }
    return { mods: c128(s.split('')), text: s };
  }
  function gs1(s) {
    var items = ['F1'], parts, k, p, ix, ai, data, fixos = ['00', '01', '02', '11', '12', '13', '14', '15', '16', '17', '18', '19', '20', '31', '32', '33', '34', '35', '36', '41'], last;
    if (!/^[\x20-\x7e]+$/.test(s)) { throw new Error('use apenas caracteres ASCII imprimíveis (sem acentos).'); }
    if (s.indexOf('(') === -1) { return { mods: c128(items.concat(s.split(''))), text: s }; }
    parts = s.split('(');
    last = parts.length - 1;
    for (k = 1; k !== parts.length; k++) {
      p = parts[k];
      ix = p.indexOf(')');
      ai = p.slice(0, ix);
      data = p.slice(ix + 1);
      if (!/^[0-9]+$/.test(ai) || ai.length === 1 || ai.length > 4 || data === '') { throw new Error('use o formato (IA)dados, por exemplo (01)12345678901231.'); }
      items = items.concat((ai + data).split(''));
      if (k !== last) { if (fixos.indexOf(ai.slice(0, 2)) === -1) { items.push('F1'); } }
    }
    return { mods: c128(items), text: s };
  }
  var C39 = '0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ-. *$/+%';
  var P39 = 'nnnwwnwnn wnnwnnnnw nnwwnnnnw wnwwnnnnn nnnwwnnnw wnnwwnnnn nnwwwnnnn nnnwnnwnw wnnwnnwnn nnwwnnwnn wnnnnwnnw nnwnnwnnw wnwnnwnnn nnnnwwnnw wnnnwwnnn nnwnwwnnn nnnnnwwnw wnnnnwwnn nnwnnwwnn nnnnwwwnn wnnnnnnww nnwnnnnww wnwnnnnwn nnnnwnnww wnnnwnnwn nnwnwnnwn nnnnnnwww wnnnnnwwn nnwnnnwwn nnnnwnwwn wwnnnnnnw nwwnnnnnw wwwnnnnnn nwnnwnnnw wwnnwnnnn nwwnwnnnn nwnnnnwnw wwnnnnwnn nwwnnnwnn nwnnwnwnn nwnwnwnnn nwnwnnnwn nwnnnwnwn nnnwnwnwn'.split(' ');
  function ext39(s) {
    var o = '', i, c, h;
    for (i = 0; i !== s.length; i++) {
      c = s.charCodeAt(i);
      h = s.charAt(i);
      if (c === 0) { o += '%U'; }
      else if (27 > c) { o += '$' + String.fromCharCode(64 + c); }
      else if (32 > c) { o += '%' + String.fromCharCode(38 + c); }
      else if (c === 32 || c === 45 || c === 46 || inr(c, 48, 57) || inr(c, 65, 90)) { o += h; }
      else if (48 > c) { o += '/' + String.fromCharCode(32 + c); }
      else if (c === 58) { o += '/Z'; }
      else if (64 > c) { o += '%' + String.fromCharCode(11 + c); }
      else if (c === 64) { o += '%V'; }
      else if (96 > c) { o += '%' + String.fromCharCode(c - 16); }
      else if (c === 96) { o += '%W'; }
      else if (123 > c) { o += '+' + String.fromCharCode(c - 32); }
      else { o += '%' + String.fromCharCode(c - 43); }
    }
    return o;
  }
  function code39(s, estendido) {
    var t, full, i, k, parts = [];
    if (estendido) {
      if (!/^[\x00-\x7f]+$/.test(s)) { throw new Error('use apenas caracteres ASCII (sem acentos).'); }
      t = ext39(s);
    } else {
      t = s.toUpperCase();
      for (i = 0; i !== t.length; i++) {
        k = C39.indexOf(t.charAt(i));
        if (k === -1 || t.charAt(i) === '*') { throw new Error('caractere inválido para Code 39: ' + t.charAt(i) + '.'); }
      }
    }
    full = '*' + t + '*';
    for (i = 0; i !== full.length; i++) { parts.push(W(nw(P39[C39.indexOf(full.charAt(i))]))); }
    return { mods: parts.join('0'), text: s };
  }
  var C93 = '0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ-. $/+%';
  var P93 = '100010100 101001000 101000100 101000010 100101000 100100100 100100010 101010000 100010010 100001010 110101000 110100100 110100010 110010100 110010010 110001010 101101000 101100100 101100010 100110100 100011010 101011000 101001100 101000110 100101100 100010110 110110100 110110010 110101100 110100110 110010110 110011010 101101100 101100110 100110110 100111010 100101110 111010100 111010010 111001010 101101110 101110110 110101110 100100110 111011010 111010110 100110010'.split(' ');
  function code93(s) {
    var t = s.toUpperCase(), v = [], i, k, m = '101011110';
    for (i = 0; i !== t.length; i++) {
      k = C93.indexOf(t.charAt(i));
      if (k === -1) { throw new Error('caractere inválido para Code 93: ' + t.charAt(i) + '.'); }
      v.push(k);
    }
    v.push(modck(v, 20, 47));
    v.push(modck(v, 15, 47));
    for (i = 0; i !== v.length; i++) { m += P93[v[i]]; }
    return { mods: m + '1010111101', text: t };
  }
  var CB = '0123456789-$:/.+ABCD';
  var PCB = 'nnnnnww nnnnwwn nnnwnnw wwnnnnn nnwnnwn wnnnnwn nwnnnnw nwnnwnn nwwnnnn wnnwnnn nnnwwnn nnwwnnn wnnnwnw wnwnnnw wnwnwnn nnwnwnw nnwwnwn nwnwnnw nnnwnww nnnwwwn'.split(' ');
  function codabar(s) {
    var t = s.toUpperCase(), i, k, parts = [];
    if (!/^[A-D].*[A-D]$/.test(t)) { t = 'A' + t + 'A'; }
    for (i = 0; i !== t.length; i++) {
      k = CB.indexOf(t.charAt(i));
      if (k === -1) { throw new Error('caractere inválido para Codabar: ' + t.charAt(i) + '.'); }
      if (k > 15) { if (i !== 0) { if (i !== t.length - 1) { throw new Error('as letras A, B, C e D só podem ser usadas no início e no fim.'); } } }
      parts.push(W(nw(PCB[k])));
    }
    return { mods: parts.join('0'), text: t };
  }
  var P11 = 'nnnnw wnnnw nwnnw wwnnn nnwnw wnwnn nwwnn nnnww wnnwn wnnnn nnwnn'.split(' ');
  function code11(s) {
    if (!/^[0-9-]+$/.test(s)) { throw new Error('use apenas números e hífen.'); }
    var v = [], i, parts = [], txt = s;
    for (i = 0; i !== s.length; i++) { v.push(s.charAt(i) === '-' ? 10 : Number(s.charAt(i))); }
    v.push(modck(v, 10, 11));
    if (s.length > 9) { v.push(modck(v, 9, 11)); }
    parts.push(W(nw('nnwwn')));
    for (i = 0; i !== v.length; i++) { parts.push(W(nw(P11[v[i]]))); }
    parts.push(W(nw('nnwwn')));
    for (i = s.length; i !== v.length; i++) { txt += (v[i] === 10 ? '-' : String(v[i])); }
    return { mods: parts.join('0'), text: txt };
  }
  var P25 = 'nnwwn wnnnw nwnnw wwnnn nnwnw wnwnn nwwnn nnnww wnnwn nwnwn'.split(' ');
  function itf(s) {
    dig(s);
    if (s.length % 2 === 1) { s = '0' + s; }
    var m = '1010', i, k, a, b;
    for (i = 0; i !== s.length; i += 2) {
      a = P25[Number(s.charAt(i))];
      b = P25[Number(s.charAt(i + 1))];
      for (k = 0; k !== 5; k++) {
        m += '1'.repeat(a.charAt(k) === 'w' ? 3 : 1);
        m += '0'.repeat(b.charAt(k) === 'w' ? 3 : 1);
      }
    }
    return { mods: m + '11101', text: s };
  }
  function std25(s) {
    dig(s);
    var m = W('313111'), i, k, a;
    for (i = 0; i !== s.length; i++) {
      a = P25[Number(s.charAt(i))];
      for (k = 0; k !== 5; k++) { m += '1'.repeat(a.charAt(k) === 'w' ? 3 : 1) + '0'; }
    }
    return { mods: m + W('31113'), text: s };
  }
  function msi(s) {
    dig(s);
    var n = s.length, odd = '', even = 0, i, v, carry = 0, d = '', sum, c, full, m = '110', bits, k;
    for (i = 0; i !== n; i++) {
      if (i % 2 === 0) { odd = s.charAt(n - 1 - i) + odd; }
      else { even += Number(s.charAt(n - 1 - i)); }
    }
    for (i = odd.length - 1; i !== -1; i--) {
      v = Number(odd.charAt(i)) * 2 + carry;
      d = (v % 10) + d;
      carry = v > 9 ? 1 : 0;
    }
    if (carry === 1) { d = '1' + d; }
    sum = even;
    for (i = 0; i !== d.length; i++) { sum += Number(d.charAt(i)); }
    c = (10 - sum % 10) % 10;
    full = s + c;
    for (i = 0; i !== full.length; i++) {
      bits = ('000' + Number(full.charAt(i)).toString(2)).slice(-4);
      for (k = 0; k !== 4; k++) { m += bits.charAt(k) === '1' ? '110' : '100'; }
    }
    return { mods: m + '1001', text: full };
  }
  var PN = ['11000', '00011', '00101', '00110', '01001', '01010', '01100', '10001', '10010', '10100'];
  function postnet(s) {
    s = s.replace(/-/g, '');
    dig(s);
    if ([5, 9, 11].indexOf(s.length) === -1) { throw new Error('o PostNet precisa de 5, 9 ou 11 dígitos.'); }
    var sum = 0, i, k, full, bars = [1], p;
    for (i = 0; i !== s.length; i++) { sum += Number(s.charAt(i)); }
    full = s + ((10 - sum % 10) % 10);
    for (i = 0; i !== full.length; i++) {
      p = PN[Number(full.charAt(i))];
      for (k = 0; k !== 5; k++) { bars.push(Number(p.charAt(k))); }
    }
    bars.push(1);
    return { post: bars, text: full };
  }
  function encode(t, s) {
    if (NUM.indexOf(t) !== -1) { s = s.replace(/\s/g, ''); }
    switch (t) {
      case 'codabar': return codabar(s);
      case 'code11': return code11(s);
      case 'code39': return code39(s, false);
      case 'code39ext': return code39(s, true);
      case 'code93': return code93(s);
      case 'code128': return code128(s);
      case 'ean8': return ean8(s);
      case 'ean13': return ean13(s);
      case 'gs1128': return gs1(s);
      case 'itf': return itf(s);
      case 'isbn': return isbn(s);
      case 'msi': return msi(s);
      case 'postnet': return postnet(s);
      case 'std25': return std25(s);
      case 'upca': return upca(s);
      case 'upce': return upce(s);
      case 'upcext2': return ext(s, 2);
      case 'upcext5': return ext(s, 5);
    }
    throw new Error('tipo de código não suportado.');
  }
  function desenhar(r, esc, alt, texto, rot) {
    var q = 10 * esc, pad = 10, fs = 10 + esc * 3, c = document.createElement('canvas'), ctx = c.getContext('2d');
    var n, bw, w, h, x0, i, j, m, tw = 0, curto, rc, rcv;
    if (r.post) { n = r.post.length; bw = (n * 5 - 3) * esc; }
    else { n = r.mods.length; bw = n * esc; }
    if (texto) { ctx.font = fs + 'px Arial'; tw = Math.ceil(ctx.measureText(r.text).width) + 20; }
    w = Math.max(bw + 2 * q, tw);
    h = pad + alt + (texto ? fs + 8 : 0) + pad;
    c.width = w;
    c.height = h;
    ctx.fillStyle = '#ffffff';
    ctx.fillRect(0, 0, w, h);
    ctx.fillStyle = '#000000';
    x0 = Math.floor((w - bw) / 2);
    if (r.post) {
      curto = Math.round(alt * 0.4);
      for (i = 0; i !== n; i++) {
        j = r.post[i] === 1 ? alt : curto;
        ctx.fillRect(x0 + i * 5 * esc, pad + alt - j, 2 * esc, j);
      }
    } else {
      m = r.mods;
      i = 0;
      while (i !== n) {
        if (m.charAt(i) === '1') {
          j = i;
          while (j !== n ? m.charAt(j) === '1' : false) { j++; }
          ctx.fillRect(x0 + i * esc, pad, (j - i) * esc, alt);
          i = j;
        } else { i++; }
      }
    }
    if (texto) {
      ctx.font = fs + 'px Arial';
      ctx.textAlign = 'center';
      ctx.textBaseline = 'top';
      ctx.fillText(r.text, w / 2, pad + alt + 4);
    }
    rcv = document.createElement('canvas');
    if (rot === 90 || rot === 270) { rcv.width = h; rcv.height = w; }
    else { rcv.width = w; rcv.height = h; }
    rc = rcv.getContext('2d');
    rc.fillStyle = '#ffffff';
    rc.fillRect(0, 0, rcv.width, rcv.height);
    rc.translate(rcv.width / 2, rcv.height / 2);
    rc.rotate(rot * Math.PI / 180);
    rc.drawImage(c, -w / 2, -h / 2);
    return rcv;
  }
  function estilo(ok) {
    caixa.style.borderColor = ok ? '#86efac' : '#fca5a5';
    caixa.style.background = ok ? '#f0fdf4' : '#fef2f2';
    resultado.style.color = ok ? '#166534' : '#b91c1c';
    resultado.style.display = ok ? 'block' : '';
    resultado.style.marginTop = ok ? '12px' : '';
    resultado.style.textAlign = ok ? 'center' : '';
  }
  function erro(msg) {
    estilo(false);
    resultado.textContent = msg;
  }
  function gerar() {
    var t = tipo.value, s = codigo.value.trim(), h = Number(altura.value.replace(',', '.')), r, c, img, a;
    if (s === '') { erro('digite o código que deseja gerar.'); return; }
    if (isNaN(h) || !(h > 9) || h > 500) { erro('a altura deve ser um número entre 10 e 500.'); return; }
    try {
      r = encode(t, s);
      c = desenhar(r, Number(tamanho.value), Math.round(h), fonte.value === 'arial', Number(rotacao.value));
    } catch (e) {
      erro(e.message || 'não foi possível gerar o código.');
      return;
    }
    estilo(true);
    resultado.textContent = '';
    img = document.createElement('img');
    img.src = c.toDataURL('image/png');
    img.alt = 'Código de barras: ' + r.text;
    img.setAttribute('style', 'display:block;margin:0 auto;max-width:100%;height:auto;background:#ffffff;border:1px solid #e2e8f0;border-radius:6px;');
    a = document.createElement('a');
    a.href = img.src;
    a.download = 'codigo-de-barras.png';
    a.textContent = 'Baixar imagem (PNG)';
    a.setAttribute('style', 'display:inline-block;margin-top:12px;padding:8px 14px;font-size:0.9rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;text-decoration:none;');
    resultado.appendChild(img);
    resultado.appendChild(a);
  }
  function atualizarDica() {
    var d = DICAS[tipo.value];
    codigo.placeholder = 'Ex.: ' + d[0];
    dica.textContent = 'Formato: ' + d[1];
  }
  function limpar() {
    codigo.value = '';
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    resultado.style.color = '#64748b';
    resultado.style.display = '';
    resultado.style.marginTop = '';
    resultado.style.textAlign = '';
    resultado.textContent = 'preencha os campos e clique em "Gerar Imagem".';
    codigo.focus();
  }
  document.getElementById('cb-gerar').addEventListener('click', gerar);
  document.getElementById('cb-limpar').addEventListener('click', limpar);
  tipo.addEventListener('change', atualizarDica);
  [tipo, tamanho, rotacao, fonte, altura, codigo].forEach(function (el) {
    el.addEventListener('focus', function () { el.style.borderColor = '#6366f1'; });
    el.addEventListener('blur', function () { el.style.borderColor = '#c7d2fe'; });
  });
  [codigo, altura].forEach(function (el) {
    el.addEventListener('keydown', function (e) { if (e.key === 'Enter') { gerar(); } });
  });
  atualizarDica();
})();
</script>

## Como usar o gerador

1. Escolha o **Tipo** de código de barras na lista (por exemplo, EAN-13, Code 128 ou UPC-A).
2. Defina o **Tamanho** de 1 a 9. Quanto maior o número, mais larga é cada barra e maior fica a imagem.
3. Se precisar, escolha a **Rotação** (0°, 90°, 180° ou 270°), a **Fonte** do texto (Arial ou Sem Texto) e a **Altura** das barras em pixels.
4. Digite o **Código** no campo. Logo abaixo dele, uma dica mostra o formato aceito pelo tipo escolhido.
5. Clique em **Gerar Imagem** (ou pressione Enter) para ver o resultado.
6. Clique em **Baixar imagem (PNG)** para salvar o código de barras.
7. Use o botão **Limpar** para apagar o código e fazer uma nova geração.

Cada tipo aceita caracteres diferentes. Nos formatos com dígito verificador (como EAN-13, EAN-8 e UPC-A), você pode informar o código sem esse dígito, que ele é calculado automaticamente. Se você informar o dígito, ele é conferido e, se estiver errado, a ferramenta mostra qual é o correto. A imagem é criada no seu próprio navegador, sem enviar o código para nenhum servidor.

## Entendendo os termos

- **Código de barras:** representação de dados em barras e espaços de larguras diferentes, que pode ser lida por um leitor óptico.
- **Tipo:** padrão (simbologia) usado para codificar os dados. Cada tipo tem regras próprias de caracteres e tamanho.
- **Tamanho:** largura de cada módulo (a menor barra) em pixels. Valores de 1 a 9.
- **Rotação:** ângulo em que a imagem final é girada: 0°, 90°, 180° ou 270°.
- **Fonte:** estilo do texto exibido abaixo das barras. **Arial** mostra o código escrito e **Sem Texto** gera apenas as barras.
- **Altura:** comprimento vertical das barras, em pixels.
- **Código:** conteúdo (números, letras ou símbolos) que será representado nas barras.
- **Dígito verificador:** dígito extra calculado a partir dos demais, usado pelo leitor para confirmar que a leitura está correta.
- **Zona de silêncio:** margem em branco nas laterais das barras, necessária para o leitor identificar o início e o fim do código.
- **Codabar:** formato numérico com os símbolos `- $ : / . +`, usado em bibliotecas, bancos de sangue e transportadoras. Começa e termina com A, B, C ou D.
- **Code 11:** formato numérico (0 a 9 e hífen), usado principalmente em telecomunicações.
- **Code 39:** formato alfanumérico (letras maiúsculas, números e alguns símbolos), muito usado na indústria e em identificações.
- **Code 39 Extended:** versão do Code 39 que representa todos os caracteres ASCII, incluindo letras minúsculas.
- **Code 93:** formato alfanumérico mais compacto que o Code 39, com dois dígitos verificadores.
- **Code 128:** formato de alta densidade que codifica todos os caracteres ASCII, muito usado em logística e remessas.
- **EAN-8:** versão curta do EAN, com 8 dígitos, para produtos pequenos.
- **EAN-13:** padrão internacional de produtos no varejo, com 13 dígitos (no Brasil, começa com 789 ou 790).
- **GS1-128 (EAN-128):** variação do Code 128 que usa Identificadores de Aplicação (IA), como GTIN, validade e lote, escritos entre parênteses.
- **Interleaved 2 of 5:** formato numérico que codifica pares de dígitos, usado em caixas de papelão e logística.
- **ISBN-10 / ISBN-13:** código internacional de livros. A ferramenta gera a barra a partir do ISBN, no padrão EAN-13 (prefixo 978 ou 979).
- **MSI Plessey:** formato numérico usado em inventário e controle de estoque.
- **PostNet:** formato de barras altas e baixas usado pelo correio dos Estados Unidos para o CEP (ZIP).
- **Standard 2 of 5:** formato numérico simples, também chamado de Industrial 2 of 5.
- **UPC-A:** padrão de produtos dos Estados Unidos e Canadá, com 12 dígitos.
- **UPC-E:** versão compacta do UPC-A, com 8 dígitos, para embalagens pequenas.
- **UPC Extension 2 Digits:** código complementar de 2 dígitos que acompanha o UPC/EAN, usado em revistas e periódicos (número da edição).
- **UPC Extension 5 Digits:** código complementar de 5 dígitos que acompanha o UPC/EAN, usado em livros (indicação de preço).