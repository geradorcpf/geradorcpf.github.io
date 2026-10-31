---
title: "Gerador de Inscrição Estadual de Minas Gerais (MG)"
seoTitle: "Gerador de Inscrição Estadual de Minas Gerais (MG)"
description: "Gerador de Inscrição Estadual de Minas Gerais (MG): gere números válidos para testes de software. Grátis e online."
summary: "Gere inscrições estaduais válidas para testes."
date: 2026-10-31
draft: false
category: "documentos"
tags: ["inscrição estadual", "estados", "empresas", "gerador", "dados de teste", "minas gerais", "documentos"]
keywords: ["gerador de inscrição estadual de minas gerais (mg)", "gerador de inscrição estadual de minas gerais (mg) online", "inscrição estadual", "estados", "empresas"]
compact: true
---

Basta escolher se deseja a pontuação e depois clicar em **Gerar Inscrição Estadual**.

<div id="gerador-ie-mg" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🏢 Gerador de Inscrição Estadual de MG</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Gere números válidos de Minas Gerais para testes de software.</p>
<span style="display:block;margin-bottom:8px;font-weight:600;font-size:0.95rem;">Gerar com pontuação?</span>
<div style="display:flex;gap:10px;flex-wrap:wrap;margin-bottom:20px;">
<label for="ie-pontuacao-sim" style="flex:1;min-width:120px;display:flex;align-items:center;gap:8px;padding:12px 14px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;cursor:pointer;box-sizing:border-box;"><input id="ie-pontuacao-sim" type="radio" name="ie-pontuacao" value="sim" checked style="accent-color:#4f46e5;margin:0;"> Sim</label>
<label for="ie-pontuacao-nao" style="flex:1;min-width:120px;display:flex;align-items:center;gap:8px;padding:12px 14px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;cursor:pointer;box-sizing:border-box;"><input id="ie-pontuacao-nao" type="radio" name="ie-pontuacao" value="nao" style="accent-color:#4f46e5;margin:0;"> Não</label>
</div>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="ie-gerar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Gerar Inscrição Estadual</button>
<button type="button" id="ie-copiar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Copiar</button>
</div>
<div id="ie-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="ie-resultado">clique em "Gerar Inscrição Estadual".</span></div>
</div>
<script>
(function () {
  var simRadio = document.getElementById('ie-pontuacao-sim');
  var naoRadio = document.getElementById('ie-pontuacao-nao');
  var resultado = document.getElementById('ie-resultado');
  var caixa = document.getElementById('ie-resposta');
  var btnCopiar = document.getElementById('ie-copiar');
  var numeroAtual = '';
  function aleatorio(max) { return Math.floor(Math.random() * max); }
  function preencher(valor, tamanho) {
    var s = String(valor);
    while (s.length !== tamanho) { s = '0' + s; }
    return s;
  }
  function digitos(texto) {
    var r = [];
    for (var i = 0; i !== texto.length; i++) { r.push(Number(texto.charAt(i))); }
    return r;
  }
  function primeiroDV(base) {
    var d = digitos(base);
    d.splice(3, 0, 0);
    var soma = 0;
    for (var i = 0; i !== d.length; i++) {
      var p = d[i] * (i % 2 === 0 ? 1 : 2);
      soma += Math.floor(p / 10) + (p % 10);
    }
    return (10 - (soma % 10)) % 10;
  }
  function segundoDV(base) {
    var pesos = [3, 2, 11, 10, 9, 8, 7, 6, 5, 4, 3, 2];
    var d = digitos(base);
    var soma = 0;
    for (var i = 0; i !== d.length; i++) { soma += d[i] * pesos[i]; }
    var resto = soma % 11;
    return (resto === 0 || resto === 1) ? 0 : 11 - resto;
  }
  function formatar(puro) {
    if (!simRadio.checked) { return puro; }
    return puro.slice(0, 3) + '.' + puro.slice(3, 9) + '.' + puro.slice(9, 11) + '/' + puro.slice(11, 13);
  }
  var numeroPuro = '';
  function mostrar() {
    if (numeroPuro === '') { return; }
    numeroAtual = formatar(numeroPuro);
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    resultado.textContent = '';
    var forte = document.createElement('strong');
    forte.style.fontSize = '1.2rem';
    forte.textContent = numeroAtual;
    resultado.appendChild(forte);
  }
  function gerar() {
    var municipio = preencher(aleatorio(853) + 1, 3);
    var sequencial = preencher(aleatorio(1000000), 6);
    var ordem = preencher(aleatorio(100), 2);
    var base = municipio + sequencial + ordem;
    var dv1 = primeiroDV(base);
    var dv2 = segundoDV(base + String(dv1));
    numeroPuro = base + String(dv1) + String(dv2);
    mostrar();
  }
  function feedbackCopia() {
    btnCopiar.textContent = 'Copiado!';
    setTimeout(function () { btnCopiar.textContent = 'Copiar'; }, 1500);
  }
  function copiaAlternativa() {
    var campo = document.createElement('textarea');
    campo.value = numeroAtual;
    campo.style.position = 'fixed';
    campo.style.opacity = '0';
    document.body.appendChild(campo);
    campo.select();
    try { document.execCommand('copy'); feedbackCopia(); } catch (e) {}
    document.body.removeChild(campo);
  }
  function copiar() {
    if (numeroAtual === '') { return; }
    if (navigator.clipboard && navigator.clipboard.writeText) {
      navigator.clipboard.writeText(numeroAtual).then(feedbackCopia, copiaAlternativa);
    } else {
      copiaAlternativa();
    }
  }
  document.getElementById('ie-gerar').addEventListener('click', gerar);
  btnCopiar.addEventListener('click', copiar);
  simRadio.addEventListener('change', mostrar);
  naoRadio.addEventListener('change', mostrar);
})();
</script>

