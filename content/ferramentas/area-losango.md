---
title: "Calculadora da Área do Losango"
seoTitle: "Calculadora da Área do Losango"
description: "Calculadora da Área do Losango: informe as medidas e veja o resultado na hora, com a fórmula e um exemplo resolvido."
summary: "Calcule a área do losango com a fórmula."
date: 2026-10-20
draft: false
category: "matematica"
tags: ["área", "geometria", "calculadora", "matemática"]
keywords: ["calculadora da área do losango", "calculadora da área do losango online", "área", "geometria", "calculadora"]
---
<!-- INI SUDAH DIKERJAKAN -->

Basta digitar as diagonais do losango abaixo e clicar em "Calcular Área".

<form id="losango-form" novalidate style="display:grid;gap:12px;max-width:420px;margin:16px 0;">
  <label for="losango-d1">Diagonal 1
    <input type="text" inputmode="decimal" id="losango-d1" placeholder="Ex.: 10" autocomplete="off" style="display:block;width:100%;padding:8px;margin-top:4px;box-sizing:border-box;">
  </label>
  <label for="losango-d2">Diagonal 2
    <input type="text" inputmode="decimal" id="losango-d2" placeholder="Ex.: 6" autocomplete="off" style="display:block;width:100%;padding:8px;margin-top:4px;box-sizing:border-box;">
  </label>
  <div style="display:flex;gap:8px;">
    <button type="submit" style="padding:8px 16px;cursor:pointer;">Calcular Área</button>
    <button type="reset" id="losango-limpar" style="padding:8px 16px;cursor:pointer;">Limpar</button>
  </div>
  <p id="losango-resposta" role="status" aria-live="polite" style="margin:0;font-weight:bold;"><strong>Resposta:</strong> <span id="losango-resultado"></span></p>
</form>

<script>
(function () {
  var form = document.getElementById("losango-form");
  var d1 = document.getElementById("losango-d1");
  var d2 = document.getElementById("losango-d2");
  var out = document.getElementById("losango-resultado");

  function lerNumero(valor) {
    var limpo = String(valor).trim().replace(/\s/g, "").replace(",", ".");
    if (limpo === "" || isNaN(limpo)) return NaN;
    return parseFloat(limpo);
  }

  form.addEventListener("submit", function (e) {
    e.preventDefault();
    var a = lerNumero(d1.value);
    var b = lerNumero(d2.value);
    if (isNaN(a) || isNaN(b) || a <= 0 || b <= 0) {
      out.textContent = "informe duas diagonais com valores numéricos maiores que zero.";
      return;
    }
    var area = (a * b) / 2;
    out.textContent = area.toLocaleString("pt-BR", { maximumFractionDigits: 4 });
  });

  form.addEventListener("reset", function () {
    out.textContent = "";
  });
})();
</script>

## Como usar a calculadora

1. Digite o valor da **Diagonal 1** (qualquer uma das duas diagonais do losango).
2. Digite o valor da **Diagonal 2** (a outra diagonal).
3. Clique em **Calcular Área**.
4. O resultado aparece ao lado de **Resposta:**.
5. Para fazer um novo cálculo, clique em **Limpar** e informe os novos valores.

**Dicas:**

- Use ponto ou vírgula como separador decimal (por exemplo, `7,5` ou `7.5`).
- As duas diagonais devem estar na **mesma unidade de medida** (cm, m, etc.).
- O resultado sai na unidade ao quadrado: diagonais em cm resultam em cm², em m resultam em m².
- Os campos aceitam apenas números maiores que zero.

## Fórmula da área do losango

A área do losango é o produto das duas diagonais dividido por 2:

**A = (D × d) ÷ 2**

### Exemplo resolvido

Um losango tem diagonais de 10 cm e 6 cm:

- A = (10 × 6) ÷ 2
- A = 60 ÷ 2
- **A = 30 cm²**

## Glossário: o que significa cada termo

- **Losango:** quadrilátero com os quatro lados de mesma medida. Também é chamado de rombo.
- **Diagonal:** segmento de reta que liga dois vértices opostos da figura. O losango tem duas diagonais.
- **Diagonal maior (D):** a mais longa das duas diagonais.
- **Diagonal menor (d):** a mais curta das duas diagonais.
- **Vértice:** ponto de encontro de dois lados, ou seja, cada "canto" do losango.
- **Área (A):** medida da superfície ocupada pela figura, expressa em unidades quadradas (cm², m² etc.).
- **Perpendiculares:** as diagonais do losango se cruzam formando ângulos de 90°.
- **Ponto médio:** as diagonais se cortam exatamente ao meio, dividindo o losango em quatro triângulos retângulos iguais.
- **Unidade de medida:** padrão usado para medir comprimentos e áreas. Use a mesma unidade nas duas diagonais.