---
title: "Calculadora de Regra de Três Simples"
seoTitle: "Calculadora de Regra de Três Simples"
description: "Calculadora de Regra de Três Simples: resolva regra de três simples com o passo a passo. Grátis e online, sem cadastro."
summary: "Resolva regra de três simples com o passo a passo."
date: 2026-10-22
draft: false
category: "matematica"
tags: ["regra de três", "proporção", "calculadora", "matemática"]
keywords: ["calculadora de regra de três simples", "calculadora de regra de três simples online", "regra de três", "proporção", "calculadora"]
---
<!--sudah dikerjakan-->

Basta digitar os três valores conhecidos abaixo, escolher o tipo de proporção e depois clicar em **Calcular X**.

<div id="calc-regra-tres" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🧮 Calculadora de Regra de Três Simples</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Informe A, B e C e descubra o valor de X na hora.</p>
<label for="r3-tipo" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Tipo de proporção</label>
<select id="r3-tipo" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<option value="direta">Diretamente proporcional</option>
<option value="inversa">Inversamente proporcional</option>
</select>
<label for="r3-a" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Valor de A</label>
<input id="r3-a" type="text" inputmode="decimal" placeholder="Ex.: 2" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<label for="r3-b" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">está para Valor de B</label>
<input id="r3-b" type="text" inputmode="decimal" placeholder="Ex.: 10" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<label for="r3-c" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">assim como Valor de C</label>
<input id="r3-c" type="text" inputmode="decimal" placeholder="Ex.: 6" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:20px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="r3-calcular" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Calcular X</button>
<button type="button" id="r3-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="r3-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="r3-resultado">preencha os campos e clique em "Calcular X".</span></div>
</div>
<script>
(function () {
  var tipo = document.getElementById('r3-tipo');
  var campoA = document.getElementById('r3-a');
  var campoB = document.getElementById('r3-b');
  var campoC = document.getElementById('r3-c');
  var resultado = document.getElementById('r3-resultado');
  var caixa = document.getElementById('r3-resposta');
  function numero(v) {
    var t = String(v).trim().replace(/\s/g, '');
    if (t.indexOf(',') > -1) { t = t.replace(/\./g, '').replace(',', '.'); }
    if (t === '' || isNaN(Number(t))) { return NaN; }
    return Number(t);
  }
  function fmt(n) { return n.toLocaleString('pt-BR', { maximumFractionDigits: 6 }); }
  function erro(msg) {
    caixa.style.borderColor = '#fca5a5';
    caixa.style.background = '#fef2f2';
    resultado.style.color = '#b91c1c';
    resultado.textContent = msg;
  }
  function calcular() {
    var a = numero(campoA.value);
    var b = numero(campoB.value);
    var c = numero(campoC.value);
    if (isNaN(a) || isNaN(b) || isNaN(c)) { erro('informe números válidos nos campos A, B e C.'); return; }
    var inversa = tipo.value === 'inversa';
    var x;
    var conta;
    if (inversa) {
      if (c === 0) { erro('na proporção inversa, o valor de C não pode ser zero.'); return; }
      x = (a * b) / c;
      conta = 'X = (' + fmt(a) + ' × ' + fmt(b) + ') ÷ ' + fmt(c) + ' = ' + fmt(x);
    } else {
      if (a === 0) { erro('na proporção direta, o valor de A não pode ser zero.'); return; }
      x = (b * c) / a;
      conta = 'X = (' + fmt(b) + ' × ' + fmt(c) + ') ÷ ' + fmt(a) + ' = ' + fmt(x);
    }
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    resultado.innerHTML = 'O valor de X é <strong style="font-size:1.2rem;">' + fmt(x) + '</strong><br><small style="color:#475569;">' + conta + '</small>';
  }
  function limpar() {
    campoA.value = '';
    campoB.value = '';
    campoC.value = '';
    tipo.value = 'direta';
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    resultado.style.color = '#64748b';
    resultado.textContent = 'preencha os campos e clique em "Calcular X".';
    campoA.focus();
  }
  document.getElementById('r3-calcular').addEventListener('click', calcular);
  document.getElementById('r3-limpar').addEventListener('click', limpar);
  [campoA, campoB, campoC, tipo].forEach(function (el) {
    el.addEventListener('keydown', function (e) { if (e.key === 'Enter') { calcular(); } });
    el.addEventListener('focus', function () { el.style.borderColor = '#6366f1'; });
    el.addEventListener('blur', function () { el.style.borderColor = '#c7d2fe'; });
  });
})();
</script>

## Como usar a calculadora

1. Escolha o **Tipo de proporção**: diretamente proporcional (quando uma grandeza aumenta, a outra também aumenta) ou inversamente proporcional (quando uma aumenta, a outra diminui).
2. Digite o **Valor de A** no primeiro campo.
3. Digite o **Valor de B**, que corresponde ao valor de A na outra grandeza.
4. Digite o **Valor de C**, que está na mesma grandeza de A.
5. Clique em **Calcular X** (ou pressione Enter) para ver o resultado e a conta feita.
6. Use o botão **Limpar** para apagar os valores e fazer um novo cálculo.

Você pode usar números inteiros ou decimais, com vírgula ou ponto (por exemplo, `7,5` ou `7.5`). Os valores de A e C devem estar na mesma unidade de medida, assim como os valores de B e X.

## Entendendo os termos

- **Regra de três simples:** método matemático para descobrir um valor desconhecido a partir de outros três valores conhecidos, relacionando duas grandezas.
- **Grandeza:** qualquer coisa que pode ser medida ou contada, como tempo, quantidade, velocidade, preço ou distância.
- **Valor de A:** primeiro valor conhecido, que pertence à primeira grandeza.
- **Valor de B:** valor da segunda grandeza que corresponde ao valor de A.
- **Valor de C:** segundo valor conhecido da primeira grandeza, para o qual queremos descobrir o correspondente na segunda grandeza.
- **X:** valor desconhecido que a calculadora encontra, correspondente ao valor de C na segunda grandeza.
- **Proporção:** relação de igualdade entre duas razões, como A está para B assim como C está para X.
- **Diretamente proporcional:** quando as grandezas variam no mesmo sentido; se uma dobra, a outra também dobra.
- **Inversamente proporcional:** quando as grandezas variam em sentidos opostos; se uma dobra, a outra cai pela metade.