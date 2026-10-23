---
title: "Calcular IMC"
seoTitle: "Calcular IMC: online e grátis"
description: "Calcular IMC: calcule seu Índice de Massa Corporal e veja a faixa. Grátis e online, sem cadastro."
summary: "Calcule seu Índice de Massa Corporal e veja a faixa."
date: 2026-10-23
draft: false
category: "saude"
tags: ["imc", "peso", "saúde"]
keywords: ["calcular imc", "calcular imc online", "imc", "peso", "saúde"]
---
<!--sudah dikerjakan-->

Basta digitar o seu peso e a sua altura abaixo e depois clicar em **Calcular IMC**.

<div id="calc-imc" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">⚖️ Calculadora de IMC</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Informe o peso e a altura e veja o resultado na hora.</p>
<label for="imc-peso" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Peso (kg)</label>
<input id="imc-peso" type="text" inputmode="decimal" placeholder="Ex.: 70" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<label for="imc-altura" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Altura (cm)</label>
<input id="imc-altura" type="text" inputmode="decimal" placeholder="Ex.: 175" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:20px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="imc-calcular" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Calcular IMC</button>
<button type="button" id="imc-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="imc-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="imc-resultado">preencha os campos e clique em "Calcular IMC".</span><div id="imc-detalhe" style="margin-top:8px;"><span id="imc-valor" style="display:block;font-size:1.6rem;font-weight:700;"></span><span id="imc-situacao" style="display:block;font-weight:600;"></span><span id="imc-formula" style="display:block;font-size:0.85rem;color:#475569;margin-top:4px;"></span></div></div>
</div>
<script>
(function () {
  var peso = document.getElementById('imc-peso');
  var altura = document.getElementById('imc-altura');
  var resultado = document.getElementById('imc-resultado');
  var caixa = document.getElementById('imc-resposta');
  var valorEl = document.getElementById('imc-valor');
  var situacaoEl = document.getElementById('imc-situacao');
  var formulaEl = document.getElementById('imc-formula');
  function numero(v) {
    var t = String(v).trim().replace(/\s/g, '');
    if (t.indexOf(',') > -1) { t = t.replace(/\./g, '').replace(',', '.'); }
    if (t === '' || isNaN(Number(t))) { return NaN; }
    return Number(t);
  }
  function fmt(n, casas) {
    return n.toLocaleString('pt-BR', { minimumFractionDigits: casas, maximumFractionDigits: casas });
  }
  function faixa(imc) {
    if (imc >= 40) { return { nome: 'Obesidade grau III', msg: 'Você está com obesidade grau III. Procure orientação médica.', cor: '#991b1b', bg: '#fef2f2', borda: '#fca5a5' }; }
    if (imc >= 35) { return { nome: 'Obesidade grau II', msg: 'Você está com obesidade grau II. Procure orientação médica.', cor: '#b91c1c', bg: '#fef2f2', borda: '#fca5a5' }; }
    if (imc >= 30) { return { nome: 'Obesidade grau I', msg: 'Você está com obesidade grau I. Procure orientação médica.', cor: '#c2410c', bg: '#fff7ed', borda: '#fdba74' }; }
    if (imc >= 25) { return { nome: 'Sobrepeso', msg: 'Você está com sobrepeso.', cor: '#a16207', bg: '#fefce8', borda: '#fde047' }; }
    if (imc >= 18.5) { return { nome: 'Peso ideal', msg: 'Parabéns, você está em seu peso ideal.', cor: '#166534', bg: '#f0fdf4', borda: '#86efac' }; }
    return { nome: 'Abaixo do peso ideal', msg: 'Você está abaixo do peso ideal.', cor: '#1d4ed8', bg: '#eff6ff', borda: '#93c5fd' };
  }
  function limparDetalhe() {
    valorEl.textContent = '';
    situacaoEl.textContent = '';
    formulaEl.textContent = '';
  }
  function erro(msg) {
    limparDetalhe();
    caixa.style.borderColor = '#fca5a5';
    caixa.style.background = '#fef2f2';
    resultado.style.color = '#b91c1c';
    resultado.textContent = msg;
  }
  function calcular() {
    var p = numero(peso.value);
    var a = numero(altura.value);
    if (isNaN(p) || isNaN(a)) { erro('informe números válidos para o peso e a altura.'); return; }
    if (!(p > 0) || !(a > 0)) { erro('o peso e a altura devem ser maiores que zero.'); return; }
    if (!(a >= 50)) { erro('informe a altura em centímetros (por exemplo, 175).'); return; }
    var m = a / 100;
    var imc = p / (m * m);
    var f = faixa(imc);
    caixa.style.borderColor = f.borda;
    caixa.style.background = f.bg;
    resultado.style.color = f.cor;
    resultado.textContent = f.msg;
    valorEl.style.color = f.cor;
    situacaoEl.style.color = f.cor;
    valorEl.textContent = 'IMC: ' + fmt(imc, 2);
    situacaoEl.textContent = 'Situação: ' + f.nome;
    formulaEl.textContent = 'IMC = ' + fmt(p, 2) + ' ÷ (' + fmt(m, 2) + ' × ' + fmt(m, 2) + ') = ' + fmt(imc, 2);
  }
  function limpar() {
    peso.value = '';
    altura.value = '';
    limparDetalhe();
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    resultado.style.color = '#64748b';
    resultado.textContent = 'preencha os campos e clique em "Calcular IMC".';
    peso.focus();
  }
  document.getElementById('imc-calcular').addEventListener('click', calcular);
  document.getElementById('imc-limpar').addEventListener('click', limpar);
  [peso, altura].forEach(function (el) {
    el.addEventListener('keydown', function (e) { if (e.key === 'Enter') { calcular(); } });
    el.addEventListener('focus', function () { el.style.borderColor = '#6366f1'; });
    el.addEventListener('blur', function () { el.style.borderColor = '#c7d2fe'; });
  });
})();
</script>

