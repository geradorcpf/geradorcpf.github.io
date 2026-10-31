---
title: "Gerador de Inscrição Estadual do Mato Grosso (MT)"
seoTitle: "Gerador de Inscrição Estadual do Mato Grosso (MT)"
description: "Gerador de Inscrição Estadual do Mato Grosso (MT): gere números válidos para testes de software. Grátis e online."
summary: "Gere inscrições estaduais válidas para testes."
date: 2026-10-31
draft: false
category: "documentos"
tags: ["inscrição estadual", "estados", "empresas", "gerador", "dados de teste", "mato grosso", "documentos"]
keywords: ["gerador de inscrição estadual do mato grosso (mt)", "gerador de inscrição estadual do mato grosso (mt) online", "inscrição estadual", "estados", "empresas"]
compact: true
---

Escolha se deseja o número com pontuação e depois clique em **Gerar Inscrição Estadual**.

<div id="gerador-ie-mt" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🏢 Gerador de Inscrição Estadual (MT)</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Gere um número válido para Mato Grosso na hora.</p>
<span style="display:block;margin-bottom:8px;font-weight:600;font-size:0.95rem;">Gerar com Pontuação?</span>
<div style="display:flex;gap:20px;margin-bottom:20px;flex-wrap:wrap;">
<label for="ie-pontuacao-sim" style="display:flex;align-items:center;gap:8px;font-size:1rem;cursor:pointer;"><input type="radio" id="ie-pontuacao-sim" name="ie-pontuacao" value="sim" checked style="width:18px;height:18px;accent-color:#4f46e5;cursor:pointer;">Sim</label>
<label for="ie-pontuacao-nao" style="display:flex;align-items:center;gap:8px;font-size:1rem;cursor:pointer;"><input type="radio" id="ie-pontuacao-nao" name="ie-pontuacao" value="nao" style="width:18px;height:18px;accent-color:#4f46e5;cursor:pointer;">Não</label>
</div>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="ie-gerar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Gerar Inscrição Estadual</button>
<button type="button" id="ie-copiar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Copiar</button>
</div>
<div id="ie-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="ie-resultado">clique em "Gerar Inscrição Estadual".</span></div>
<p style="margin:14px 0 0;font-size:0.8rem;color:#64748b;line-height:1.5;">Os números são gerados de forma aleatória, seguindo a regra de cálculo do dígito verificador. Use apenas para testes de software.</p>
</div>
<script>
(function () {
  var radioSim = document.getElementById('ie-pontuacao-sim');
  var resultado = document.getElementById('ie-resultado');
  var caixa = document.getElementById('ie-resposta');
  var botaoCopiar = document.getElementById('ie-copiar');
  var atual = '';
  function calcularDigito(base) {
    var pesos = [3, 2, 9, 8, 7, 6, 5, 4, 3, 2];
    var soma = 0;
    for (var i = 0; i !== 10; i++) {
      soma += base[i] * pesos[i];
    }
    var resto = soma % 11;
    if (resto === 0 || resto === 1) { return 0; }
    return 11 - resto;
  }
  function gerarNumero(comPontuacao) {
    var base = [];
    for (var i = 0; i !== 10; i++) {
      base.push(Math.floor(Math.random() * 10));
    }
    var digito = calcularDigito(base);
    var corpo = base.join('');
    if (comPontuacao) { return corpo + '-' + digito; }
    return corpo + digito;
  }
  function gerar() {
    atual = gerarNumero(radioSim.checked);
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    resultado.style.fontWeight = '700';
    resultado.style.fontSize = '1.2rem';
    resultado.style.letterSpacing = '1px';
    resultado.textContent = atual;
    botaoCopiar.textContent = 'Copiar';
  }
  function copiarFallback(texto) {
    var campo = document.createElement('textarea');
    campo.value = texto;
    campo.style.position = 'fixed';
    campo.style.opacity = '0';
    document.body.appendChild(campo);
    campo.select();
    try { document.execCommand('copy'); } catch (e) {}
    document.body.removeChild(campo);
  }
  function copiar() {
    if (atual === '') { gerar(); }
    if (navigator.clipboard) {
      navigator.clipboard.writeText(atual).catch(function () { copiarFallback(atual); });
    } else {
      copiarFallback(atual);
    }
    botaoCopiar.textContent = 'Copiado!';
    setTimeout(function () { botaoCopiar.textContent = 'Copiar'; }, 1800);
  }
  document.getElementById('ie-gerar').addEventListener('click', gerar);
  botaoCopiar.addEventListener('click', copiar);
})();
</script>

## Como usar o gerador

1. Em **Gerar com Pontuação?**, escolha **Sim** para o número com hífen (por exemplo, `0013000001-9`) ou **Não** para apenas os dígitos (por exemplo, `00130000019`).
2. Clique em **Gerar Inscrição Estadual** para criar um novo número válido de Mato Grosso.
3. Clique em **Copiar** para levar o número para a área de transferência e colar no seu sistema.
4. Clique em **Gerar Inscrição Estadual** novamente sempre que precisar de outro número.

Os números são aleatórios e respeitam a regra de criação do documento, mas não pertencem a empresas reais. Use somente em testes e desenvolvimento de software.

## Entendendo os termos

- **Inscrição Estadual (IE):** número de registro de uma empresa contribuinte de ICMS na Secretaria de Fazenda do seu estado.
- **Mato Grosso (MT):** estado para o qual o número é gerado. Cada estado brasileiro tem o seu próprio formato e cálculo de inscrição estadual.
- **ICMS:** Imposto sobre Circulação de Mercadorias e Serviços, cobrado pelos estados. A inscrição estadual identifica quem recolhe esse imposto.
- **SEFAZ-MT:** Secretaria de Estado de Fazenda de Mato Grosso, órgão responsável por emitir e controlar as inscrições estaduais no estado.
- **Dígito verificador:** último dígito do número, calculado a partir dos anteriores. Serve para conferir se a inscrição é válida.
- **Pontuação:** separadores usados na exibição do número. Em Mato Grosso, um hífen antes do dígito verificador (`0000000000-0`).
- **Módulo 11:** cálculo em que cada um dos 10 primeiros dígitos é multiplicado por um peso (3, 2, 9, 8, 7, 6, 5, 4, 3, 2), os resultados são somados e o total é dividido por 11. Do resto sai o dígito verificador: se o resto for 0 ou 1, o dígito é 0; nos demais casos, é 11 menos o resto.
- **Dados de teste:** informações fictícias, mas com formato válido, usadas por programadores, analistas e testadores para validar cadastros e sistemas.