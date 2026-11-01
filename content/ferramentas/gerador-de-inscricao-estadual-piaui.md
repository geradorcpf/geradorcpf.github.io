---
title: "Gerador de Inscrição Estadual do Piauí (PI)"
seoTitle: "Gerador de Inscrição Estadual do Piauí (PI)"
description: "Gerador de Inscrição Estadual do Piauí (PI): gere números válidos para testes de software. Grátis e online."
summary: "Gere inscrições estaduais válidas para testes."
date: 2026-11-01
draft: false
category: "documentos"
tags: ["inscrição estadual", "estados", "empresas", "gerador", "dados de teste", "piauí", "documentos"]
keywords: ["gerador de inscrição estadual do piauí (pi)", "gerador de inscrição estadual do piauí (pi) online", "inscrição estadual", "estados", "empresas"]
compact: true
---

Escolha se deseja o número com ou sem pontuação e clique em **Gerar Inscrição Estadual**.

<div id="gerador-ie-pi" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🏢 Gerador de Inscrição Estadual do Piauí (PI)</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Gere números válidos para testar seus sistemas.</p>
<span style="display:block;margin-bottom:8px;font-weight:600;font-size:0.95rem;">Gerar com pontuação?</span>
<div style="display:flex;gap:20px;flex-wrap:wrap;margin-bottom:20px;">
<label for="ie-pont-sim" style="display:flex;align-items:center;gap:8px;font-size:1rem;cursor:pointer;"><input type="radio" id="ie-pont-sim" name="ie-pontuacao" value="sim" checked style="width:18px;height:18px;accent-color:#4f46e5;cursor:pointer;">Sim</label>
<label for="ie-pont-nao" style="display:flex;align-items:center;gap:8px;font-size:1rem;cursor:pointer;"><input type="radio" id="ie-pont-nao" name="ie-pontuacao" value="nao" style="width:18px;height:18px;accent-color:#4f46e5;cursor:pointer;">Não</label>
</div>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="ie-gerar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Gerar Inscrição Estadual</button>
<button type="button" id="ie-copiar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Copiar</button>
</div>
<div id="ie-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="ie-resultado">clique em "Gerar Inscrição Estadual".</span></div>
</div>
<script>
(function () {
  var resultado = document.getElementById('ie-resultado');
  var caixa = document.getElementById('ie-resposta');
  var botaoCopiar = document.getElementById('ie-copiar');
  var atual = '';
  function gerar() {
    var digitos = [];
    var soma = 0;
    var i;
    for (i = 0; i !== 8; i++) {
      var n = Math.floor(Math.random() * 10);
      digitos.push(n);
      soma += n * (9 - i);
    }
    var dv = 11 - (soma % 11);
    if (dv > 9) { dv = 0; }
    var base = digitos.join('');
    var comPontuacao = document.getElementById('ie-pont-sim').checked;
    atual = comPontuacao ? base + '-' + dv : base + String(dv);
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    resultado.style.fontWeight = '700';
    resultado.style.fontSize = '1.2rem';
    resultado.style.letterSpacing = '1px';
    resultado.textContent = atual;
    botaoCopiar.textContent = 'Copiar';
  }
  function marcarCopiado() {
    botaoCopiar.textContent = 'Copiado!';
  }
  function copiar() {
    if (atual === '') { return; }
    if (navigator.clipboard && navigator.clipboard.writeText) {
      navigator.clipboard.writeText(atual).then(marcarCopiado, function () {});
      return;
    }
    var campo = document.createElement('textarea');
    campo.value = atual;
    document.body.appendChild(campo);
    campo.select();
    try { document.execCommand('copy'); marcarCopiado(); } catch (e) {}
    document.body.removeChild(campo);
  }
  document.getElementById('ie-gerar').addEventListener('click', gerar);
  botaoCopiar.addEventListener('click', copiar);
})();
</script>

## Como usar o gerador

1. Em **Gerar com pontuação?**, escolha **Sim** para receber o número com hífen (ex.: `12345678-9`) ou **Não** para receber apenas os dígitos (ex.: `123456789`).
2. Clique em **Gerar Inscrição Estadual** para criar um novo número válido para o Piauí.
3. Clique em **Copiar** para levar o número para a área de transferência e colá-lo no seu sistema ou formulário de teste.
4. Clique em **Gerar Inscrição Estadual** novamente sempre que precisar de outro número.

Os números são gerados de forma aleatória, respeitando a regra de cálculo do dígito verificador do estado. Eles servem apenas para testes de software e não correspondem necessariamente a empresas reais.

## Entendendo os termos

- **Inscrição Estadual (IE):** número de registro de uma empresa na Secretaria da Fazenda do estado, usado para controlar o ICMS.
- **ICMS:** imposto estadual sobre a circulação de mercadorias e serviços.
- **Piauí (PI):** estado brasileiro cuja inscrição estadual possui 9 dígitos.
- **Pontuação:** separadores visuais no número, como o hífen antes do último dígito.
- **Dígito verificador:** último dígito do número, calculado a partir dos 8 primeiros para confirmar que a inscrição é válida.
- **Número válido:** número que passa na regra de cálculo do dígito verificador, mesmo sem estar cadastrado na Sefaz.
- **Dados de teste:** informações fictícias usadas por programadores, analistas e testadores para validar sistemas.
- **Copiar:** botão que envia o número gerado para a área de transferência do seu dispositivo.

## Como o dígito verificador é calculado

Cada um dos 8 primeiros dígitos é multiplicado por pesos decrescentes de 9 a 2. A soma dos resultados é dividida por 11 e o dígito verificador é **11 menos o resto da divisão**. Se o resultado for 10 ou 11, o dígito verificador passa a ser 0.

## Aviso importante

Este gerador ajuda estudantes, programadores, analistas e testadores a obter inscrições estaduais válidas para testar softwares em desenvolvimento. O uso indevido dos dados gerados é de responsabilidade do usuário.