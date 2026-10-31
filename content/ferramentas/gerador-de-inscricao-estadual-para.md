---
title: "Gerador de Inscrição Estadual do Pará (PA)"
seoTitle: "Gerador de Inscrição Estadual do Pará (PA)"
description: "Gerador de Inscrição Estadual do Pará (PA): gere números válidos para testes de software. Grátis e online."
summary: "Gere inscrições estaduais válidas para testes."
date: 2026-10-31
draft: false
category: "documentos"
tags: ["inscrição estadual", "estados", "empresas", "gerador", "dados de teste", "pará", "documentos"]
keywords: ["gerador de inscrição estadual do pará (pa)", "gerador de inscrição estadual do pará (pa) online", "inscrição estadual", "estados", "empresas"]
compact: true
---
<!--INI SUDAH DIKERJAKAN-->

Basta escolher se deseja a inscrição com ou sem pontuação e depois clicar em **Gerar Inscrição Estadual**.

<div id="gerador-ie-pa" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🏢 Gerador de Inscrição Estadual do Pará (PA)</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Escolha a opção e gere um número válido na hora.</p>
<span style="display:block;margin-bottom:8px;font-weight:600;font-size:0.95rem;">Gerar com pontuação?</span>
<div style="display:flex;gap:12px;flex-wrap:wrap;margin-bottom:20px;">
<label for="ie-pontuacao-sim" style="flex:1;min-width:120px;display:flex;align-items:center;gap:8px;padding:12px 14px;font-size:1rem;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;box-sizing:border-box;"><input type="radio" id="ie-pontuacao-sim" name="ie-pontuacao" value="sim" checked style="margin:0;accent-color:#4f46e5;cursor:pointer;">Sim</label>
<label for="ie-pontuacao-nao" style="flex:1;min-width:120px;display:flex;align-items:center;gap:8px;padding:12px 14px;font-size:1rem;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;box-sizing:border-box;"><input type="radio" id="ie-pontuacao-nao" name="ie-pontuacao" value="nao" style="margin:0;accent-color:#4f46e5;cursor:pointer;">Não</label>
</div>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="ie-gerar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Gerar Inscrição Estadual</button>
<button type="button" id="ie-copiar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Copiar</button>
</div>
<div id="ie-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="ie-resultado">clique em "Gerar Inscrição Estadual".</span></div>
</div>
<script>
(function () {
  var radioSim = document.getElementById('ie-pontuacao-sim');
  var radioNao = document.getElementById('ie-pontuacao-nao');
  var resultado = document.getElementById('ie-resultado');
  var caixa = document.getElementById('ie-resposta');
  var botaoGerar = document.getElementById('ie-gerar');
  var botaoCopiar = document.getElementById('ie-copiar');
  var corpo = '';
  var dv = 0;
  var timer = null;
  function formatar() {
    if (radioSim.checked) {
      return corpo.substring(0, 2) + '-' + corpo.substring(2) + '-' + String(dv);
    }
    return corpo + String(dv);
  }
  function mostrar() {
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    resultado.style.fontWeight = '700';
    resultado.style.fontSize = '1.2rem';
    resultado.style.letterSpacing = '0.5px';
    resultado.textContent = formatar();
  }
  function gerar() {
    var base = [1, 5];
    var i;
    for (i = 0; i !== 6; i++) {
      base.push(Math.floor(Math.random() * 10));
    }
    var soma = 0;
    for (i = 0; i !== 8; i++) {
      soma += base[i] * (9 - i);
    }
    var resto = soma % 11;
    dv = (resto === 0 || resto === 1) ? 0 : 11 - resto;
    corpo = base.join('');
    mostrar();
  }
  function copiarTexto(texto) {
    if (navigator.clipboard && navigator.clipboard.writeText) {
      return navigator.clipboard.writeText(texto);
    }
    return new Promise(function (ok, falha) {
      var area = document.createElement('textarea');
      area.value = texto;
      area.style.position = 'fixed';
      area.style.opacity = '0';
      document.body.appendChild(area);
      area.select();
      var certo = false;
      try { certo = document.execCommand('copy'); } catch (e) { certo = false; }
      document.body.removeChild(area);
      if (certo) { ok(); } else { falha(); }
    });
  }
  function avisar(texto) {
    botaoCopiar.textContent = texto;
    if (timer) { clearTimeout(timer); }
    timer = setTimeout(function () { botaoCopiar.textContent = 'Copiar'; }, 1500);
  }
  function copiar() {
    if (corpo === '') { avisar('Gere primeiro'); return; }
    copiarTexto(formatar()).then(function () { avisar('Copiado!'); }, function () { avisar('Erro ao copiar'); });
  }
  botaoGerar.addEventListener('click', gerar);
  botaoCopiar.addEventListener('click', copiar);
  radioSim.addEventListener('change', function () { if (corpo !== '') { mostrar(); } });
  radioNao.addEventListener('change', function () { if (corpo !== '') { mostrar(); } });
})();
</script>

## Como usar a ferramenta

1. Em **Gerar com pontuação?**, escolha **Sim** para receber o número com hífens (por exemplo, `15-123456-7`) ou **Não** para receber apenas os dígitos (por exemplo, `151234567`).
2. Clique em **Gerar Inscrição Estadual** para criar um número válido para o estado do Pará.
3. Clique em **Copiar** para levar o número para a área de transferência e colá-lo no seu sistema ou formulário de teste.
4. Clique em **Gerar Inscrição Estadual** novamente sempre que precisar de um novo número. Se trocar a opção de pontuação depois de gerar, o mesmo número é exibido no novo formato.

Os números são gerados de forma aleatória, seguindo a regra de cálculo do dígito verificador do Pará. Eles servem para estudantes, programadores, analistas e testadores validarem softwares em desenvolvimento. Não pertencem a empresas reais, e o uso indevido dos dados gerados é de responsabilidade de quem os utiliza.

## Entendendo os termos

- **Inscrição Estadual (IE):** número de identificação de uma empresa contribuinte do ICMS perante a Secretaria da Fazenda do seu estado. Cada estado tem o seu próprio formato e regra de validação.
- **Pará (PA):** estado brasileiro para o qual a inscrição é gerada. No Pará, a inscrição estadual tem 9 dígitos e começa com 15.
- **ICMS:** Imposto sobre Circulação de Mercadorias e Serviços, cobrado pelos estados. Empresas que o recolhem precisam de inscrição estadual.
- **Pontuação:** hífens que separam os grupos de dígitos. No Pará, o formato com pontuação é `15-999999-9`.
- **Dígito verificador (DV):** último dígito do número, calculado a partir dos oito primeiros. Ele serve para confirmar que a sequência é válida.
- **Número válido:** número que passa na regra de cálculo do dígito verificador. Isso não significa que ele esteja cadastrado ou pertença a uma empresa real.
- **Dados de teste:** informações fictícias usadas para testar sistemas, formulários e cadastros sem expor dados de verdade.
- **Gerar com pontuação:** opção que define se o resultado sai com hífens ou apenas com números.