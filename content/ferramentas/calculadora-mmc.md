---
title: "Calculadora de MMC"
seoTitle: "Calculadora de MMC"
description: "Calculadora de MMC: calcule o mínimo múltiplo comum de dois ou mais números. Grátis e online, sem cadastro."
summary: "Calcule o mínimo múltiplo comum de dois ou mais números."
date: 2026-10-20
draft: false
category: "matematica"
tags: ["mmc", "mdc", "calculadora", "matemática"]
keywords: ["calculadora de mmc", "calculadora de mmc online", "mmc", "mdc", "calculadora"]
---

<!--sudah dikerjakan-->

Basta digitar de 2 até 6 números naturais nos campos abaixo e depois clicar em **Calcular MMC**.

<div id="calc-mmc" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🔢 Calculadora de MMC</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Informe de 2 até 6 números e veja o resultado na hora.</p>
<div style="display:grid;grid-template-columns:1fr 1fr;gap:0 14px;">
<div>
<label for="mmc-n1" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Número 1</label>
<input id="mmc-n1" type="text" inputmode="numeric" placeholder="Ex.: 8" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
</div>
<div>
<label for="mmc-n2" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Número 2</label>
<input id="mmc-n2" type="text" inputmode="numeric" placeholder="Ex.: 12" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
</div>
<div>
<label for="mmc-n3" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Número 3</label>
<input id="mmc-n3" type="text" inputmode="numeric" placeholder="Opcional" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
</div>
<div>
<label for="mmc-n4" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Número 4</label>
<input id="mmc-n4" type="text" inputmode="numeric" placeholder="Opcional" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
</div>
<div>
<label for="mmc-n5" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Número 5</label>
<input id="mmc-n5" type="text" inputmode="numeric" placeholder="Opcional" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
</div>
<div>
<label for="mmc-n6" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Número 6</label>
<input id="mmc-n6" type="text" inputmode="numeric" placeholder="Opcional" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
</div>
</div>
<div style="display:flex;gap:10px;flex-wrap:wrap;margin-top:4px;">
<button type="button" id="mmc-calcular" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Calcular MMC</button>
<button type="button" id="mmc-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="mmc-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="mmc-resultado">preencha os campos e clique em "Calcular MMC".</span></div>
</div>
<script>
(function () {
  var campos = [1, 2, 3, 4, 5, 6].map(function (i) { return document.getElementById('mmc-n' + i); });
  var resultado = document.getElementById('mmc-resultado');
  var caixa = document.getElementById('mmc-resposta');
  var LIMITE_PASSOS = 1000000;
  function fmt(n) { return n.toLocaleString('pt-BR'); }
  function erro(msg) {
    caixa.style.borderColor = '#fca5a5';
    caixa.style.background = '#fef2f2';
    resultado.style.color = '#b91c1c';
    resultado.textContent = msg;
  }
  function mdc(a, b) {
    while (b !== 0) {
      var t = a % b;
      a = b;
      b = t;
    }
    return a;
  }
  function ler() {
    var lista = [];
    var msg = '';
    campos.forEach(function (campo) {
      var t = campo.value.trim();
      if (t === '') { return; }
      if (/^[0-9]+$/.test(t)) {
        var n = Number(t);
        if (n === 0) { msg = 'use apenas números naturais maiores que zero.'; }
        else if (!Number.isSafeInteger(n)) { msg = 'um dos números é grande demais.'; }
        else { lista.push(n); }
      } else {
        msg = 'digite apenas números naturais (sem vírgula, ponto ou sinal).';
      }
    });
    return { lista: lista, msg: msg };
  }
  function fatorar(lista) {
    var atual = lista.slice();
    var linhas = [];
    var divisores = [];
    var d = 2;
    function restam() { return atual.some(function (x) { return x !== 1; }); }
    while (restam()) {
      if (atual.some(function (x) { return x % d === 0; })) {
        linhas.push(atual.join(', ') + '  |  ' + d);
        divisores.push(d);
        atual = atual.map(function (x) { return x % d === 0 ? x / d : x; });
      } else {
        d = d + 1;
      }
    }
    linhas.push(atual.join(', ') + '  |');
    return { linhas: linhas, divisores: divisores };
  }
  function calcular() {
    var dados = ler();
    if (dados.msg !== '') { erro(dados.msg); return; }
    var lista = dados.lista;
    if (lista.length === 0) { erro('informe pelo menos dois números.'); return; }
    if (lista.length === 1) { erro('informe pelo menos dois números.'); return; }
    var mmc = lista[0];
    lista.forEach(function (n) { mmc = (mmc / mdc(mmc, n)) * n; });
    if (!Number.isSafeInteger(mmc)) { erro('o resultado é grande demais para ser calculado.'); return; }
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    resultado.textContent = '';
    resultado.appendChild(document.createTextNode('O MMC de ' + lista.join(', ') + ' é '));
    var destaque = document.createElement('strong');
    destaque.style.fontSize = '1.2rem';
    destaque.textContent = fmt(mmc);
    resultado.appendChild(destaque);
    if (Math.min(Math.max.apply(null, lista), LIMITE_PASSOS) === Math.max.apply(null, lista)) {
      var f = fatorar(lista);
      var detalhe = document.createElement('div');
      detalhe.style.marginTop = '10px';
      detalhe.style.fontSize = '0.9rem';
      detalhe.style.color = '#475569';
      var titulo = document.createElement('div');
      titulo.style.fontWeight = '600';
      titulo.textContent = 'Fatoração simultânea:';
      var tabela = document.createElement('div');
      tabela.style.whiteSpace = 'pre-line';
      tabela.style.fontFamily = 'ui-monospace,SFMono-Regular,Menlo,Consolas,monospace';
      tabela.style.margin = '4px 0 8px';
      tabela.textContent = f.linhas.join('\n');
      var conta = document.createElement('div');
      conta.textContent = 'MMC = ' + f.divisores.join(' × ') + ' = ' + fmt(mmc);
      detalhe.appendChild(titulo);
      detalhe.appendChild(tabela);
      detalhe.appendChild(conta);
      resultado.appendChild(detalhe);
    }
  }
  function limpar() {
    campos.forEach(function (c) { c.value = ''; });
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    resultado.style.color = '#64748b';
    resultado.textContent = 'preencha os campos e clique em "Calcular MMC".';
    campos[0].focus();
  }
  document.getElementById('mmc-calcular').addEventListener('click', calcular);
  document.getElementById('mmc-limpar').addEventListener('click', limpar);
  campos.forEach(function (el) {
    el.addEventListener('keydown', function (e) { if (e.key === 'Enter') { calcular(); } });
    el.addEventListener('focus', function () { el.style.borderColor = '#6366f1'; });
    el.addEventListener('blur', function () { el.style.borderColor = '#c7d2fe'; });
  });
})();
</script>

