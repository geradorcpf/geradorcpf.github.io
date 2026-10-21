---
title: "Calculadora da Área do Polígono Regular"
seoTitle: "Calculadora da Área do Polígono Regular"
description: "Calculadora da Área do Polígono Regular: informe as medidas e veja o resultado na hora, com a fórmula e um exemplo resolvido."
summary: "Calcule a área do polígono regular com a fórmula."
date: 2026-10-20
draft: false
category: "matematica"
tags: ["área", "geometria", "calculadora", "matemática"]
keywords: ["calculadora da área do polígono regular", "calculadora da área do polígono regular online", "área", "geometria", "calculadora"]
---
<!-- INI SUDAH DIKERJAKAN -->

Basta digitar a quantidade de lados e o tamanho do lado do polígono abaixo e clicar em "Calcular Área". O resultado aparece na hora.

<form id="calc-poligono" novalidate>
  <p>
    <label for="qtd-lados">Quantidade de Lados</label><br>
    <input type="number" id="qtd-lados" min="3" step="1" placeholder="Ex.: 6" inputmode="numeric">
  </p>
  <p>
    <label for="tam-lado">Lado</label><br>
    <input type="number" id="tam-lado" min="0" step="any" placeholder="Ex.: 6" inputmode="decimal">
  </p>
  <p>
    <button type="submit">Calcular Área</button>
    <button type="reset" id="limpar-poligono">Limpar</button>
  </p>
  <p><strong>Resposta:</strong> <span id="resposta-poligono" aria-live="polite"></span></p>
</form>

<script>
(function () {
  var form = document.getElementById('calc-poligono');
  var resposta = document.getElementById('resposta-poligono');

  form.addEventListener('submit', function (e) {
    e.preventDefault();
    var n = parseFloat(document.getElementById('qtd-lados').value.replace(',', '.'));
    var l = parseFloat(document.getElementById('tam-lado').value.replace(',', '.'));

    if (!Number.isInteger(n) || n < 3) {
      resposta.textContent = 'Informe uma quantidade de lados inteira, maior ou igual a 3.';
      return;
    }
    if (isNaN(l) || l <= 0) {
      resposta.textContent = 'Informe um valor de lado maior que zero.';
      return;
    }

    var area = (n * l * l) / (4 * Math.tan(Math.PI / n));
    resposta.textContent = area.toLocaleString('pt-BR', {
      minimumFractionDigits: 2,
      maximumFractionDigits: 4
    }) + ' unidades de área (mesma unidade do lado, ao quadrado)';
  });

  form.addEventListener('reset', function () {
    resposta.textContent = '';
  });
})();
</script>

## Como usar a calculadora

1. Digite a **Quantidade de Lados** do polígono no primeiro campo. Use um número inteiro maior ou igual a 3 (3 = triângulo, 4 = quadrado, 5 = pentágono, 6 = hexágono e assim por diante).
2. Digite o tamanho do **Lado** no segundo campo. Todos os lados de um polígono regular têm a mesma medida. Você pode usar números decimais (por exemplo, 4,5).
3. Clique em **Calcular Área**.
4. Veja o valor em **Resposta**. Ele está na unidade do lado elevada ao quadrado: se o lado foi informado em centímetros, a área sai em cm²; se foi em metros, em m².
5. Para fazer um novo cálculo, clique em **Limpar** ou simplesmente altere os valores e calcule de novo.

## Significado de cada termo

- **Polígono regular:** figura plana fechada com todos os lados do mesmo tamanho e todos os ângulos internos iguais.
- **Quantidade de lados (n):** número de lados do polígono. Define o tipo da figura e deve ser no mínimo 3.
- **Lado (l):** medida de cada um dos lados do polígono.
- **Área (A):** medida da superfície ocupada pelo polígono, expressa em unidades quadradas (cm², m² etc.).
- **Apótema (a):** segmento que liga o centro do polígono ao ponto médio de um dos lados, formando ângulo reto com ele. Pode ser usado em outra fórmula: A = (perímetro × apótema) / 2.
- **Perímetro (P):** soma de todos os lados do polígono, ou seja, P = n × l.
- **Tangente (tan):** função trigonométrica usada na fórmula para relacionar o ângulo central com o apótema.
- **π (pi):** constante matemática de valor aproximado 3,14159. Na fórmula, π/n em radianos corresponde a 180°/n.

## Fórmula da área do polígono regular

A calculadora usa a fórmula:

**A = (n × l²) / (4 × tan(π / n))**

onde **n** é a quantidade de lados, **l** é a medida do lado e **tan** é a tangente, com o ângulo em radianos (π/n radianos equivalem a 180°/n).

## Exemplo resolvido

Qual é a área de um hexágono regular com lado de 6 cm?

- Quantidade de lados: n = 6
- Lado: l = 6 cm

1. Calcule l²: 6² = 36
2. Calcule n × l²: 6 × 36 = 216
3. Calcule o ângulo: π / 6 = 30°, e tan(30°) ≈ 0,57735
4. Calcule o denominador: 4 × 0,57735 ≈ 2,3094
5. Divida: A = 216 / 2,3094 ≈ **93,53 cm²**

Portanto, a área do hexágono regular é de aproximadamente **93,53 cm²**.