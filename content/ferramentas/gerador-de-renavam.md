---
title: "Gerador de Renavam"
seoTitle: "Gerador de Renavam"
description: "Gerador de Renavam: gere números de Renavam válidos para testes. Grátis e online, sem cadastro."
summary: "Gere números de Renavam válidos para testes."
date: 2026-11-03
draft: false
category: "documentos"
tags: ["renavam", "veículos", "gerador", "dados de teste", "documentos"]
keywords: ["gerador de renavam", "gerador de renavam online", "renavam", "veículos", "gerador"]
---

Basta clicar em **Gerar Renavam** abaixo para criar um número de Renavam válido, feito para testes de sistemas e formulários.

<div id="gerador-renavam" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🚗 Gerador de Renavam</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Clique no botão e receba um Renavam válido na hora.</p>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="ren-gerar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Gerar Renavam</button>
<button type="button" id="ren-copiar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Copiar</button>
<button type="button" id="ren-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="ren-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="ren-resultado">clique em "Gerar Renavam".</span></div>
</div>
<script>
(function () {
  var resultado = document.getElementById('ren-resultado');
  var caixa = document.getElementById('ren-resposta');
  var btnCopiar = document.getElementById('ren-copiar');
  var atual = '';
  var pesos = [3, 2, 9, 8, 7, 6, 5, 4, 3, 2];
  function aleatorio(max) { return Math.floor(Math.random() * max); }
  function criarRenavam() {
    var digitos = [1 + aleatorio(9)];
    while (digitos.length !== 10) { digitos.push(aleatorio(10)); }
    var soma = 0;
    digitos.forEach(function (d, i) { soma += d * pesos[i]; });
    var dv = (soma * 10) % 11;
    if (dv === 10) { dv = 0; }
    digitos.push(dv);
    return digitos.join('');
  }
  function gerar() {
    atual = criarRenavam();
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    resultado.innerHTML = '<strong style="font-size:1.4rem;letter-spacing:2px;font-family:ui-monospace,SFMono-Regular,Menlo,Consolas,monospace;">' + atual + '</strong><br><small style="color:#475569;">Renavam válido de 11 dígitos, gerado aleatoriamente.</small>';
    btnCopiar.textContent = 'Copiar';
  }
  function avisoCopiado() {
    btnCopiar.textContent = 'Copiado!';
    setTimeout(function () { btnCopiar.textContent = 'Copiar'; }, 1800);
  }
  function copiarAlternativo() {
    var campo = document.createElement('textarea');
    campo.value = atual;
    campo.setAttribute('readonly', '');
    campo.style.position = 'fixed';
    campo.style.opacity = '0';
    document.body.appendChild(campo);
    campo.select();
    try { document.execCommand('copy'); avisoCopiado(); } catch (e) { btnCopiar.textContent = 'Erro ao copiar'; }
    document.body.removeChild(campo);
  }
  function copiar() {
    if (atual === '') {
      caixa.style.borderColor = '#fca5a5';
      caixa.style.background = '#fef2f2';
      resultado.style.color = '#b91c1c';
      resultado.textContent = 'gere um Renavam antes de copiar.';
      return;
    }
    if (navigator.clipboard) {
      navigator.clipboard.writeText(atual).then(avisoCopiado, copiarAlternativo);
    } else {
      copiarAlternativo();
    }
  }
  function limpar() {
    atual = '';
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    resultado.style.color = '#64748b';
    resultado.textContent = 'clique em "Gerar Renavam".';
    btnCopiar.textContent = 'Copiar';
  }
  document.getElementById('ren-gerar').addEventListener('click', gerar);
  btnCopiar.addEventListener('click', copiar);
  document.getElementById('ren-limpar').addEventListener('click', limpar);
})();
</script>

## Como usar o gerador

1. Clique no botão **Gerar Renavam** para criar um novo número.
2. Veja o Renavam de 11 dígitos exibido na caixa de resposta.
3. Clique em **Copiar** para levar o número para a área de transferência e colar onde precisar.
4. Clique em **Gerar Renavam** quantas vezes quiser para obter novos números, ou use **Limpar** para apagar o resultado.

Os números são criados de forma aleatória, seguindo a regra de cálculo do dígito verificador. Eles servem apenas para testes de software, preenchimento de formulários de desenvolvimento e estudos. Não correspondem a veículos reais, e o uso indevido dos dados é de responsabilidade de quem os utiliza.

## Entendendo os termos

- **Renavam:** sigla de Registro Nacional de Veículos Automotores, o número que identifica cada veículo registrado no Brasil. Aparece no documento do veículo (CRLV).
- **Gerador de Renavam:** ferramenta que cria números de Renavam com estrutura válida, sem precisar consultar nenhum veículo real.
- **Número válido:** número que respeita o formato e o cálculo do dígito verificador, por isso passa em validações de formulários e sistemas.
- **Dígito verificador:** último dígito do Renavam, calculado a partir dos 10 dígitos anteriores. Serve para detectar erros de digitação.
- **11 dígitos:** tamanho padrão atual do Renavam. Números antigos com 9 dígitos são completados com zeros à esquerda.
- **Dados de teste:** informações fictícias usadas por programadores, analistas e testadores para verificar o funcionamento de sistemas.
- **CRLV:** Certificado de Registro e Licenciamento de Veículo, o documento que traz o Renavam, a placa e os dados do veículo.
- **Aleatório:** cada clique gera uma combinação diferente de dígitos, sem relação com veículos existentes.