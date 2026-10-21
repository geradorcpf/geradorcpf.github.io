---
title: "Calculadora da Área da Coroa Circular"
seoTitle: "Calculadora da Área da Coroa Circular"
description: "Calculadora da Área da Coroa Circular: informe as medidas e veja o resultado na hora, com a fórmula e um exemplo resolvido."
summary: "Calcule a área da coroa circular com a fórmula."
date: 2026-10-20
draft: false
category: "matematica"
tags: ["área", "geometria", "calculadora", "matemática"]
keywords: ["calculadora da área da coroa circular", "calculadora da área da coroa circular online", "área", "geometria", "calculadora"]
---

<!-- INI SUDAH DIKERJAKAN -->

Use esta calculadora para descobrir a área de uma coroa circular, a região em formato de anel que fica entre dois círculos com o mesmo centro. Basta informar o raio maior e o raio menor e o resultado aparece na hora.

## Calculadora

<div class="calc-coroa">
<style>
.calc-coroa { max-width: 420px; padding: 1.25rem; border: 1px solid #d0d7de; border-radius: 12px; }
.calc-coroa label { display: block; margin-bottom: .75rem; font-weight: 600; }
.calc-coroa input { display: block; width: 100%; margin-top: .35rem; padding: .6rem .75rem; font-size: 1rem; border: 1px solid #b0b8c1; border-radius: 8px; box-sizing: border-box; }
.calc-coroa .acoes { display: flex; gap: .5rem; margin-top: .5rem; }
.calc-coroa button { padding: .6rem 1.1rem; font-size: 1rem; border: 0; border-radius: 8px; cursor: pointer; background: #2563eb; color: #fff; }
.calc-coroa button.secundario { background: #e5e7eb; color: #111; }
.calc-coroa .resposta { margin-top: 1rem; font-size: 1.1rem; min-height: 1.5rem; }
.calc-coroa .resposta.erro { color: #b91c1c; }
</style>
<form id="form-coroa" novalidate>
<label for="raio-maior">Raio Maior (R)
<input type="text" id="raio-maior" inputmode="decimal" placeholder="Ex.: 10" autocomplete="off">
</label>
<label for="raio-menor">Raio Menor (r)
<input type="text" id="raio-menor" inputmode="decimal" placeholder="Ex.: 6" autocomplete="off">
</label>
<div class="acoes">
<button type="submit">Calcular Área</button>
<button type="button" class="secundario" id="limpar-coroa">Limpar</button>
</div>
</form>
<div class="resposta" id="resposta-coroa" aria-live="polite"></div>
<script>
(function () {
  var form = document.getElementById('form-coroa');
  var maior = document.getElementById('raio-maior');
  var menor = document.getElementById('raio-menor');
  var saida = document.getElementById('resposta-coroa');
  var limpar = document.getElementById('limpar-coroa');
  function ler(campo) {
    var texto = campo.value.trim().replace(',', '.');
    if (texto === '') return NaN;
    return Number(texto);
  }
  function mostrar(msg, erro) {
    saida.textContent = msg;
    saida.className = 'resposta' + (erro ? ' erro' : '');
  }
  form.addEventListener('submit', function (e) {
    e.preventDefault();
    var R = ler(maior);
    var r = ler(menor);
    if (isNaN(R) || isNaN(r)) {
      mostrar('Informe valores numéricos para os dois raios.', true);
      return;
    }
    if (R <= 0 || r < 0) {
      mostrar('Os raios devem ser maiores que zero.', true);
      return;
    }
    if (R <= r) {
      mostrar('O raio maior deve ser maior que o raio menor.', true);
      return;
    }
    var area = Math.PI * (R * R - r * r);
    var formatado = area.toLocaleString('pt-BR', { minimumFractionDigits: 2, maximumFractionDigits: 2 });
    mostrar('Resposta: ' + formatado + ' unidades quadradas', false);
  });
  limpar.addEventListener('click', function () {
    maior.value = '';
    menor.value = '';
    mostrar('', false);
    maior.focus();
  });
})();
</script>
</div>

## Como usar a calculadora

1. Digite o valor do **Raio Maior (R)**, que é o raio do círculo externo.
2. Digite o valor do **Raio Menor (r)**, que é o raio do círculo interno.
3. Clique em **Calcular Área** para ver a resposta.
4. Para fazer um novo cálculo, clique em **Limpar**.

Dicas:

- Use a mesma unidade de medida nos dois campos (cm, m, etc.). A resposta sai na unidade ao quadrado (cm², m², etc.).
- Você pode usar ponto ou vírgula como separador decimal.
- O raio maior precisa ser maior que o raio menor. Caso contrário, a calculadora mostra um aviso.
- Se você só tem o diâmetro, divida-o por 2 para obter o raio.

## Fórmula

A área da coroa circular é a área do círculo maior menos a área do círculo menor:

**A = π × (R² − r²)**

## Significado de cada termo

- **Coroa circular:** figura plana em forma de anel, limitada por dois círculos concêntricos.
- **Círculo concêntrico:** círculo que compartilha o mesmo centro com outro círculo.
- **Raio maior (R):** distância do centro até a borda do círculo externo.
- **Raio menor (r):** distância do centro até a borda do círculo interno, ou seja, o "buraco" do anel.
- **π (pi):** constante matemática de valor aproximado 3,14159, que relaciona o raio de um círculo à sua área.
- **Área (A):** medida da superfície da coroa, expressa em unidades quadradas.
- **Largura da coroa (R − r):** espessura do anel, a diferença entre os dois raios.

## Exemplo resolvido

Uma coroa circular tem raio maior R = 10 cm e raio menor r = 6 cm.

1. Elevar os raios ao quadrado: R² = 100 e r² = 36.
2. Subtrair: 100 − 36 = 64.
3. Multiplicar por π: A = π × 64 ≈ 201,06.

**Resposta:** a área da coroa circular é de aproximadamente **201,06 cm²**.