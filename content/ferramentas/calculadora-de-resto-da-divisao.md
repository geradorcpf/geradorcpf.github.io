---
title: "Calculadora de Resto da Divisão"
seoTitle: "Calculadora de Resto da Divisão"
description: "Calculadora de Resto da Divisão: descubra o quociente e o resto de uma divisão. Grátis e online, sem cadastro."
summary: "Descubra o quociente e o resto de uma divisão."
date: 2026-10-22
draft: false
category: "matematica"
tags: ["divisão", "calculadora", "matemática"]
keywords: ["calculadora de resto da divisão", "calculadora de resto da divisão online", "divisão", "calculadora", "matemática"]
---

<!--sudah dikerjakan-->

Basta digitar os números abaixo e depois clicar em **Calcular Resto**. Atenção: a calculadora não funciona com números fracionados.

<div id="calc-resto-divisao" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">➗ Calculadora de Resto da Divisão</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Informe os dois números inteiros e veja o quociente e o resto na hora.</p>
<label for="rd-dividendo" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Quanto é o resto da divisão de (dividendo)</label>
<input id="rd-dividendo" type="text" inputmode="numeric" placeholder="Ex.: 17" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<label for="rd-divisor" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">por (divisor)</label>
<input id="rd-divisor" type="text" inputmode="numeric" placeholder="Ex.: 5" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:20px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="rd-calcular" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Calcular Resto</button>
<button type="button" id="rd-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="rd-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="rd-resultado">preencha os campos e clique em "Calcular Resto".</span></div>
</div>
<script>
(function () {
  var campoDividendo = document.getElementById('rd-dividendo');
  var campoDivisor = document.getElementById('rd-divisor');
  var resultado = document.getElementById('rd-resultado');
  var caixa = document.getElementById('rd-resposta');
  function inteiro(v) {
    var t = String(v).trim().replace(/\s/g, '');
    if (/^[+-]?\d+$/.test(t)) { return BigInt(t); }
    return null;
  }
  function temDecimal(v) {
    return /[.,]/.test(String(v));
  }
  function fmt(n) { return n.toLocaleString('pt-BR'); }
  function erro(msg) {
    caixa.style.borderColor = '#fca5a5';
    caixa.style.background = '#fef2f2';
    resultado.style.color = '#b91c1c';
    resultado.textContent = msg;
  }
  function calcular() {
    var vA = campoDividendo.value;
    var vB = campoDivisor.value;
    if (temDecimal(vA) || temDecimal(vB)) { erro('a calculadora não funciona com números fracionados. Use apenas números inteiros.'); return; }
    var a = inteiro(vA);
    var b = inteiro(vB);
    if (a === null || b === null) { erro('informe números inteiros válidos nos dois campos.'); return; }
    if (b === 0n) { erro('o divisor não pode ser zero.'); return; }
    var q = a / b;
    var r = a % b;
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    resultado.innerHTML = 'O resto da divisão é <strong style="font-size:1.2rem;">' + fmt(r) + '</strong><br><small style="color:#475569;">Quociente: ' + fmt(q) + '<br>' + fmt(a) + ' = ' + fmt(b) + ' × ' + fmt(q) + ' + ' + fmt(r) + '</small>';
  }
  function limpar() {
    campoDividendo.value = '';
    campoDivisor.value = '';
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    resultado.style.color = '#64748b';
    resultado.textContent = 'preencha os campos e clique em "Calcular Resto".';
    campoDividendo.focus();
  }
  document.getElementById('rd-calcular').addEventListener('click', calcular);
  document.getElementById('rd-limpar').addEventListener('click', limpar);
  [campoDividendo, campoDivisor].forEach(function (el) {
    el.addEventListener('keydown', function (e) { if (e.key === 'Enter') { calcular(); } });
    el.addEventListener('focus', function () { el.style.borderColor = '#6366f1'; });
    el.addEventListener('blur', function () { el.style.borderColor = '#c7d2fe'; });
  });
})();
</script>

## Como usar a calculadora

1. Digite o **dividendo** (o número que será dividido) no primeiro campo.
2. Digite o **divisor** (o número pelo qual você quer dividir) no segundo campo.
3. Clique em **Calcular Resto** (ou pressione Enter) para ver o resto e o quociente.
4. Use o botão **Limpar** para apagar os valores e fazer um novo cálculo.

Use apenas números inteiros, sem vírgula nem ponto decimal. A calculadora não funciona com números fracionados, e o divisor não pode ser zero.

## Entendendo os termos

- **Divisão inteira:** divisão em que o resultado é composto por um quociente inteiro e um resto, sem casas decimais.
- **Dividendo:** o número que está sendo dividido.
- **Divisor:** o número que divide o dividendo, ou seja, quantas partes iguais você quer formar. Não pode ser zero.
- **Quociente:** o resultado inteiro da divisão, isto é, quantas vezes o divisor cabe por completo no dividendo.
- **Resto:** o que sobra do dividendo depois de retirar o maior múltiplo possível do divisor. Em uma divisão com números positivos, ele é sempre menor que o divisor.
- **Número fracionado:** número com parte decimal (como 2,5), que não pode ser usado nesta calculadora.