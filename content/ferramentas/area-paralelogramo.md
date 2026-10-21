---
title: "Calculadora da Área do Paralelogramo"
seoTitle: "Calculadora da Área do Paralelogramo"
description: "Calculadora da Área do Paralelogramo: informe as medidas e veja o resultado na hora, com a fórmula e um exemplo resolvido."
summary: "Calcule a área do paralelogramo com a fórmula."
date: 2026-10-20
draft: false
category: "matematica"
tags: ["área", "geometria", "calculadora", "matemática"]
keywords: ["calculadora da área do paralelogramo", "calculadora da área do paralelogramo online", "área", "geometria", "calculadora"]
---
<!-- INI SUDAH DIKERJAKAN -->

Basta digitar a base e a altura do paralelogramo abaixo e depois clicar em "Calcular Área".

<form id="calc-paralelogramo" novalidate style="max-width:420px;margin:1.5rem 0;">
  <div style="margin-bottom:1rem;">
    <label for="pg-base" style="display:block;font-weight:600;margin-bottom:.25rem;">Base</label>
    <input type="text" id="pg-base" inputmode="decimal" autocomplete="off" placeholder="Ex.: 8" style="width:100%;padding:.6rem;font-size:1rem;box-sizing:border-box;">
  </div>
  <div style="margin-bottom:1rem;">
    <label for="pg-altura" style="display:block;font-weight:600;margin-bottom:.25rem;">Altura</label>
    <input type="text" id="pg-altura" inputmode="decimal" autocomplete="off" placeholder="Ex.: 5" style="width:100%;padding:.6rem;font-size:1rem;box-sizing:border-box;">
  </div>
  <button type="submit" style="padding:.6rem 1.2rem;font-size:1rem;cursor:pointer;">Calcular Área</button>
  <button type="reset" id="pg-limpar" style="padding:.6rem 1.2rem;font-size:1rem;cursor:pointer;margin-left:.5rem;">Limpar</button>
  <p style="margin-top:1rem;font-size:1.1rem;"><strong>Resposta:</strong> <span id="pg-resposta" aria-live="polite"></span></p>
</form>

<script>
(function () {
  var form = document.getElementById("calc-paralelogramo");
  var baseEl = document.getElementById("pg-base");
  var alturaEl = document.getElementById("pg-altura");
  var respostaEl = document.getElementById("pg-resposta");

  function toNumber(value) {
    return parseFloat(String(value).trim().replace(",", "."));
  }

  form.addEventListener("submit", function (e) {
    e.preventDefault();
    var base = toNumber(baseEl.value);
    var altura = toNumber(alturaEl.value);

    if (!isFinite(base) || !isFinite(altura) || base <= 0 || altura <= 0) {
      respostaEl.textContent = "Informe valores numéricos maiores que zero para a base e a altura.";
      return;
    }

    var area = base * altura;
    respostaEl.textContent = area.toLocaleString("pt-BR", { maximumFractionDigits: 4 });
  });

  form.addEventListener("reset", function () {
    respostaEl.textContent = "";
  });
})();
</script>

## Como usar a calculadora

1. Digite a medida da **base** do paralelogramo no campo "Base".
2. Digite a medida da **altura** no campo "Altura". Use a mesma unidade de medida nos dois campos (por exemplo, centímetros).
3. Clique em **Calcular Área**.
4. O valor aparece ao lado de "Resposta:", na unidade escolhida elevada ao quadrado (cm², m² etc.).
5. Para fazer um novo cálculo, clique em **Limpar** e informe outros valores.

Você pode usar números decimais, com vírgula ou ponto (por exemplo, `7,5` ou `7.5`).

## Fórmula da área do paralelogramo

A área é o produto da base pela altura:

**Área = base × altura**

### Exemplo resolvido

Um paralelogramo tem base de 8 cm e altura de 5 cm.

- Área = 8 × 5
- Área = **40 cm²**

## Significado dos termos

- **Paralelogramo:** quadrilátero com dois pares de lados opostos paralelos e de mesmo comprimento. Retângulos, losangos e quadrados são casos particulares.
- **Base:** um dos lados do paralelogramo, normalmente o que está na parte inferior da figura.
- **Altura:** distância perpendicular entre a base e o lado oposto a ela. Não é a medida do lado inclinado.
- **Área:** medida da superfície ocupada pela figura, expressa em unidades quadradas (cm², m², km² etc.).
- **Resposta:** resultado do cálculo, exibido depois que você clica em "Calcular Área".
- **Unidade de medida:** padrão usado para medir os lados (cm, m etc.). Base e altura precisam estar na mesma unidade para o resultado ser correto.