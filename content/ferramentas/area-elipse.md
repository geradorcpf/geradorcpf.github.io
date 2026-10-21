---
title: "Calculadora da Área da Elipse"
seoTitle: "Calculadora da Área da Elipse"
description: "Calculadora da Área da Elipse: informe as medidas e veja o resultado na hora, com a fórmula e um exemplo resolvido."
summary: "Calcule a área da elipse com a fórmula."
date: 2026-10-20
draft: false
category: "matematica"
tags: ["área", "geometria", "calculadora", "matemática"]
keywords: ["calculadora da área da elipse", "calculadora da área da elipse online", "área", "geometria", "calculadora"]
---
<!-- INI SUDAH DIKERJAKAN -->

## Calcule a área da elipse

Basta digitar os semi eixos maior e menor da elipse e depois clicar em "Calcular Área".

<div id="calc-elipse" style="max-width:480px;padding:16px;border:1px solid #d0d7de;border-radius:8px;font-family:inherit;">
  <form id="form-elipse" novalidate>
    <div style="margin-bottom:12px;">
      <label for="semi-eixo-maior" style="display:block;font-weight:600;margin-bottom:4px;">Semi Eixo Maior (a)</label>
      <input id="semi-eixo-maior" type="text" inputmode="decimal" autocomplete="off" placeholder="Ex.: 5" style="width:100%;padding:8px;border:1px solid #b0b7bf;border-radius:4px;box-sizing:border-box;">
    </div>
    <div style="margin-bottom:12px;">
      <label for="semi-eixo-menor" style="display:block;font-weight:600;margin-bottom:4px;">Semi Eixo Menor (b)</label>
      <input id="semi-eixo-menor" type="text" inputmode="decimal" autocomplete="off" placeholder="Ex.: 3" style="width:100%;padding:8px;border:1px solid #b0b7bf;border-radius:4px;box-sizing:border-box;">
    </div>
    <button type="submit" style="padding:10px 18px;border:0;border-radius:4px;background:#0b6bcb;color:#fff;font-weight:600;cursor:pointer;">Calcular Área</button>
    <button type="button" id="limpar-elipse" style="padding:10px 18px;border:1px solid #b0b7bf;border-radius:4px;background:transparent;color:inherit;cursor:pointer;margin-left:8px;">Limpar</button>
  </form>
  <p style="margin:16px 0 4px;font-weight:600;">Resposta:</p>
  <div id="resposta-elipse" role="status" aria-live="polite" style="min-height:1.5em;"></div>
</div>

<script>
(function () {
  var form = document.getElementById("form-elipse");
  var campoA = document.getElementById("semi-eixo-maior");
  var campoB = document.getElementById("semi-eixo-menor");
  var resposta = document.getElementById("resposta-elipse");
  var limpar = document.getElementById("limpar-elipse");
  if (!form) return;

  function lerNumero(texto) {
    var valor = String(texto).trim().replace(/\s+/g, "").replace(",", ".");
    if (valor === "" || !/^\d*\.?\d+$|^\d+\.$/.test(valor)) return NaN;
    return parseFloat(valor);
  }

  function formatar(numero) {
    return numero.toLocaleString("pt-BR", { maximumFractionDigits: 4 });
  }

  function mostrarErro(mensagem) {
    resposta.style.color = "#c62828";
    resposta.textContent = mensagem;
  }

  form.addEventListener("submit", function (evento) {
    evento.preventDefault();
    var a = lerNumero(campoA.value);
    var b = lerNumero(campoB.value);

    if (isNaN(a) || isNaN(b)) {
      mostrarErro("Informe valores numéricos válidos nos dois semi eixos.");
      return;
    }
    if (a <= 0 || b <= 0) {
      mostrarErro("Os semi eixos devem ser maiores que zero.");
      return;
    }

    var area = Math.PI * a * b;
    resposta.style.color = "inherit";
    resposta.innerHTML =
      "<strong>A = " + formatar(area) + "</strong> (unidade de medida ao quadrado)" +
      "<br><small>A = π × " + formatar(a) + " × " + formatar(b) + "</small>";
  });

  limpar.addEventListener("click", function () {
    campoA.value = "";
    campoB.value = "";
    resposta.textContent = "";
    campoA.focus();
  });
})();
</script>

## Como usar a calculadora

1. Digite o valor do **Semi Eixo Maior** (a) no primeiro campo.
2. Digite o valor do **Semi Eixo Menor** (b) no segundo campo.
3. Clique em **Calcular Área** para ver o resultado em **Resposta**.
4. Para fazer um novo cálculo, clique em **Limpar** e informe outros valores.

**Dicas:**

- Use ponto ou vírgula como separador decimal (por exemplo, `2,5` ou `2.5`).
- Os dois semi eixos devem estar na mesma unidade de medida (cm, m, km etc.).
- O resultado sai na unidade correspondente ao quadrado (cm², m², km² etc.).
- Os valores precisam ser maiores que zero.

## Significado dos termos

- **Elipse:** curva fechada e achatada, parecida com um círculo "esticado". Todos os seus pontos têm a mesma soma de distâncias até dois pontos fixos, chamados focos.
- **Semi Eixo Maior (a):** metade do maior diâmetro da elipse, ou seja, a distância do centro até o ponto mais afastado da curva.
- **Semi Eixo Menor (b):** metade do menor diâmetro da elipse, ou seja, a distância do centro até o ponto mais próximo da curva.
- **Área (A):** medida da região interna delimitada pela elipse, expressa em unidades quadradas.
- **π (pi):** constante matemática aproximadamente igual a 3,14159, que relaciona a circunferência de um círculo ao seu diâmetro.
- **Resposta:** campo onde a calculadora mostra a área calculada.

## Fórmula da área da elipse

A área da elipse é calculada multiplicando π pelos dois semi eixos:

**A = π × a × b**

Em que:

- **A** é a área da elipse;
- **a** é o semi eixo maior;
- **b** é o semi eixo menor;
- **π** é aproximadamente 3,14159.

Quando a = b, a elipse vira um círculo de raio r e a fórmula se reduz à conhecida **A = π × r²**.

## Exemplo resolvido

Qual é a área de uma elipse com semi eixo maior de 5 cm e semi eixo menor de 3 cm?

1. Aplique a fórmula: A = π × a × b
2. Substitua os valores: A = π × 5 × 3
3. Multiplique: A = 15π
4. Use π ≈ 3,14159: A ≈ 47,1239

Portanto, a área da elipse é de aproximadamente **47,12 cm²**.