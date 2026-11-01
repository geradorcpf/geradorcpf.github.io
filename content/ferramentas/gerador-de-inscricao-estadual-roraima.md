---
title: "Gerador de Inscrição Estadual de Roraima (RR)"
seoTitle: "Gerador de Inscrição Estadual de Roraima (RR)"
description: "Gerador de Inscrição Estadual de Roraima (RR): gere números válidos para testes de software. Grátis e online."
summary: "Gere inscrições estaduais válidas para testes."
date: 2026-11-01
draft: false
category: "documentos"
tags: ["inscrição estadual", "estados", "empresas", "gerador", "dados de teste", "roraima", "documentos"]
keywords: ["gerador de inscrição estadual de roraima (rr)", "gerador de inscrição estadual de roraima (rr) online", "inscrição estadual", "estados", "empresas"]
compact: true
---

Escolha se quer a pontuação e clique em **Gerar Inscrição Estadual**.

<div id="gerador-ie-rr" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🏢 Gerador de Inscrição Estadual de Roraima</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Gere números válidos de Roraima (RR) para testes de software.</p>
<span style="display:block;margin-bottom:8px;font-weight:600;font-size:0.95rem;">Gerar com pontuação?</span>
<div style="display:flex;gap:20px;flex-wrap:wrap;margin-bottom:20px;">
<label for="rr-pont-sim" style="display:flex;align-items:center;gap:8px;font-size:1rem;cursor:pointer;"><input type="radio" id="rr-pont-sim" name="rr-pontuacao" value="sim" checked style="width:18px;height:18px;accent-color:#4f46e5;cursor:pointer;">Sim</label>
<label for="rr-pont-nao" style="display:flex;align-items:center;gap:8px;font-size:1rem;cursor:pointer;"><input type="radio" id="rr-pont-nao" name="rr-pontuacao" value="nao" style="width:18px;height:18px;accent-color:#4f46e5;cursor:pointer;">Não</label>
</div>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="rr-gerar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Gerar Inscrição Estadual</button>
<button type="button" id="rr-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="rr-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="rr-resultado">clique em "Gerar Inscrição Estadual".</span></div>
<button type="button" id="rr-copiar" style="display:none;margin-top:12px;padding:10px 16px;font-size:0.95rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">📋 Copiar</button>
<p style="margin:16px 0 0;font-size:0.8rem;color:#64748b;line-height:1.5;">Os números são gerados de forma aleatória, respeitando a regra de criação do documento, e servem apenas para testes. O uso indevido é de responsabilidade do usuário.</p>
</div>
<script>
(function () {
  var sim = document.getElementById('rr-pont-sim');
  var resultado = document.getElementById('rr-resultado');
  var caixa = document.getElementById('rr-resposta');
  var btnCopiar = document.getElementById('rr-copiar');
  var padrao = 'clique em "Gerar Inscrição Estadual".';
  var atual = '';
  function gerar() {
    var digitos = [2, 4].concat(Array.from({ length: 6 }, function () { return Math.floor(Math.random() * 10); }));
    var soma = digitos.reduce(function (acc, d, i) { return acc + d * (i + 1); }, 0);
    var dv = soma % 9;
    var base = digitos.join('');
    return sim.checked ? base + '-' + dv : base + String(dv);
  }
  function mostrar() {
    atual = gerar();
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    resultado.style.fontWeight = '700';
    resultado.style.fontSize = '1.3rem';
    resultado.style.letterSpacing = '1px';
    resultado.textContent = atual;
    btnCopiar.style.display = 'inline-block';
    btnCopiar.textContent = '📋 Copiar';
  }
  function limpar() {
    atual = '';
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    resultado.style.color = '#64748b';
    resultado.style.fontWeight = '400';
    resultado.style.fontSize = '1rem';
    resultado.style.letterSpacing = 'normal';
    resultado.textContent = padrao;
    btnCopiar.style.display = 'none';
  }
  function copiado() {
    btnCopiar.textContent = '✅ Copiado!';
  }
  function copiar() {
    if (!atual) { return; }
    if (navigator.clipboard && navigator.clipboard.writeText) {
      navigator.clipboard.writeText(atual).then(copiado, copiarAlternativo);
    } else {
      copiarAlternativo();
    }
  }
  function copiarAlternativo() {
    var campo = document.createElement('textarea');
    campo.value = atual;
    campo.style.position = 'fixed';
    campo.style.opacity = '0';
    document.body.appendChild(campo);
    campo.select();
    try { document.execCommand('copy'); copiado(); } catch (e) { btnCopiar.textContent = 'Não foi possível copiar'; }
    document.body.removeChild(campo);
  }
  document.getElementById('rr-gerar').addEventListener('click', mostrar);
  document.getElementById('rr-limpar').addEventListener('click', limpar);
  btnCopiar.addEventListener('click', copiar);
})();
</script>

## Como usar o gerador

1. Em **Gerar com pontuação?**, escolha **Sim** para receber o número com hífen (por exemplo, `24006628-1`) ou **Não** para receber apenas os dígitos (`240066281`).
2. Clique em **Gerar Inscrição Estadual** para criar um novo número válido de Roraima.
3. Clique em **Copiar** para levar o número para a área de transferência e colá-lo no seu sistema ou formulário de teste.
4. Use o botão **Limpar** para apagar o resultado atual. Para gerar outro número, basta clicar novamente em **Gerar Inscrição Estadual**.

Cada clique cria um número diferente. Os números são fictícios e servem para testar softwares; não representam empresas reais.

## Entendendo os termos

- **Inscrição Estadual (IE):** número de cadastro de uma empresa na Secretaria da Fazenda do estado, usado para o controle do ICMS. Cada estado tem a sua própria regra de formação.
- **Roraima (RR):** estado cuja regra de formação é usada neste gerador. As inscrições estaduais de Roraima têm 9 dígitos e começam sempre com 24.
- **Pontuação:** o hífen que separa o dígito verificador do restante do número. No formato com pontuação, o número aparece como `24006628-1`.
- **Dígito verificador:** último dígito do número, calculado a partir dos 8 dígitos anteriores. Ele serve para conferir se a inscrição foi digitada corretamente.
- **Número válido:** número que segue a regra de formação e tem o dígito verificador correto. Isso não significa que ele esteja cadastrado na Secretaria da Fazenda.
- **Dados de teste:** informações fictícias usadas por programadores, analistas e testadores para verificar formulários e sistemas sem precisar de dados reais.
- **Copiar:** botão que envia o número gerado para a área de transferência, pronto para colar em outro lugar.