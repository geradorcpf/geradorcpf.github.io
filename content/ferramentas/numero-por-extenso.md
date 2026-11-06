---
title: "Número por Extenso"
seoTitle: "Número por Extenso"
description: "Número por Extenso: escreva qualquer número por extenso, inclusive valores em reais. Grátis e online, sem cadastro."
summary: "Escreva qualquer número por extenso, inclusive valores em reais."
date: 2026-11-06
draft: false
category: "texto"
tags: ["número por extenso", "escrita", "finanças", "texto"]
keywords: ["número por extenso", "número por extenso online", "escrita", "finanças"]
---

Basta escolher a unidade e o tipo de letra, digitar o valor abaixo e depois clicar em **Escrever por Extenso**.

<div id="calc-extenso" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🔢 Número por Extenso</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Digite um número ou valor em reais e veja o resultado na hora.</p>
<div style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">1. Qual a unidade?</div>
<div style="display:flex;gap:16px;flex-wrap:wrap;margin-bottom:16px;">
<label for="ext-un-moeda" style="display:flex;align-items:center;gap:6px;font-size:0.95rem;cursor:pointer;"><input type="radio" name="ext-unidade" id="ext-un-moeda" value="moeda" checked style="accent-color:#4f46e5;margin:0;">Monetária (Reais)</label>
<label for="ext-un-numero" style="display:flex;align-items:center;gap:6px;font-size:0.95rem;cursor:pointer;"><input type="radio" name="ext-unidade" id="ext-un-numero" value="numero" style="accent-color:#4f46e5;margin:0;">Numérica (Número Simples)</label>
</div>
<div style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">2. Tipo de letra?</div>
<div style="display:flex;gap:16px;flex-wrap:wrap;margin-bottom:16px;">
<label for="ext-ca-min" style="display:flex;align-items:center;gap:6px;font-size:0.95rem;cursor:pointer;"><input type="radio" name="ext-caso" id="ext-ca-min" value="min" checked style="accent-color:#4f46e5;margin:0;">minúsculas</label>
<label for="ext-ca-mai" style="display:flex;align-items:center;gap:6px;font-size:0.95rem;cursor:pointer;"><input type="radio" name="ext-caso" id="ext-ca-mai" value="mai" style="accent-color:#4f46e5;margin:0;">MAIÚSCULAS</label>
<label for="ext-ca-pri" style="display:flex;align-items:center;gap:6px;font-size:0.95rem;cursor:pointer;"><input type="radio" name="ext-caso" id="ext-ca-pri" value="pri" style="accent-color:#4f46e5;margin:0;">Primeira Maiúscula</label>
</div>
<label for="ext-valor" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">3. Digite o valor</label>
<input id="ext-valor" type="text" inputmode="decimal" placeholder="Ex.: 1234,56" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:20px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="ext-converter" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Escrever por Extenso</button>
<button type="button" id="ext-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="ext-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;word-wrap:break-word;overflow-wrap:anywhere;"><strong style="color:#3730a3;">Resposta por extenso:</strong> <span id="ext-resultado">preencha o valor e clique em "Escrever por Extenso".</span></div>
</div>
<script>
(function () {
  var campo = document.getElementById('ext-valor');
  var resultado = document.getElementById('ext-resultado');
  var caixa = document.getElementById('ext-resposta');
  var TEXTO_INICIAL = 'preencha o valor e clique em "Escrever por Extenso".';
  var UN = ['zero', 'um', 'dois', 'três', 'quatro', 'cinco', 'seis', 'sete', 'oito', 'nove', 'dez', 'onze', 'doze', 'treze', 'catorze', 'quinze', 'dezesseis', 'dezessete', 'dezoito', 'dezenove'];
  var DZ = ['', '', 'vinte', 'trinta', 'quarenta', 'cinquenta', 'sessenta', 'setenta', 'oitenta', 'noventa'];
  var CT = ['', 'cento', 'duzentos', 'trezentos', 'quatrocentos', 'quinhentos', 'seiscentos', 'setecentos', 'oitocentos', 'novecentos'];
  var ESC_S = ['', 'mil', 'milhão', 'bilhão', 'trilhão', 'quatrilhão', 'quintilhão', 'sextilhão', 'setilhão', 'octilhão', 'nonilhão'];
  var ESC_P = ['', 'mil', 'milhões', 'bilhões', 'trilhões', 'quatrilhões', 'quintilhões', 'sextilhões', 'setilhões', 'octilhões', 'nonilhões'];
  var FRAC_S = ['', 'décimo', 'centésimo', 'milésimo', 'décimo de milésimo', 'centésimo de milésimo', 'milionésimo'];
  var FRAC_P = ['', 'décimos', 'centésimos', 'milésimos', 'décimos de milésimo', 'centésimos de milésimo', 'milionésimos'];
  var MAX_DIGITOS = 30;
  var MAX_DECIMAIS = 6;
  function selecionado(nome) {
    var lista = document.getElementsByName(nome);
    for (var i = 0; lista.length > i; i++) {
      if (lista[i].checked) { return lista[i].value; }
    }
    return '';
  }
  function grupo(n) {
    if (n === 100) { return 'cem'; }
    var c = Math.floor(n / 100);
    var r = n % 100;
    var p = [];
    if (c > 0) { p.push(CT[c]); }
    if (r > 0) {
      if (r >= 20) {
        var d = Math.floor(r / 10);
        var u = r % 10;
        p.push(u > 0 ? DZ[d] + ' e ' + UN[u] : DZ[d]);
      } else {
        p.push(UN[r]);
      }
    }
    return p.join(' e ');
  }
  function inteiro(str) {
    var s = str.replace(/^0+/, '');
    if (s === '') { return { texto: 'zero', ultimo: 0 }; }
    var g = [];
    while (s.length > 0) {
      g.push(parseInt(s.slice(-3), 10));
      s = s.slice(0, -3);
    }
    var partes = [];
    var ultimo = -1;
    for (var i = g.length - 1; i >= 0; i--) {
      var v = g[i];
      if (v > 0) {
        var txt;
        if (i === 1 && v === 1) {
          txt = 'mil';
        } else {
          txt = grupo(v);
          if (i > 0) { txt = txt + ' ' + (v === 1 ? ESC_S[i] : ESC_P[i]); }
        }
        partes.push({ txt: txt, val: v });
        ultimo = i;
      }
    }
    var out = partes[0].txt;
    for (var k = 1; partes.length > k; k++) {
      var val = partes[k].val;
      var sep = ' e ';
      if (val >= 100) {
        if (val % 100 !== 0) { sep = ' '; }
      }
      out = out + sep + partes[k].txt;
    }
    return { texto: out, ultimo: ultimo };
  }
  function normalizar(v) {
    var t = String(v).trim().replace(/R\$/gi, '').replace(/\s/g, '');
    var neg = false;
    if (t.charAt(0) === '-') { neg = true; t = t.slice(1); }
    if (t.indexOf(',') > -1) {
      t = t.replace(/\./g, '').replace(',', '.');
    } else if (t.indexOf('.') > -1) {
      var pts = t.split('.');
      var ehMilhar = false;
      if (pts.length > 2) {
        ehMilhar = true;
      } else if (pts[1].length === 3) {
        if (pts[0] !== '0') { ehMilhar = true; }
      }
      if (ehMilhar) { t = t.replace(/\./g, ''); }
    }
    if (!/^\d+(\.\d+)?$/.test(t)) { return null; }
    var partes = t.split('.');
    var ip = partes[0].replace(/^0+/, '');
    if (ip === '') { ip = '0'; }
    return { neg: neg, inteira: ip, decimal: partes.length > 1 ? partes[1] : '' };
  }
  function moeda(n) {
    var dec = n.decimal;
    if (dec.length > 2) {
      if (/[1-9]/.test(dec.slice(2))) { return { erro: 'valores em reais aceitam no máximo 2 casas decimais (centavos).' }; }
    }
    dec = (dec + '00').slice(0, 2);
    var cent = parseInt(dec, 10);
    var partes = [];
    if (n.inteira !== '0') {
      var r = inteiro(n.inteira);
      var de = r.ultimo >= 2 ? ' de' : '';
      partes.push(r.texto + de + (n.inteira === '1' ? ' real' : ' reais'));
    }
    if (cent > 0) {
      partes.push(inteiro(String(cent)).texto + (cent === 1 ? ' centavo' : ' centavos'));
    }
    if (partes.length === 0) { return { texto: 'zero real' }; }
    return { texto: partes.join(' e '), zero: false };
  }
  function simples(n) {
    var dec = n.decimal.replace(/0+$/, '');
    if (dec.length > MAX_DECIMAIS) { return { erro: 'use no máximo ' + MAX_DECIMAIS + ' casas decimais.' }; }
    var base = inteiro(n.inteira).texto;
    if (dec === '') { return { texto: base }; }
    var num = dec.replace(/^0+/, '');
    var frac = inteiro(num).texto + ' ' + (num === '1' ? FRAC_S[dec.length] : FRAC_P[dec.length]);
    if (n.inteira === '0') { return { texto: frac }; }
    return { texto: base + (n.inteira === '1' ? ' inteiro' : ' inteiros') + ' e ' + frac };
  }
  function aplicarCaso(t, modo) {
    if (modo === 'mai') { return t.toUpperCase(); }
    if (modo === 'pri') { return t.charAt(0).toUpperCase() + t.slice(1); }
    return t;
  }
  function erro(msg) {
    caixa.style.borderColor = '#fca5a5';
    caixa.style.background = '#fef2f2';
    resultado.style.color = '#b91c1c';
    resultado.textContent = msg;
  }
  function converter() {
    var n = normalizar(campo.value);
    if (n === null) { erro('informe um número válido (ex.: 1234,56).'); return; }
    if (n.inteira.length > MAX_DIGITOS) { erro('o número é muito grande (máximo de ' + MAX_DIGITOS + ' dígitos antes da vírgula).'); return; }
    var unidade = selecionado('ext-unidade');
    var r = unidade === 'moeda' ? moeda(n) : simples(n);
    if (r.erro) { erro(r.erro); return; }
    var texto = r.texto;
    var ehZero = n.inteira === '0' && !/[1-9]/.test(n.decimal);
    if (n.neg) {
      if (!ehZero) { texto = 'menos ' + texto; }
    }
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    resultado.textContent = aplicarCaso(texto, selecionado('ext-caso'));
  }
  function limpar() {
    campo.value = '';
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    resultado.style.color = '#64748b';
    resultado.textContent = TEXTO_INICIAL;
    campo.focus();
  }
  function recalcular() {
    if (campo.value.trim() !== '') { converter(); }
  }
  document.getElementById('ext-converter').addEventListener('click', converter);
  document.getElementById('ext-limpar').addEventListener('click', limpar);
  var radios = document.querySelectorAll('#calc-extenso input[type="radio"]');
  for (var i = 0; radios.length > i; i++) {
    radios[i].addEventListener('change', recalcular);
  }
  campo.addEventListener('keydown', function (e) { if (e.key === 'Enter') { converter(); } });
  campo.addEventListener('focus', function () { campo.style.borderColor = '#6366f1'; });
  campo.addEventListener('blur', function () { campo.style.borderColor = '#c7d2fe'; });
})();
</script>

