---
title: "Gerador de Inscrição Estadual de Sergipe (SE)"
seoTitle: "Gerador de Inscrição Estadual de Sergipe (SE)"
description: "Gerador de Inscrição Estadual de Sergipe (SE): gere números válidos para testes de software. Grátis e online."
summary: "Gere inscrições estaduais válidas para testes."
date: 2026-11-01
draft: false
category: "documentos"
tags: ["inscrição estadual", "estados", "empresas", "gerador", "dados de teste", "sergipe", "documentos"]
keywords: ["gerador de inscrição estadual de sergipe (se)", "gerador de inscrição estadual de sergipe (se) online", "inscrição estadual", "estados", "empresas"]
compact: true
---
<!--INI SUDAH DIKERJAKAN-->

Basta escolher se deseja a pontuação e depois clicar em **Gerar Inscrição Estadual**.

<div id="gerador-ie-se" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🏢 Gerador de Inscrição Estadual de Sergipe (SE)</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Escolha a opção e gere um número válido na hora.</p>
<span style="display:block;margin-bottom:8px;font-weight:600;font-size:0.95rem;">Gerar com Pontuação?</span>
<div style="display:flex;gap:10px;flex-wrap:wrap;margin-bottom:20px;">
<label for="ie-pontuacao-sim" style="flex:1;min-width:140px;display:flex;align-items:center;gap:8px;padding:12px 14px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;cursor:pointer;"><input type="radio" id="ie-pontuacao-sim" name="ie-pontuacao" value="sim" checked style="accent-color:#4f46e5;margin:0;cursor:pointer;"> Sim</label>
<label for="ie-pontuacao-nao" style="flex:1;min-width:140px;display:flex;align-items:center;gap:8px;padding:12px 14px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;cursor:pointer;"><input type="radio" id="ie-pontuacao-nao" name="ie-pontuacao" value="nao" style="accent-color:#4f46e5;margin:0;cursor:pointer;"> Não</label>
</div>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="ie-gerar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Gerar Inscrição Estadual</button>
<button type="button" id="ie-copiar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Copiar</button>
</div>
<div id="ie-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="ie-resultado">clique em "Gerar Inscrição Estadual".</span></div>
</div>
<script>
(function () {
  var radios = document.getElementsByName('ie-pontuacao');
  var resultado = document.getElementById('ie-resultado');
  var caixa = document.getElementById('ie-resposta');
  var botaoCopiar = document.getElementById('ie-copiar');
  var base = '';
  var dv = '';
  function comPontuacao() {
    var sim = true;
    Array.prototype.forEach.call(radios, function (r) {
      if (r.checked) { sim = (r.value === 'sim'); }
    });
    return sim;
  }
  function formatar() {
    return comPontuacao() ? base + '-' + dv : base + dv;
  }
  function mostrar() {
    if (base === '') { return; }
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    resultado.textContent = formatar();
    resultado.style.fontSize = '1.2rem';
    resultado.style.fontWeight = '700';
  }
  function gerar() {
    var digitos = [];
    var soma = 0;
    var i;
    for (i = 0; i !== 8; i++) {
      digitos.push(Math.floor(Math.random() * 10));
      soma += digitos[i] * (9 - i);
    }
    var d = 11 - (soma % 11);
    if (d === 10 || d === 11) { d = 0; }
    base = digitos.join('');
    dv = String(d);
    mostrar();
  }
  function copiarTexto(texto) {
    if (navigator.clipboard && navigator.clipboard.writeText) {
      return navigator.clipboard.writeText(texto);
    }
    return new Promise(function (resolve, reject) {
      try {
        var ta = document.createElement('textarea');
        ta.value = texto;
        ta.style.position = 'fixed';
        ta.style.opacity = '0';
        document.body.appendChild(ta);
        ta.select();
        var ok = document.execCommand('copy');
        document.body.removeChild(ta);
        if (ok) { resolve(); } else { reject(new Error('copy')); }
      } catch (e) { reject(e); }
    });
  }
  function copiar() {
    if (base === '') { gerar(); }
    copiarTexto(formatar()).then(function () {
      botaoCopiar.textContent = 'Copiado!';
      setTimeout(function () { botaoCopiar.textContent = 'Copiar'; }, 1500);
    }, function () {
      botaoCopiar.textContent = 'Falhou';
      setTimeout(function () { botaoCopiar.textContent = 'Copiar'; }, 1500);
    });
  }
  document.getElementById('ie-gerar').addEventListener('click', gerar);
  botaoCopiar.addEventListener('click', copiar);
  Array.prototype.forEach.call(radios, function (r) {
    r.addEventListener('change', mostrar);
  });
})();
</script>

## Como usar o gerador

1. Em **Gerar com Pontuação?**, escolha **Sim** para o número com hífen (por exemplo, `27123456-3`) ou **Não** para apenas os dígitos (por exemplo, `271234563`).
2. Clique em **Gerar Inscrição Estadual** (ou no mesmo botão novamente para gerar outro número).
3. Veja o número válido no campo **Resposta**.
4. Clique em **Copiar** para levar o número para a área de transferência e colar onde precisar.

Se você trocar a opção de pontuação depois de gerar, o mesmo número é exibido no novo formato, sem precisar gerar de novo. Os números são sorteados de forma aleatória, seguindo a regra de cálculo usada em Sergipe.

**Importante:** este gerador serve para ajudar estudantes, programadores, analistas e testadores a obter números válidos para testar softwares em desenvolvimento. Os números são fictícios e não representam empresas reais. O uso indevido dos dados gerados é de responsabilidade de quem os utiliza.

## Entendendo os termos

- **Inscrição Estadual (IE):** número de registro de uma empresa na Secretaria da Fazenda do estado, exigido de contribuintes do ICMS (comércio, indústria e alguns serviços).
- **Sergipe (SE):** estado brasileiro cujas regras de formação da inscrição estadual são usadas neste gerador.
- **SEFAZ:** Secretaria de Estado da Fazenda, órgão que emite e controla as inscrições estaduais.
- **ICMS:** Imposto sobre Circulação de Mercadorias e Serviços, cobrado pelos estados. É ele que torna a inscrição estadual obrigatória.
- **Pontuação:** os sinais gráficos do número. Em Sergipe, o formato é `99999999-9` (oito dígitos, hífen e um dígito verificador).
- **Dígito verificador (DV):** último dígito do número, calculado a partir dos oito primeiros. Serve para conferir se o número foi digitado corretamente.
- **Módulo 11:** cálculo usado para obter o dígito verificador. Cada um dos oito dígitos é multiplicado por pesos de 9 a 2, os resultados são somados e o DV é 11 menos o resto da divisão da soma por 11 (se der 10 ou 11, o DV é 0).
- **Número válido:** número que respeita a regra de formação e passa na verificação do dígito, mas que não está necessariamente cadastrado na SEFAZ.
- **Dados de teste:** informações fictícias usadas para testar sistemas, formulários e validações sem expor dados reais.
- **Copiar:** botão que envia o número exibido para a área de transferência do seu dispositivo.