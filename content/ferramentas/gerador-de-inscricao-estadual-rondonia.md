---
title: "Gerador de Inscrição Estadual de Rondônia (RO)"
seoTitle: "Gerador de Inscrição Estadual de Rondônia (RO)"
description: "Gerador de Inscrição Estadual de Rondônia (RO): gere números válidos para testes de software. Grátis e online."
summary: "Gere inscrições estaduais válidas para testes."
date: 2026-11-01
draft: false
category: "documentos"
tags: ["inscrição estadual", "estados", "empresas", "gerador", "dados de teste", "rondônia", "documentos"]
keywords: ["gerador de inscrição estadual de rondônia (ro)", "gerador de inscrição estadual de rondônia (ro) online", "inscrição estadual", "estados", "empresas"]
compact: true
---

Escolha se deseja a inscrição com ou sem pontuação e clique em **Gerar Inscrição Estadual**.

<div id="gerador-ie-ro" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🏢 Gerador de Inscrição Estadual de Rondônia (RO)</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Gere números válidos para testes de software.</p>
<span style="display:block;margin-bottom:8px;font-weight:600;font-size:0.95rem;">Gerar com pontuação?</span>
<div style="display:flex;gap:10px;flex-wrap:wrap;margin-bottom:20px;">
<label for="ie-pontuacao-sim" style="flex:1;min-width:120px;display:flex;align-items:center;gap:8px;padding:12px 14px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;cursor:pointer;box-sizing:border-box;"><input type="radio" id="ie-pontuacao-sim" name="ie-pontuacao" value="sim" checked style="accent-color:#4f46e5;margin:0;cursor:pointer;"> Sim</label>
<label for="ie-pontuacao-nao" style="flex:1;min-width:120px;display:flex;align-items:center;gap:8px;padding:12px 14px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;cursor:pointer;box-sizing:border-box;"><input type="radio" id="ie-pontuacao-nao" name="ie-pontuacao" value="nao" style="accent-color:#4f46e5;margin:0;cursor:pointer;"> Não</label>
</div>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="ie-gerar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Gerar Inscrição Estadual</button>
<button type="button" id="ie-copiar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Copiar</button>
</div>
<div id="ie-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="ie-resultado">clique em "Gerar Inscrição Estadual".</span></div>
</div>
<script>
(function () {
  var radSim = document.getElementById('ie-pontuacao-sim');
  var radNao = document.getElementById('ie-pontuacao-nao');
  var btnGerar = document.getElementById('ie-gerar');
  var btnCopiar = document.getElementById('ie-copiar');
  var resultado = document.getElementById('ie-resultado');
  var caixa = document.getElementById('ie-resposta');
  var pesos = [6, 5, 4, 3, 2, 9, 8, 7, 6, 5, 4, 3, 2];
  var atual = null;
  function calcularDV(digitos) {
    var soma = 0;
    pesos.forEach(function (peso, i) { soma += digitos[i] * peso; });
    var dv = 11 - (soma % 11);
    if (dv === 10 || dv === 11) { dv -= 10; }
    return dv;
  }
  function mostrar() {
    if (atual === null) { return; }
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    resultado.style.fontWeight = '700';
    resultado.style.fontSize = '1.2rem';
    resultado.style.letterSpacing = '0.5px';
    resultado.textContent = radSim.checked ? atual.formatado : atual.puro;
  }
  function gerar() {
    var digitos;
    do {
      digitos = pesos.map(function () { return Math.floor(Math.random() * 10); });
    } while (digitos.join('') === '0000000000000');
    var base = digitos.join('');
    var dv = calcularDV(digitos);
    atual = { puro: base + String(dv), formatado: base + '-' + String(dv) };
    btnCopiar.textContent = 'Copiar';
    mostrar();
  }
  function copiarFallback(texto) {
    var area = document.createElement('textarea');
    area.value = texto;
    area.style.position = 'fixed';
    area.style.opacity = '0';
    document.body.appendChild(area);
    area.select();
    try { document.execCommand('copy'); } catch (e) {}
    document.body.removeChild(area);
  }
  function copiar() {
    if (atual === null) { return; }
    var texto = radSim.checked ? atual.formatado : atual.puro;
    if (navigator.clipboard) {
      if (navigator.clipboard.writeText) {
        navigator.clipboard.writeText(texto).catch(function () { copiarFallback(texto); });
      } else { copiarFallback(texto); }
    } else { copiarFallback(texto); }
    btnCopiar.textContent = 'Copiado!';
    setTimeout(function () { btnCopiar.textContent = 'Copiar'; }, 1500);
  }
  btnGerar.addEventListener('click', gerar);
  btnCopiar.addEventListener('click', copiar);
  radSim.addEventListener('change', mostrar);
  radNao.addEventListener('change', mostrar);
})();
</script>

## Como usar o gerador

1. Em **Gerar com pontuação?**, escolha **Sim** para receber o número com hífen antes do dígito verificador (por exemplo, `0000000062521-3`) ou **Não** para receber apenas os números (por exemplo, `00000000625213`).
2. Clique em **Gerar Inscrição Estadual** para criar um novo número válido para Rondônia.
3. Clique em **Copiar** para levar o número para a área de transferência e colá-lo no seu sistema.
4. Se mudar a opção de pontuação depois de gerar, o número exibido é atualizado na hora. Clique novamente em **Gerar Inscrição Estadual** sempre que precisar de outro número.

Os números são gerados de forma aleatória, respeitando a regra de cálculo da inscrição estadual de Rondônia. Eles servem para testar softwares, formulários e validações, e não pertencem a empresas reais.

## Entendendo os termos

- **Inscrição Estadual (IE):** número de cadastro de uma empresa na Secretaria da Fazenda do seu estado, usado principalmente para controle do ICMS.
- **Rondônia (RO):** estado cuja regra de formação e de cálculo é usada para gerar o número.
- **Pontuação:** o hífen que separa os 13 primeiros dígitos do dígito verificador. Com pontuação o número fica no formato `0000000000000-0`.
- **Dígito verificador (DV):** último dígito do número, calculado a partir dos 13 dígitos anteriores. Ele serve para conferir se a inscrição é válida.
- **Módulo 11:** método de cálculo do dígito verificador. Cada dígito é multiplicado por um peso, os resultados são somados e a soma é dividida por 11. O resto da divisão define o dígito.
- **Pesos:** sequência de multiplicadores usada no cálculo. Para Rondônia, os 13 dígitos usam os pesos 6, 5, 4, 3, 2, 9, 8, 7, 6, 5, 4, 3 e 2, nessa ordem.
- **Dados de teste:** informações fictícias usadas por estudantes, programadores e testadores para verificar o funcionamento de um sistema sem usar dados reais.
- **Copiar:** botão que envia o número exibido para a área de transferência do seu dispositivo.

## Como o dígito verificador é calculado

1. Multiplique cada um dos 13 primeiros dígitos pelo peso correspondente (6, 5, 4, 3, 2, 9, 8, 7, 6, 5, 4, 3, 2).
2. Some todos os resultados.
3. Divida a soma por 11 e pegue o resto.
4. Calcule **11 − resto**. Se o resultado for 10 ou 11, subtraia 10 dele. O valor final é o dígito verificador.

**Exemplo:** para `0000000062521`, a soma é 6×6 + 2×5 + 5×4 + 2×3 + 1×2 = 74. O resto de 74 ÷ 11 é 8, então o dígito é 11 − 8 = **3**, e a inscrição completa é `0000000062521-3`.

**Importante:** use os números gerados apenas para testes. A má utilização dos dados é de responsabilidade de quem os utiliza.