## Como usar a ferramenta

1. Em **1. Qual a unidade?**, escolha **Monetária (Reais)** para escrever valores em dinheiro ou **Numérica (Número Simples)** para escrever um número comum.
2. Em **2. Tipo de letra?**, escolha como o texto deve aparecer: **minúsculas**, **MAIÚSCULAS** ou **Primeira Maiúscula**.
3. Em **3. Digite o valor**, informe o número que deseja escrever por extenso.
4. Clique em **Escrever por Extenso** (ou pressione Enter) para ver o resultado.
5. Use o botão **Limpar** para apagar o valor e fazer uma nova conversão.

Use a vírgula para separar os decimais e, se quiser, o ponto para separar os milhares (por exemplo, `1.234,56` ou `1234,56`). Também é possível digitar números negativos (como `-15`) e o símbolo `R$` antes do valor. Ao trocar a unidade ou o tipo de letra, o resultado é atualizado automaticamente.

Exemplos de resultado:

- Monetária com `1234,56`: *mil duzentos e trinta e quatro reais e cinquenta e seis centavos*.
- Numérica com `1234,56`: *mil duzentos e trinta e quatro inteiros e cinquenta e seis centésimos*.

## Entendendo os termos

- **Número por extenso:** forma de escrever um número com palavras em vez de algarismos, como "vinte e cinco" no lugar de 25.
- **Unidade:** define o tipo de valor que será escrito, se é dinheiro (reais) ou um número simples.
- **Monetária (Reais):** escreve o valor como dinheiro, usando "real" ou "reais" para a parte inteira e "centavo" ou "centavos" para a parte decimal.
- **Numérica (Número Simples):** escreve o número sem moeda. A parte decimal é lida como fração, por exemplo, 0,5 vira "cinco décimos".
- **Tipo de letra:** define como as letras do resultado serão apresentadas.
- **minúsculas:** todas as letras do texto em minúsculo.
- **MAIÚSCULAS:** todas as letras do texto em maiúsculo, comum em cheques e contratos.
- **Primeira Maiúscula:** apenas a primeira letra do texto em maiúsculo, como em uma frase normal.
- **Casas decimais:** quantidade de dígitos depois da vírgula. Em reais, são os centavos e o limite é de duas casas.
- **Centavo:** centésima parte de um real. Cem centavos formam um real.
- **Número negativo:** número menor que zero, escrito com o sinal de menos e lido com a palavra "menos" no início.