---
title: "Calculadora da Área do Círculo"
seoTitle: "Calculadora da Área do Círculo"
description: "Calculadora da Área do Círculo: informe as medidas e veja o resultado na hora, com a fórmula e um exemplo resolvido."
summary: "Calcule a área do círculo com a fórmula."
date: 2026-10-20
draft: false
category: "matematica"
tags: ["área", "geometria", "calculadora", "matemática"]
keywords: ["calculadora da área do círculo", "calculadora da área do círculo online", "área", "geometria", "calculadora"]
---

<!-- INI SUDAH DIKERJAKAN -->

Calcule a área de um círculo informando o **raio** ou o **diâmetro**. Escolha a fórmula, digite a medida, selecione a unidade e o número de casas decimais, e o resultado aparece na hora.

<div id="calc-area-circulo" class="calc-box">
  <fieldset>
    <legend>Fórmula</legend>
    <label><input type="radio" name="formula" value="raio" checked> Pelo <strong>raio</strong> (S = π × r²)</label>
    <label><input type="radio" name="formula" value="diametro"> Pelo <strong>diâmetro</strong> (S = π × d² ÷ 4)</label>
  </fieldset>

  <p>
    <label for="medida" id="rotulo-medida">Digite o raio:</label><br>
    <input type="number" id="medida" min="0" step="any" inputmode="decimal" placeholder="Ex.: 5">
  </p>

  <p>
    <label for="unidade">Unidade:</label><br>
    <select id="unidade">
      <option value="km">km (quilômetros)</option>
      <option value="m" selected>m (metros)</option>
      <option value="cm">cm (centímetros)</option>
      <option value="mm">mm (milímetros)</option>
    </select>
  </p>

  <p>
    <label for="casas">Casas decimais:</label><br>
    <select id="casas">
      <option value="0">Nenhuma</option>
      <option value="1">1</option>
      <option value="2" selected>2</option>
      <option value="3">3</option>
      <option value="4">4</option>
      <option value="5">5</option>
      <option value="6">6</option>
      <option value="7">7</option>
      <option value="8">8</option>
      <option value="9">9</option>
      <option value="10">10</option>
    </select>
  </p>

  <p>
    <button type="button" id="btn-calcular">Calcular área</button>
    <button type="button" id="btn-limpar">Limpar</button>
  </p>

  <p><strong>Resposta:</strong></p>
  <p id="resposta" aria-live="polite">—</p>
</div>

<script>
(function () {
  var radios = document.querySelectorAll('#calc-area-circulo input[name="formula"]');
  var rotulo = document.getElementById('rotulo-medida');
  var medida = document.getElementById('medida');
  var unidade = document.getElementById('unidade');
  var casas = document.getElementById('casas');
  var resposta = document.getElementById('resposta');

  function formulaAtual() {
    for (var i = 0; i < radios.length; i++) {
      if (radios[i].checked) return radios[i].value;
    }
    return 'raio';
  }

  function atualizarRotulo() {
    rotulo.textContent = formulaAtual() === 'raio' ? 'Digite o raio:' : 'Digite o diâmetro:';
  }

  function calcular() {
    var valor = parseFloat(String(medida.value).replace(',', '.'));
    if (isNaN(valor) || valor < 0) {
      resposta.textContent = 'Informe um valor válido (número maior ou igual a zero).';
      return;
    }
    var area = formulaAtual() === 'raio'
      ? Math.PI * valor * valor
      : (Math.PI * valor * valor) / 4;
    var texto = area.toLocaleString('pt-BR', {
      minimumFractionDigits: parseInt(casas.value, 10),
      maximumFractionDigits: parseInt(casas.value, 10)
    });
    resposta.innerHTML = texto + ' ' + unidade.value + '<sup>2</sup>';
  }

  function limpar() {
    medida.value = '';
    resposta.textContent = '—';
    medida.focus();
  }

  for (var i = 0; i < radios.length; i++) radios[i].addEventListener('change', atualizarRotulo);
  document.getElementById('btn-calcular').addEventListener('click', calcular);
  document.getElementById('btn-limpar').addEventListener('click', limpar);
  medida.addEventListener('keydown', function (e) { if (e.key === 'Enter') calcular(); });
  atualizarRotulo();
})();
</script>

## Como usar a calculadora

1. **Escolha a fórmula:** selecione "Pelo raio" se você conhece a distância do centro até a borda do círculo, ou "Pelo diâmetro" se conhece a medida que atravessa o círculo de ponta a ponta.
2. **Digite a medida:** informe o valor do raio ou do diâmetro (conforme a fórmula escolhida). Pode usar números decimais, como `2,5` ou `2.5`.
3. **Selecione a unidade:** escolha km, m, cm ou mm. A área será exibida na mesma unidade, elevada ao quadrado.
4. **Defina as casas decimais:** escolha de "Nenhuma" até 10 casas para o arredondamento do resultado.
5. **Clique em "Calcular área":** o resultado aparece no campo "Resposta". Use "Limpar" para começar um novo cálculo.

## Fórmulas

- **Pelo raio:** S = π × r²
- **Pelo diâmetro:** S = (π × d²) ÷ 4

As duas fórmulas dão o mesmo resultado, pois o raio é a metade do diâmetro (r = d ÷ 2).

## Significado dos termos

- **Círculo:** região plana limitada por uma circunferência, ou seja, toda a superfície dentro da borda.
- **Raio (r):** distância do centro do círculo até qualquer ponto da borda. É igual à metade do diâmetro.
- **Diâmetro (d):** segmento que passa pelo centro e liga dois pontos opostos da borda. É igual ao dobro do raio.
- **Área (S):** medida da superfície ocupada pelo círculo, expressa em unidades quadradas (m², cm² etc.).
- **π (pi):** constante matemática que representa a razão entre o comprimento da circunferência e o seu diâmetro. Vale aproximadamente 3,1415926535898.
- **Unidade:** padrão de medida usado na entrada (km, m, cm ou mm). A área sai na mesma unidade ao quadrado.
- **Casas decimais:** quantidade de dígitos mostrados depois da vírgula no resultado.

## Exemplo resolvido

Qual é a área de um círculo com **raio de 5 m**?

- S = π × r²
- S = 3,14159 × 5²
- S = 3,14159 × 25
- **S ≈ 78,54 m²**

Pelo diâmetro, o mesmo círculo tem d = 10 m: S = (π × 10²) ÷ 4 = (3,14159 × 100) ÷ 4 ≈ **78,54 m²**.