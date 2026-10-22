---
title: "Cálculo de Combustível"
seoTitle: "Cálculo de Combustível"
description: "Cálculo de Combustível: calcule o gasto de combustível de uma viagem. Grátis e online, sem cadastro."
summary: "Calcule o gasto de combustível de uma viagem."
date: 2026-10-22
draft: false
category: "financas"
tags: ["combustível", "veículos", "viagem", "calculadora"]
keywords: ["cálculo de combustível", "cálculo de combustível online", "combustível", "veículos", "viagem"]
---
<!--SUDAH DIKERJAKAN-->

Informe a distância, o consumo do veículo e o preço por litro abaixo e depois clique em **Calcular**.

<div id="calc-combustivel" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">⛽ Cálculo de Combustível</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Informe os dados da viagem e veja o custo na hora.</p>
<label for="comb-distancia" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Distância (km)</label>
<input id="comb-distancia" type="text" inputmode="decimal" placeholder="Ex.: 350" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<label for="comb-consumo" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Consumo do veículo (km/litro)</label>
<input id="comb-consumo" type="text" inputmode="decimal" placeholder="Ex.: 12" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<label for="comb-preco" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Preço por litro (R$)</label>
<input id="comb-preco" type="text" inputmode="decimal" placeholder="Ex.: 5,89" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:20px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="comb-calcular" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Calcular</button>
<button type="button" id="comb-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="comb-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="comb-resultado">preencha os campos e clique em "Calcular".</span></div>
</div>
<script>
(function () {
  var distancia = document.getElementById('comb-distancia');
  var consumo = document.getElementById('comb-consumo');
  var preco = document.getElementById('comb-preco');
  var resultado = document.getElementById('comb-resultado');
  var caixa = document.getElementById('comb-resposta');
  function numero(v) {
    var t = String(v).trim().replace(/\s/g, '').replace(/^R\$/i, '');
    if (t.indexOf(',') > -1) { t = t.replace(/\./g, '').replace(',', '.'); }
    if (t === '' || isNaN(Number(t))) { return NaN; }
    return Number(t);
  }
  function fmt(n) { return n.toLocaleString('pt-BR', { maximumFractionDigits: 2 }); }
  function moeda(n) { return n.toLocaleString('pt-BR', { style: 'currency', currency: 'BRL' }); }
  function erro(msg) {
    caixa.style.borderColor = '#fca5a5';
    caixa.style.background = '#fef2f2';
    resultado.style.color = '#b91c1c';
    resultado.textContent = msg;
  }
  function calcular() {
    var d = numero(distancia.value);
    var c = numero(consumo.value);
    var p = numero(preco.value);
    if (isNaN(d) || isNaN(c) || isNaN(p)) { erro('informe números válidos nos três campos.'); return; }
    if (d <= 0 || c <= 0 || p <= 0) { erro('todos os valores devem ser maiores que zero.'); return; }
    var litros = d / c;
    var custo = litros * p;
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    resultado.innerHTML = 'O custo estimado da viagem é <strong style="font-size:1.2rem;">' + moeda(custo) + '</strong><br>' +
      '<small style="color:#475569;">Combustível necessário: ' + fmt(litros) + ' litros<br>' +
      'Litros = ' + fmt(d) + ' ÷ ' + fmt(c) + ' = ' + fmt(litros) + '<br>' +
      'Custo = ' + fmt(litros) + ' × ' + moeda(p) + ' = ' + moeda(custo) + '</small>';
  }
  function limpar() {
    distancia.value = '';
    consumo.value = '';
    preco.value = '';
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    resultado.style.color = '#64748b';
    resultado.textContent = 'preencha os campos e clique em "Calcular".';
    distancia.focus();
  }
  document.getElementById('comb-calcular').addEventListener('click', calcular);
  document.getElementById('comb-limpar').addEventListener('click', limpar);
  [distancia, consumo, preco].forEach(function (el) {
    el.addEventListener('keydown', function (e) { if (e.key === 'Enter') { calcular(); } });
    el.addEventListener('focus', function () { el.style.borderColor = '#6366f1'; });
    el.addEventListener('blur', function () { el.style.borderColor = '#c7d2fe'; });
  });
})();
</script>

## Como usar a calculadora

1. Digite a **Distância (km)** que você pretende percorrer no primeiro campo.
2. Digite o **Consumo do veículo (km/litro)**, ou seja, quantos quilômetros o carro faz com 1 litro.
3. Digite o **Preço por litro (R$)** praticado no posto.
4. Clique em **Calcular** (ou pressione Enter) para ver a quantidade de combustível e o custo estimado da viagem.
5. Use o botão **Limpar** para apagar os valores e fazer um novo cálculo.

Você pode usar números inteiros ou decimais, com vírgula ou ponto (por exemplo, `5,89` ou `5.89`). Para uma viagem de ida e volta, informe a distância total do percurso. O consumo real varia conforme o trânsito, a velocidade e a carga do veículo, por isso o resultado é uma estimativa.

## Entendendo os termos

- **Distância (km):** total de quilômetros que será percorrido na viagem.
- **Consumo do veículo (km/litro):** média de quilômetros que o veículo percorre com cada litro de combustível. Quanto maior o número, mais econômico é o veículo.
- **Preço por litro (R$):** valor cobrado por cada litro de combustível no posto, em reais.
- **Litros necessários:** quantidade de combustível que será gasta para percorrer a distância informada.
- **Custo:** valor total estimado em reais para abastecer o veículo durante a viagem.

## Fórmula do cálculo de combustível

Primeiro descobrimos quantos litros serão gastos e depois multiplicamos pelo preço do litro:

**Litros = distância ÷ consumo**

**Custo = litros × preço por litro**

## Exemplo resolvido

Uma viagem de 350 km será feita em um carro que faz 12 km/litro, com a gasolina a R$ 5,89 por litro. Qual é o custo estimado?

1. Identifique os dados: distância = 350 km, consumo = 12 km/litro e preço = R$ 5,89.
2. Calcule os litros: 350 ÷ 12 = 29,17 litros (aproximadamente).
3. Calcule o custo: 29,17 × 5,89 = R$ 171,79 (aproximadamente, usando o valor exato dos litros).

**Resposta:** o gasto estimado de combustível é de cerca de **R$ 171,79**.