## Como usar a calculadora

1. Digite o primeiro número no campo **Número 1** e o segundo no campo **Número 2**.
2. Se quiser, preencha também os campos **Número 3** até **Número 6**. Os campos vazios são ignorados.
3. Clique em **Calcular MMC** (ou pressione Enter) para ver o resultado.
4. Confira a **fatoração simultânea**, que mostra o passo a passo do cálculo.
5. Use o botão **Limpar** para apagar os valores e fazer um novo cálculo.

Use apenas números naturais maiores que zero, sem vírgula, ponto ou sinal (por exemplo, `8`, `12` ou `45`).

## Entendendo os termos

- **MMC (mínimo múltiplo comum):** o menor número maior que zero que é múltiplo de todos os números informados ao mesmo tempo.
- **Múltiplo:** resultado da multiplicação de um número por qualquer número natural. Os múltiplos de 3 são 3, 6, 9, 12 e assim por diante.
- **Múltiplo comum:** número que é múltiplo de dois ou mais números ao mesmo tempo. Por exemplo, 24 é múltiplo comum de 6 e 8.
- **Número natural:** número inteiro e positivo usado para contar (1, 2, 3, 4...). Nesta calculadora, o zero não é aceito.
- **Divisor:** número que divide outro de forma exata, sem deixar resto. O 4 é divisor de 12, pois 12 ÷ 4 = 3.
- **Número primo:** número natural maior que 1 que só tem dois divisores: o 1 e ele mesmo, como 2, 3, 5, 7 e 11.
- **Fatoração simultânea:** método que divide todos os números ao mesmo tempo, sempre pelo menor número primo possível, até todos chegarem a 1. O MMC é o produto desses divisores.
- **MDC (máximo divisor comum):** o maior número que divide todos os números informados de forma exata. Ele se relaciona com o MMC: para dois números, MMC × MDC = produto dos dois números.