## Como usar a calculadora

1. Digite o seu **Peso** em quilogramas (kg) no primeiro campo.
2. Digite a sua **Altura** em centímetros (cm) no segundo campo.
3. Clique em **Calcular IMC** (ou pressione Enter) para ver o resultado e a faixa em que você está.
4. Use o botão **Limpar** para apagar os valores e fazer um novo cálculo.

Você pode usar números inteiros ou decimais, com vírgula ou ponto (por exemplo, `70,5` ou `70.5`). A altura deve ser informada em centímetros: para 1,75 m, digite `175`.

## Entendendo os termos

- **IMC (Índice de Massa Corporal):** número que relaciona o peso e a altura de uma pessoa e serve como referência para avaliar se o peso está adequado.
- **Peso (kg):** massa corporal da pessoa, medida em quilogramas.
- **Altura (cm):** estatura da pessoa, medida em centímetros. No cálculo, ela é convertida para metros.
- **Abaixo do peso ideal:** IMC menor que 18,5. Indica peso abaixo do considerado adequado para a altura.
- **Peso ideal:** IMC entre 18,5 e 24,9. É a faixa considerada adequada para a altura.
- **Sobrepeso:** IMC entre 25,0 e 29,9. O peso está acima do adequado.
- **Obesidade grau I, II e III:** faixas de IMC a partir de 30, em que o grau aumenta conforme o IMC (I: 30,0 a 34,9; II: 35,0 a 39,9; III: 40 ou mais).

## Tabela de classificação do IMC

| Resultado | Situação |
|-----------|----------|
| Abaixo de 18,5 | Abaixo do peso ideal |
| Entre 18,5 e 24,9 | Peso ideal |
| Entre 25,0 e 29,9 | Sobrepeso |
| Entre 30,0 e 34,9 | Obesidade grau I |
| Entre 35,0 e 39,9 | Obesidade grau II |
| Entre 40 e acima | Obesidade grau III |

## Fórmula do IMC

O IMC é o peso dividido pela altura ao quadrado:

**IMC = peso ÷ (altura × altura)**

Nessa fórmula, o peso é dado em quilogramas (kg) e a altura em metros (m).

## Exemplo resolvido

Uma pessoa pesa 70 kg e mede 175 cm. Qual é o seu IMC?

1. Converta a altura para metros: 175 cm = 1,75 m.
2. Aplique a fórmula: IMC = 70 ÷ (1,75 × 1,75).
3. Calcule: IMC = 70 ÷ 3,0625 = 22,86.

**Resposta:** o IMC é de **22,86**, que está na faixa de **peso ideal**.

O IMC é apenas uma referência e não substitui a avaliação de um médico ou nutricionista.