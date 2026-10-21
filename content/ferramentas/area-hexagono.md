---
title: "Calculadora da Área do Hexágono"
seoTitle: "Calculadora da Área do Hexágono"
description: "Calculadora da Área do Hexágono: informe as medidas e veja o resultado na hora, com a fórmula e um exemplo resolvido."
summary: "Calcule a área do hexágono com a fórmula."
date: 2026-10-20
draft: false
category: "matematica"
tags: ["área", "geometria", "calculadora", "matemática"]
keywords: ["calculadora da área do hexágono", "calculadora da área do hexágono online", "área", "geometria", "calculadora"]
---

<!-- INI SUDAH DIKERJAKAN -->

Basta digitar o lado do hexágono regular abaixo e clicar em "Calcular Área" para ver o resultado na hora.

<div id="calc-area-hexagono" style="max-width:420px;padding:16px;border:1px solid #ddd;border-radius:8px;">
  <label for="hex-lado" style="display:block;font-weight:600;margin-bottom:6px;">Lado</label>
  <input id="hex-lado" type="text" inputmode="decimal" placeholder="Ex.: 4" style="width:100%;padding:8px;box-sizing:border-box;margin-bottom:12px;">
  <button id="hex-calcular" type="button" style="padding:8px 16px;cursor:pointer;">Calcular Área</button>
  <button id="hex-limpar" type="button" style="padding:8px 16px;cursor:pointer;margin-left:8px;">Limpar</button>
  <p id="hex-resposta" style="margin-top:14px;font-weight:600;" aria-live="polite">Resposta:</p>
</div>
<script>
(function () {
  var lado = document.getElementById('hex-lado');
  var resposta = document.getElementById('hex-resposta');
  function calcular() {
    var l = parseFloat(String(lado.value).trim().replace(',', '.'));
    if (isNaN(l) || l <= 0) {
      resposta.textContent = 'Resposta: informe um valor numérico maior que zero.';
      return;
    }
    var area = (3 * Math.sqrt(3) / 2) * l * l;
    resposta.textContent = 'Resposta: ' + area.toLocaleString('pt-BR', { maximumFractionDigits: 4 });
  }
  document.getElementById('hex-calcular').addEventListener('click', calcular);
  lado.addEventListener('keydown', function (e) { if (e.key === 'Enter') calcular(); });
  document.getElementById('hex-limpar').addEventListener('click', function () {
    lado.value = '';
    resposta.textContent = 'Resposta:';
    lado.focus();
  });
})();
</script>

## Como usar a calculadora

1. Digite a medida do **lado** do hexágono regular no campo "Lado". Pode usar ponto ou vírgula como separador decimal (ex.: `4,5`).
2. Clique em **Calcular Área** (ou pressione Enter).
3. O valor da área aparece em **Resposta**, na mesma unidade do lado elevada ao quadrado. Se o lado estiver em cm, a área será em cm².
4. Para fazer outro cálculo, clique em **Limpar** e informe um novo valor.

## Fórmula da área do hexágono regular

A = (3 × √3 / 2) × l²

Ou seja, a área é igual a 3 vezes a raiz quadrada de 3, dividido por 2 e multiplicado pelo quadrado do lado. O resultado vem do fato de um hexágono regular poder ser dividido em 6 triângulos equiláteros de lado l, cada um com área (l² × √3) / 4.

## Exemplo resolvido

Qual é a área de um hexágono regular com lado de 4 cm?

- A = (3 × √3 / 2) × 4²
- A = (3 × 1,7321 / 2) × 16
- A = 2,5981 × 16
- A ≈ **41,57 cm²**

## Significado dos termos

- **Hexágono:** polígono com 6 lados e 6 ângulos. Aqui, tratamos do hexágono regular, com todos os lados e ângulos iguais.
- **Lado (l):** medida de cada um dos segmentos que formam o contorno do hexágono. É o único dado que você precisa informar.
- **Área (A):** medida da superfície interna do hexágono, expressa em unidades quadradas (cm², m² etc.).
- **Hexágono regular:** hexágono com 6 lados de mesmo comprimento e 6 ângulos internos de 120°.
- **Triângulo equilátero:** triângulo com os 3 lados iguais. O hexágono regular é formado por 6 deles.
- **Raiz quadrada de 3 (√3):** constante matemática com valor aproximado de 1,7321, presente na fórmula.
- **Unidade de medida:** padrão usado para medir o lado (cm, m, mm...). A área sai sempre nessa mesma unidade ao quadrado.