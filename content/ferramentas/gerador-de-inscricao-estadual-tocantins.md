---
title: "Gerador de Inscrição Estadual de Tocantins (TO)"
seoTitle: "Gerador de Inscrição Estadual de Tocantins (TO)"
description: "Gerador de Inscrição Estadual de Tocantins (TO): gere números válidos para testes de software. Grátis e online."
summary: "Gere inscrições estaduais válidas para testes."
date: 2026-11-01
draft: false
category: "documentos"
tags: ["inscrição estadual", "estados", "empresas", "gerador", "dados de teste", "tocantins", "documentos"]
keywords: ["gerador de inscrição estadual de tocantins (to)", "gerador de inscrição estadual de tocantins (to) online", "inscrição estadual", "estados", "empresas"]
compact: true
---

Basta escolher se deseja a inscrição com ou sem pontuação e depois clicar em **Gerar Inscrição Estadual**.

<div id="gerador-ie-to" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🏢 Gerador de Inscrição Estadual - TO</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Gere números válidos de Tocantins para testes de software.</p>
<span style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Gerar com Pontuação?</span>
<div style="display:flex;gap:10px;flex-wrap:wrap;margin-bottom:20px;">
<label for="ie-pont-sim" style="flex:1;min-width:120px;display:flex;align-items:center;gap:8px;padding:12px 14px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;cursor:pointer;"><input type="radio" id="ie-pont-sim" name="ie-pontuacao" value="sim" checked style="accent-color:#4f46e5;margin:0;"> Sim</label>
<label for="ie-pont-nao" style="flex:1;min-width:120px;display:flex;align-items:center;gap:8px;padding:12px 14px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;cursor:pointer;"><input type="radio" id="ie-pont-nao" name="ie-pontuacao" value="nao" style="accent-color:#4f46e5;margin:0;"> Não</label>
</div>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="ie-gerar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Gerar Inscrição Estadual</button>
<button type="button" id="ie-copiar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Copiar</button>
<button type="button" id="ie-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="ie-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="ie-resultado">clique em "Gerar Inscrição Estadual".</span></div>
</div>
<script>
(function () {
  var resultado = document.getElementById('ie-resultado');
  var caixa = document.getElementById('ie-resposta');
  var btnCopiar = document.getElementById('ie-copiar');
  var textoPadrao = 'clique em "Gerar Inscrição Estadual".';
  var ultimo = '';
  function sorteio(max) { return Math.floor(Math.random() * max); }
  function calcularDV(base) {
    var soma = 0;
    for (var i = 0; i !== base.length; i++) { soma += Number(base.charAt(i)) * (9 - i); }
    var resto = soma % 11;
    return (resto === 0 || resto === 1) ? 0 : 11 - resto;
  }
  function comPontuacao() {
    var marcado = document.querySelector('input[name="ie-pontuacao"]:checked');
    return !marcado || marcado.value === 'sim';
  }
  function gerar() {
    var tipos = ['01', '02', '03', '99'];
    var tipo = tipos[sorteio(tipos.length)];
    var seq = '';
    for (var i = 0; i !== 6; i++) { seq += String(sorteio(10)); }
    var dv = String(calcularDV('29' + seq));
    ultimo = comPontuacao() ? '29.' + tipo + '.' + seq + '-' + dv : '29' + tipo + seq + dv;
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    resultado.style.fontSize = '1.2rem';
    resultado.style.fontWeight = '700';
    resultado.style.letterSpacing = '0.04em';
    resultado.textContent = ultimo;
  }
  function erro(msg) {
    caixa.style.borderColor = '#fca5a5';
    caixa.style.background = '#fef2f2';
    resultado.style.color = '#b91c1c';
    resultado.style.fontSize = '1rem';
    resultado.style.fontWeight = '400';
    resultado.style.letterSpacing = 'normal';
    resultado.textContent = msg;
  }
  function feedbackCopiado() {
    btnCopiar.textContent = 'Copiado!';
    setTimeout(function () { btnCopiar.textContent = 'Copiar'; }, 1500);
  }
  function copiarFallback() {
    var area = document.createElement('textarea');
    area.value = ultimo;
    area.style.position = 'fixed';
    area.style.opacity = '0';
    document.body.appendChild(area);
    area.select();
    try { document.execCommand('copy'); feedbackCopiado(); } catch (e) { erro('não foi possível copiar automaticamente.'); }
    document.body.removeChild(area);
  }
  function copiar() {
    if (ultimo === '') { erro('gere uma inscrição estadual antes de copiar.'); return; }
    if (navigator.clipboard && navigator.clipboard.writeText) {
      navigator.clipboard.writeText(ultimo).then(feedbackCopiado, copiarFallback);
    } else {
      copiarFallback();
    }
  }
  function limpar() {
    ultimo = '';
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    resultado.style.color = '#64748b';
    resultado.style.fontSize = '1rem';
    resultado.style.fontWeight = '400';
    resultado.style.letterSpacing = 'normal';
    resultado.textContent = textoPadrao;
  }
  document.getElementById('ie-gerar').addEventListener('click', gerar);
  btnCopiar.addEventListener('click', copiar);
  document.getElementById('ie-limpar').addEventListener('click', limpar);
})();
</script>

## Como usar o gerador

1. Escolha se a inscrição estadual deve ser gerada **com pontuação** (ex.: `29.01.022783-6`) ou **sem pontuação** (ex.: `29010227836`).
2. Clique em **Gerar Inscrição Estadual** para criar um novo número válido para o estado de Tocantins (TO).
3. Clique em **Copiar** para enviar o número para a área de transferência e colá-lo no seu sistema ou formulário de teste.
4. Use o botão **Limpar** para apagar o resultado. Para gerar outro número, basta clicar novamente em **Gerar Inscrição Estadual**.

Os números são gerados de forma aleatória, seguindo a regra de formação e o cálculo do dígito verificador usados em Tocantins. Eles servem apenas para testes de software e não pertencem necessariamente a empresas reais.

## Entendendo os termos

- **Inscrição Estadual (IE):** número de cadastro de uma empresa na Secretaria da Fazenda do estado, usado principalmente para o controle do ICMS.
- **Tocantins (TO):** estado para o qual o número é gerado. Cada estado brasileiro tem seu próprio formato e regra de cálculo.
- **Pontuação:** pontos e hífen que separam os grupos do número, no formato `99.99.999999-9`.
- **Código do estado (29):** os dois primeiros dígitos, que identificam as inscrições estaduais de Tocantins.
- **Tipo de empresa:** o terceiro e o quarto dígitos, que indicam a categoria do contribuinte. Os valores usados são 01, 02, 03 e 99.
- **Número sequencial:** os seis dígitos seguintes, gerados aleatoriamente neste gerador.
- **Dígito verificador:** o último dígito, calculado a partir dos demais para confirmar que o número é válido.
- **Dados de teste:** números fictícios, mas com formato válido, usados para testar sistemas sem expor dados reais de empresas.