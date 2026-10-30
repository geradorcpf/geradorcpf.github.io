---
title: "Gerador de Inscrição Estadual do Amapá (AP)"
seoTitle: "Gerador de Inscrição Estadual do Amapá (AP)"
description: "Gerador de Inscrição Estadual do Amapá (AP): gere números válidos para testes de software. Grátis e online."
summary: "Gere inscrições estaduais válidas para testes."
date: 2026-10-30
draft: false
category: "documentos"
tags: ["inscrição estadual", "estados", "empresas", "gerador", "dados de teste", "amapá", "documentos"]
keywords: ["gerador de inscrição estadual do amapá (ap)", "gerador de inscrição estadual do amapá (ap) online", "inscrição estadual", "estados", "empresas"]
compact: true
---

Escolha se quer a pontuação e clique em **Gerar Inscrição Estadual** para criar um número válido do Amapá (AP).

<div id="gerador-ie-ap" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🏢 Gerador de Inscrição Estadual do Amapá (AP)</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Gere números válidos para testes de software.</p>
<span style="display:block;margin-bottom:8px;font-weight:600;font-size:0.95rem;">Gerar com Pontuação?</span>
<div style="display:flex;gap:10px;flex-wrap:wrap;margin-bottom:20px;">
<label for="ie-pontuacao-sim" style="flex:1;min-width:120px;display:flex;align-items:center;gap:8px;padding:12px 14px;font-size:1rem;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;box-sizing:border-box;"><input type="radio" id="ie-pontuacao-sim" name="ie-pontuacao" value="sim" checked style="accent-color:#4f46e5;"> Sim</label>
<label for="ie-pontuacao-nao" style="flex:1;min-width:120px;display:flex;align-items:center;gap:8px;padding:12px 14px;font-size:1rem;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;box-sizing:border-box;"><input type="radio" id="ie-pontuacao-nao" name="ie-pontuacao" value="nao" style="accent-color:#4f46e5;"> Não</label>
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
  var botaoGerar = document.getElementById('ie-gerar');
  var radioSim = document.getElementById('ie-pontuacao-sim');
  var atual = '';
  function sorteiaBase() {
    var n = 0;
    while (n === 0) { n = Math.floor(Math.random() * 1000000); }
    return '03' + ('000000' + n).slice(-6);
  }
  function digitoVerificador(base) {
    var n = Number(base);
    var p = 0;
    var d = 0;
    if (n >= 3000001 && n <= 3017000) { p = 5; d = 0; }
    else if (n >= 3017001 && n <= 3019022) { p = 9; d = 1; }
    var soma = p;
    base.split('').forEach(function (c, i) { soma += Number(c) * (9 - i); });
    var dv = 11 - (soma % 11);
    if (dv === 10) { dv = 0; }
    else if (dv === 11) { dv = d; }
    return String(dv);
  }
  function formatar(ie) {
    return ie.substr(0, 2) + '.' + ie.substr(2, 3) + '.' + ie.substr(5, 3) + '-' + ie.substr(8, 1);
  }
  function mostrar(texto) {
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    resultado.textContent = '';
    var forte = document.createElement('strong');
    forte.style.fontSize = '1.2rem';
    forte.textContent = texto;
    resultado.appendChild(forte);
  }
  function erro(msg) {
    caixa.style.borderColor = '#fca5a5';
    caixa.style.background = '#fef2f2';
    resultado.style.color = '#b91c1c';
    resultado.textContent = msg;
  }
  function gerar() {
    var base = sorteiaBase();
    var ie = base + digitoVerificador(base);
    atual = radioSim.checked ? formatar(ie) : ie;
    mostrar(atual);
    botaoCopiar.textContent = 'Copiar';
  }
  function copiarFallback(texto) {
    var campo = document.createElement('textarea');
    campo.value = texto;
    campo.setAttribute('readonly', '');
    campo.style.position = 'fixed';
    campo.style.top = '-1000px';
    document.body.appendChild(campo);
    campo.select();
    var ok = false;
    try { ok = document.execCommand('copy'); } catch (e) { ok = false; }
    document.body.removeChild(campo);
    return ok;
  }
  function copiar() {
    if (atual === '') { erro('gere uma inscrição estadual antes de copiar.'); return; }
    function sucesso() { botaoCopiar.textContent = 'Copiado!'; }
    function falha() {
      if (copiarFallback(atual)) { sucesso(); } else { erro('não foi possível copiar. Selecione o número e copie manualmente.'); }
    }
    if (navigator.clipboard && navigator.clipboard.writeText) {
      navigator.clipboard.writeText(atual).then(sucesso, falha);
    } else {
      falha();
    }
  }
  function atualizarFormato() {
    if (atual === '') { return; }
    var puro = atual.replace(/\D/g, '');
    atual = radioSim.checked ? formatar(puro) : puro;
    mostrar(atual);
  }
  botaoGerar.addEventListener('click', gerar);
  botaoCopiar.addEventListener('click', copiar);
  Array.prototype.forEach.call(document.getElementsByName('ie-pontuacao'), function (el) {
    el.addEventListener('change', atualizarFormato);
  });
})();
</script>

## Como usar o gerador

1. Em **Gerar com Pontuação?**, escolha **Sim** para o número com pontos e traço (ex.: `03.012.345-9`) ou **Não** para apenas os dígitos (ex.: `030123459`).
2. Clique em **Gerar Inscrição Estadual** para criar um novo número válido do Amapá.
3. Se quiser trocar o formato depois de gerar, basta alternar entre **Sim** e **Não**: o mesmo número é exibido com ou sem pontuação.
4. Clique em **Copiar** para levar o número para a área de transferência e colar no seu sistema ou formulário de teste.
5. Clique em **Gerar Inscrição Estadual** novamente sempre que precisar de outro número.

Os números são gerados de forma aleatória, seguindo a regra de formação da inscrição estadual do Amapá. Eles servem apenas para testes de software e não pertencem, necessariamente, a empresas reais.

## Entendendo os termos

- **Inscrição Estadual (IE):** número de cadastro de uma empresa na Secretaria da Fazenda do seu estado, usado para contribuintes de ICMS.
- **Amapá (AP):** estado onde a inscrição é válida. No Amapá, o número tem 9 dígitos e sempre começa com **03**.
- **Gerar com Pontuação:** define se o número aparece formatado com pontos e traço (`03.012.345-9`) ou somente com dígitos (`030123459`).
- **Dígito verificador:** o último dígito do número, calculado a partir dos 8 primeiros. Serve para conferir se a inscrição é válida.
- **Número válido:** número que passa na regra de cálculo do dígito verificador, mas que pode não estar cadastrado de fato na Sefaz.
- **Dados de teste:** informações fictícias usadas por programadores, analistas e testadores para validar formulários e sistemas em desenvolvimento.
- **Copiar:** botão que envia o número gerado para a área de transferência do seu dispositivo.

## Aviso importante

Este gerador ajuda estudantes, programadores, analistas e testadores a obter inscrições estaduais válidas para testar softwares em desenvolvimento. A má utilização dos dados gerados é de total responsabilidade do usuário.