## Como usar o gerador

1. Em **Gerar com pontuação?**, escolha **Sim** para receber o número com pontos, barra e separadores (ex.: `062.307.904/0081`) ou **Não** para receber apenas os 13 dígitos (ex.: `0623079040081`).
2. Clique em **Gerar Inscrição Estadual** para criar um novo número válido de Minas Gerais.
3. Clique em **Copiar** para levar o número para a área de transferência e colá-lo no seu sistema ou formulário de teste.
4. Se mudar a opção de pontuação depois de gerar, o mesmo número é reformatado na hora. Clique em gerar novamente quando quiser outro número.

Os números são criados de forma aleatória, respeitando a regra de cálculo dos dígitos verificadores de MG. Eles servem apenas para **testes de software**: não pertencem a empresas reais, e o uso indevido é de responsabilidade de quem os utiliza.

## Entendendo os termos

- **Inscrição Estadual (IE):** número de registro de uma empresa na Secretaria da Fazenda do estado, usado principalmente por contribuintes do ICMS (imposto sobre circulação de mercadorias e serviços).
- **Minas Gerais (MG):** cada estado brasileiro tem seu próprio formato e cálculo de inscrição estadual. Em MG, o número tem 13 dígitos.
- **Pontuação:** os pontos e a barra que separam os grupos de dígitos. O formato de MG com pontuação é `AAA.BBBBBB.CC/DD`.
- **Código do município (AAA):** os 3 primeiros dígitos, que identificam o município de MG onde a empresa foi registrada.
- **Número sequencial (BBBBBB):** grupo de 6 dígitos que identifica o contribuinte dentro do município.
- **Número de ordem (CC):** grupo de 2 dígitos que diferencia os estabelecimentos ou o registro dentro do mesmo número base.
- **Dígitos verificadores (DD):** os 2 últimos dígitos, calculados a partir dos anteriores. Eles servem para conferir se o número é válido, evitando erros de digitação.
- **Número válido:** número que passa no cálculo dos dígitos verificadores. Ele é válido apenas na estrutura, o que não significa que exista de fato na Receita estadual.
- **Dados de teste:** informações fictícias usadas por programadores, analistas e testadores para validar cadastros e sistemas sem expor dados reais.