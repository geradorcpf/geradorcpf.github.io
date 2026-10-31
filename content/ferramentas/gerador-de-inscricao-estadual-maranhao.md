---
title: "Gerador de Inscrição Estadual do Maranhão (MA)"
seoTitle: "Gerador de Inscrição Estadual do Maranhão (MA)"
description: "Gerador de Inscrição Estadual do Maranhão (MA): gere números válidos para testes de software. Grátis e online."
summary: "Gere inscrições estaduais válidas para testes."
date: 2026-10-31
draft: false
category: "documentos"
tags: ["inscrição estadual", "estados", "empresas", "gerador", "dados de teste", "maranhão", "documentos"]
keywords: ["gerador de inscrição estadual do maranhão (ma)", "gerador de inscrição estadual do maranhão (ma) online", "inscrição estadual", "estados", "empresas"]
compact: true
---

Basta escolher se quer a pontuação e clicar em **Gerar Inscrição Estadual**.

<div id="gerador-ie-ma" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🏢 Gerador de Inscrição Estadual do Maranhão (MA)</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Gere números válidos para testes de software.</p>
<span style="display:block;margin-bottom:8px;font-weight:600;font-size:0.95rem;">Gerar com pontuação?</span>
<div style="display:flex;gap:20px;margin-bottom:20px;flex-wrap:wrap;">
<label for="ie-ma-sim" style="display:flex;align-items:center;gap:8px;font-size:1rem;cursor:pointer;"><input type="radio" id="ie-ma-sim" name="ie-ma-pontuacao" value="sim" checked style="width:18px;height:18px;accent-color:#4f46e5;cursor:pointer;">Sim</label>
<label for="ie-ma-nao" style="display:flex;align-items:center;gap:8px;font-size:1rem;cursor:pointer;"><input type="radio" id="ie-ma-nao" name="ie-ma-pontuacao" value="nao" style="width:18px;height:18px;accent-color:#4f46e5;cursor:pointer;">Não</label>
</div>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="ie-ma-gerar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Gerar Inscrição Estadual</button>
<button type="button" id="ie-ma-copiar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Copiar</button>
</div>
<div id="ie-ma-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="ie-ma-resultado">clique em "Gerar Inscrição Estadual".</span></div>
</div>
<script>
(function () {
  var radioSim = document.getElementById('ie-ma-sim');
  var resultado = document.getElementById('ie-ma-resultado');
  var caixa = document.getElementById('ie-ma-resposta');
  var botaoCopiar = document.getElementById('ie-ma-copiar');
  var atual = '';
  function calcularDv(digitos) {
    var soma = 0;
    for (var i = 0; i !== 8; i++) { soma += digitos[i] * (9 - i); }
    var resto = soma % 11;
    return (resto === 0 || resto === 1) ? 0 : 11 - resto;
  }
  function gerar() {
    var d = [1, 2];
    for (var i = 0; i !== 6; i++) { d.push(Math.floor(Math.random() * 10)); }
    d.push(calcularDv(d));
    var s = d.join('');
    if (radioSim.checked) {
      s = s.slice(0, 2) + '.' + s.slice(2, 5) + '.' + s.slice(5, 8) + '-' + s.slice(8);
    }
    atual = s;
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    resultado.style.fontWeight = '700';
    resultado.style.fontSize = '1.2rem';
    resultado.textContent = s;
    botaoCopiar.textContent = 'Copiar';
  }
  function copiar() {
    if (atual === '') { return; }
    var ok = function () { botaoCopiar.textContent = 'Copiado!'; };
    if (navigator.clipboard && navigator.clipboard.writeText) {
      navigator.clipboard.writeText(atual).then(ok, function () { copiarAntigo(ok); });
    } else {
      copiarAntigo(ok);
    }
  }
  function copiarAntigo(ok) {
    var t = document.createElement('textarea');
    t.value = atual;
    t.style.position = 'fixed';
    t.style.opacity = '0';
    document.body.appendChild(t);
    t.select();
    try { document.execCommand('copy'); ok(); } catch (e) {}
    document.body.removeChild(t);
  }
  document.getElementById('ie-ma-gerar').addEventListener('click', gerar);
  botaoCopiar.addEventListener('click', copiar);
})();
</script>

## Como usar o gerador

1. Em **Gerar com pontuação?**, escolha **Sim** para o número com pontos e hífen (por exemplo, `12.345.678-9`) ou **Não** para apenas os dígitos (`123456789`).
2. Clique em **Gerar Inscrição Estadual** para criar um novo número válido do Maranhão.
3. Veja o número no campo **Resposta**.
4. Clique em **Copiar** para levar o número para a área de transferência e colá-lo no seu sistema.
5. Clique em **Gerar Inscrição Estadual** quantas vezes quiser para obter novos números.

Os números são gerados de forma aleatória, seguindo as regras de formação da inscrição estadual do Maranhão. Eles servem apenas para testes e não pertencem necessariamente a empresas reais.

## Entendendo os termos

- **Inscrição Estadual (IE):** número de registro de uma empresa na Secretaria da Fazenda do estado, usado para o recolhimento do ICMS.
- **Maranhão (MA):** estado para o qual o número é gerado. Cada estado brasileiro tem seu próprio formato e regra de cálculo.
- **Pontuação:** pontos e hífen usados para separar os grupos de dígitos, como em `12.345.678-9`.
- **Dígito verificador (DV):** último dígito do número, calculado a partir dos anteriores para confirmar que a inscrição é válida.
- **Número válido:** número que passa na regra de cálculo do dígito verificador, mesmo sem estar cadastrado de verdade.
- **ICMS:** Imposto sobre Circulação de Mercadorias e Serviços, cobrado pelos estados e ligado à inscrição estadual.
- **Dados de teste:** informações fictícias usadas por desenvolvedores e testadores para verificar o funcionamento de sistemas.

## Como a inscrição estadual do Maranhão é formada

A inscrição estadual do Maranhão tem **9 dígitos** e sempre começa com **12**. O formato com pontuação é `12.NNN.NNN-D`:

- **12:** código do estado do Maranhão.
- **NNNNNN:** seis dígitos aleatórios.
- **D:** dígito verificador.

O dígito verificador é calculado assim:

1. Multiplique os 8 primeiros dígitos pelos pesos **9, 8, 7, 6, 5, 4, 3 e 2**, nessa ordem.
2. Some os resultados.
3. Divida a soma por 11 e pegue o **resto**.
4. Se o resto for **0** ou **1**, o dígito verificador é **0**. Nos demais casos, ele é **11 menos o resto**.

## Exemplo resolvido

Vamos calcular o dígito verificador da base `12345678`:

1. Multiplicação: 1×9 + 2×8 + 3×7 + 4×6 + 5×5 + 6×4 + 7×3 + 8×2.
2. Soma: 9 + 16 + 21 + 24 + 25 + 24 + 21 + 16 = 156.
3. Resto da divisão: 156 ÷ 11 = 14, com resto 2.
4. Dígito verificador: 11 − 2 = 9.

**Resposta:** a inscrição estadual é `123456789`, ou **12.345.678-9** com pontuação.

**Importante:** use os números gerados apenas para testes de software. O uso indevido dos dados é de responsabilidade do usuário.