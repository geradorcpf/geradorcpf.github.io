---
title: "Calculadora da Área do Pentágono"
seoTitle: "Calculadora da Área do Pentágono"
description: "Calculadora da Área do Pentágono: informe as medidas e veja o resultado na hora, com a fórmula e um exemplo resolvido."
summary: "Calcule a área do pentágono com a fórmula."
date: 2026-10-20
draft: false
category: "matematica"
tags: ["área", "geometria", "calculadora", "matemática"]
keywords: ["calculadora da área do pentágono", "calculadora da área do pentágono online", "área", "geometria", "calculadora"]
---
<!-- INI SUDAH DIKERJAKAN -->

Basta digitar o lado do pentágono regular abaixo e clicar em "Calcular Área". O resultado aparece na hora, junto com o perímetro e o apótema.

<form id="calc-pentagono" novalidate style="max-width:420px;margin:1.5rem 0;padding:1.25rem;border:1px solid #d0d7de;border-radius:8px;">
  <label for="lado" style="display:block;font-weight:600;margin-bottom:.4rem;">Lado</label>
  <input type="number" id="lado" name="lado" min="0" step="any" inputmode="decimal" placeholder="Ex.: 5" style="width:100%;padding:.6rem;border:1px solid #b6bec6;border-radius:6px;box-sizing:border-box;">
  <div style="margin-top:.9rem;display:flex;gap:.6rem;">
    <button type="submit" style="padding:.6rem 1.1rem;border:0;border-radius:6px;background:#0b5fff;color:#fff;font-weight:600;cursor:pointer;">Calcular Área</button>
    <button type="reset" id="limpar" style="padding:.6rem 1.1rem;border:1px solid #b6bec6;border-radius:6px;background:#fff;cursor:pointer;">Limpar</button>
  </div>
  <p style="margin:1rem 0 0;font-weight:600;">Resposta:</p>
  <div id="resposta" aria-live="polite" style="min-height:3.2rem;margin-top:.3rem;"></div>
</form>

<script>
(function () {
  var form = document.getElementById("calc-pentagono");
  var campo = document.getElementById("lado");
  var saida = document.getElementById("resposta");
  var fmt = new Intl.NumberFormat("pt-BR", { maximumFractionDigits: 4 });

  form.addEventListener("submit", function (e) {
    e.preventDefault();
    var lado = parseFloat(String(campo.value).replace(",", "."));
    if (!isFinite(lado) || lado <= 0) {
      saida.textContent = "Informe um valor positivo para o lado.";
      return;
    }
    var area = (Math.sqrt(5 * (5 + 2 * Math.sqrt(5))) / 4) * lado * lado;
    var perimetro = 5 * lado;
    var apotema = lado / (2 * Math.tan(Math.PI / 5));
    saida.innerHTML =
      "<strong>Área:</strong> " + fmt.format(area) + " unidades²<br>" +
      "<strong>Perímetro:</strong> " + fmt.format(perimetro) + " unidades<br>" +
      "<strong>Apótema:</strong> " + fmt.format(apotema) + " unidades";
  });

  form.addEventListener("reset", function () {
    saida.textContent = "";
  });
})();
</script>

## Como usar a calculadora

1. Digite a medida do **lado** do pentágono regular no campo "Lado". Use ponto ou vírgula para casas decimais.
2. Clique em **Calcular Área**.
3. Veja a **Resposta**: a área, o perímetro e o apótema do pentágono.
4. Para fazer um novo cálculo, clique em **Limpar** ou simplesmente digite outro valor.

A unidade do resultado acompanha a unidade que você usou no lado. Se o lado estiver em centímetros, a área sai em cm² e o perímetro e o apótema saem em cm.

## Fórmula da área do pentágono regular

```
A = (1/4) · √(5 · (5 + 2√5)) · l²  ≈  1,7205 · l²
```

Onde **l** é a medida do lado. Também é possível chegar ao mesmo valor pela fórmula geral dos polígonos regulares:

```
A = (P · a) / 2
```

Onde **P** é o perímetro (5 · l) e **a** é o apótema.

## Exemplo resolvido

Qual é a área de um pentágono regular com lado de 5 cm?

1. Aplique a fórmula: A = 1,7205 · l²
2. Substitua o lado: A = 1,7205 · 5²
3. Calcule o quadrado: A = 1,7205 · 25
4. Resultado: **A ≈ 43,01 cm²**

Nesse caso, o perímetro é 5 · 5 = 25 cm e o apótema é aproximadamente 3,44 cm.

## Significado dos termos

- **Pentágono:** polígono com 5 lados e 5 ângulos.
- **Pentágono regular:** pentágono com os 5 lados de mesmo comprimento e os 5 ângulos iguais (108° cada). É o tipo calculado por esta ferramenta.
- **Lado (l):** cada um dos segmentos que formam o contorno do pentágono. É o único dado necessário para o cálculo.
- **Área (A):** medida da superfície interna do pentágono, expressa em unidades quadradas (cm², m² etc.).
- **Perímetro (P):** soma dos comprimentos de todos os lados. No pentágono regular, P = 5 · l.
- **Apótema (a):** distância do centro do pentágono até o ponto médio de um dos lados, formando um ângulo reto com ele. No pentágono regular, a = l / (2 · tan 36°) ≈ 0,6882 · l.
- **Unidade de medida:** padrão usado para medir o comprimento do lado. A área sempre aparece elevada ao quadrado (por exemplo, cm²).
- **Raiz quadrada (√):** operação usada na fórmula, que dá o número que multiplicado por ele mesmo resulta no valor original.