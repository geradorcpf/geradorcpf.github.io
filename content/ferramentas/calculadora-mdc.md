---
title: "Calculadora de MDC"
seoTitle: "Calculadora de MDC"
description: "Calculadora de MDC: calcule o máximo divisor comum de dois ou mais números. Grátis e online, sem cadastro."
summary: "Calcule o máximo divisor comum de dois ou mais números."
date: 2026-10-23
draft: false
category: "matematica"
tags: ["mmc", "mdc", "calculadora", "matemática"]
keywords: ["calculadora de mdc", "calculadora de mdc online", "mmc", "mdc", "calculadora"]
---

<!--sudah dikerjakan-->

Calculadora online de MDC (máximo divisor comum) de 2 até 6 números naturais não nulos. Basta digitar os números nos campos abaixo e depois clicar em **Calcular MDC**.

<div id="calc-mdc" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🔢 Calculadora de MDC</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Informe de 2 até 6 números e veja o resultado na hora.</p>
<label for="mdc-n1" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Número 1</label>
<input id="mdc-n1" type="text" inputmode="numeric" placeholder="Ex.: 12" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<label for="mdc-n2" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Número 2</label>
<input id="mdc-n2" type="text" inputmode="numeric" placeholder="Ex.: 18" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<label for="mdc-n3" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Número 3 (opcional)</label>
<input id="mdc-n3" type="text" inputmode="numeric" placeholder="Ex.: 24" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<label for="mdc-n4" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Número 4 (opcional)</label>
<input id="mdc-n4" type="text" inputmode="numeric" placeholder="Opcional" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<label for="mdc-n5" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Número 5 (opcional)</label>
<input id="mdc-n5" type="text" inputmode="numeric" placeholder="Opcional" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<label for="mdc-n6" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Número 6 (opcional)</label>
<input id="mdc-n6" type="text" inputmode="numeric" placeholder="Opcional" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:20px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="mdc-calcular" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Calcular MDC</button>
<button type="button" id="mdc-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="mdc-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="mdc-resultado">preencha pelo menos dois números e clique em "Calcular MDC".</span></div>
</div>
<script>
(function () {
  var ids = ['mdc-n1', 'mdc-n2', 'mdc-n3', 'mdc-n4', 'mdc-n5', 'mdc-n6'];
  var campos = ids.map(function (id) { return document.getElementById(id); });
  var resultado = document.getElementById('mdc-resultado');
  var caixa = document.getElementById('mdc-resposta');
  var textoInicial = 'preencha pelo menos dois números e clique em "Calcular MDC".';
  function mdcDois(a, b) {
    while (b !== 0) {
      var t = a % b;
      a = b;
      b = t;
    }
    return a;
  }
  function fmt(n) { return n.toLocaleString('pt-BR'); }
  function listar(arr) {
    var txt = arr.map(fmt);
    if (txt.length === 2) { return txt[0] + ' e ' + txt[1]; }
    return txt.slice(0, txt.length - 1).join(', ') + ' e ' + txt[txt.length - 1];
  }
  function erro(msg) {
    caixa.style.borderColor = '#fca5a5';
    caixa.style.background = '#fef2f2';
    resultado.style.color = '#b91c1c';
    resultado.textContent = msg;
  }
  function calcular() {
    var nums = [];
    var invalido = false;
    campos.forEach(function (c) {
      var t = c.value.trim();
      if (t === '') { return; }
      if (!/^[0-9]+$/.test(t)) { invalido = true; return; }
      nums.push(Number(t));
    });
    if (invalido) { erro('use apenas números naturais (inteiros positivos), sem vírgula, ponto ou sinal.'); return; }
    if (nums.length === 0 || nums.length === 1) { erro('informe pelo menos dois números.'); return; }
    if (nums.some(function (n) { return n === 0; })) { erro('os números devem ser maiores que zero.'); return; }
    if (nums.some(function (n) { return !Number.isSafeInteger(n); })) { erro('um dos números é grande demais. Use valores menores.'); return; }
    var atual = nums[0];
    var passos = [];
    nums.slice(1).forEach(function (n) {
      var r = mdcDois(atual, n);
      passos.push('MDC(' + fmt(atual) + ', ' + fmt(n) + ') = ' + fmt(r));
      atual = r;
    });
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    resultado.textContent = '';
    var forte = document.createElement('strong');
    forte.style.fontSize = '1.2rem';
    forte.textContent = fmt(atual);
    var detalhe = document.createElement('small');
    detalhe.style.color = '#475569';
    detalhe.textContent = passos.join('  →  ');
    resultado.appendChild(document.createTextNode('O MDC de ' + listar(nums) + ' é '));
    resultado.appendChild(forte);
    resultado.appendChild(document.createElement('br'));
    resultado.appendChild(detalhe);
  }
  function limpar() {
    campos.forEach(function (c) { c.value = ''; });
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    resultado.style.color = '#64748b';
    resultado.textContent = textoInicial;
    campos[0].focus();
  }
  document.getElementById('mdc-calcular').addEventListener('click', calcular);
  document.getElementById('mdc-limpar').addEventListener('click', limpar);
  campos.forEach(function (el) {
    el.addEventListener('keydown', function (e) { if (e.key === 'Enter') { calcular(); } });
    el.addEventListener('focus', function () { el.style.borderColor = '#6366f1'; });
    el.addEventListener('blur', function () { el.style.borderColor = '#c7d2fe'; });
  });
})();
</script>

## Como usar a calculadora

1. Digite o primeiro número no campo **Número 1**.
2. Digite o segundo número no campo **Número 2**.
3. Se quiser, preencha também os campos opcionais (**Número 3** até **Número 6**). Você pode calcular o MDC de 2 até 6 números.
4. Clique em **Calcular MDC** (ou pressione Enter) para ver o resultado.
5. Use o botão **Limpar** para apagar os valores e fazer um novo cálculo.

Use apenas números naturais não nulos, ou seja, inteiros positivos como `12`, `18` e `24`. Não use vírgula, ponto, sinal de menos nem o número zero. Abaixo do resultado, a calculadora mostra o passo a passo: o MDC é calculado para os dois primeiros números e depois combinado com os seguintes.

## Entendendo os termos

- **MDC (Máximo Divisor Comum):** o maior número que divide, ao mesmo tempo e sem deixar resto, todos os números informados.
- **Divisor:** número que divide outro de forma exata. Por exemplo, 3 é divisor de 12, pois 12 ÷ 3 = 4.
- **Divisor comum:** divisor que aparece na lista de divisores de dois ou mais números ao mesmo tempo.
- **Número natural:** número inteiro e não negativo (0, 1, 2, 3...). Nesta calculadora, só são aceitos os naturais maiores que zero.
- **Resto da divisão:** o que sobra quando a divisão não é exata. Quando o resto é zero, a divisão é exata.
- **Números primos entre si:** números cujo único divisor comum é 1. Nesse caso, o MDC é igual a 1.
- **Algoritmo de Euclides:** método que calcula o MDC por divisões sucessivas, repetindo o processo com o divisor e o resto até que o resto seja zero. O último divisor é o MDC. É o método usado por esta calculadora.
