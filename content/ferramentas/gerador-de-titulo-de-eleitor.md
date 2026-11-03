---
title: "Gerador de Título de Eleitor"
seoTitle: "Gerador de Título de Eleitor"
description: "Gerador de Título de Eleitor: gere números de título de eleitor válidos para testes. Grátis e online, sem cadastro."
summary: "Gere números de título de eleitor válidos para testes."
date: 2026-11-03
draft: false
category: "documentos"
tags: ["título de eleitor", "eleições", "gerador", "dados de teste", "cpf", "documentos"]
keywords: ["gerador de título de eleitor", "gerador de título de eleitor online", "título de eleitor", "eleições", "gerador"]
---

Escolha o estado e clique em **Gerar Título de Eleitor**. Os números são fictícios e servem apenas para testes.

<div id="gerador-titulo" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🗳️ Gerador de Título de Eleitor</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Escolha o estado e gere um número válido na hora.</p>
<label for="tit-estado" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Qual estado?</label>
<select id="tit-estado" style="width:100%;padding:12px 14px;margin-bottom:20px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<option value="">Qualquer estado (aleatório)</option>
<option value="AC">AC</option>
<option value="AL">AL</option>
<option value="AP">AP</option>
<option value="AM">AM</option>
<option value="BA">BA</option>
<option value="CE">CE</option>
<option value="DF">DF</option>
<option value="GO">GO</option>
<option value="ES">ES</option>
<option value="MA">MA</option>
<option value="MT">MT</option>
<option value="MS">MS</option>
<option value="MG">MG</option>
<option value="PA">PA</option>
<option value="PB">PB</option>
<option value="PR">PR</option>
<option value="PE">PE</option>
<option value="PI">PI</option>
<option value="RJ">RJ</option>
<option value="RN">RN</option>
<option value="RS">RS</option>
<option value="RO">RO</option>
<option value="RR">RR</option>
<option value="SP">SP</option>
<option value="SC">SC</option>
<option value="SE">SE</option>
<option value="TO">TO</option>
</select>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="tit-gerar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Gerar Título de Eleitor</button>
<button type="button" id="tit-copiar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Copiar</button>
</div>
<div id="tit-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="tit-resultado">clique em "Gerar Título de Eleitor".</span><br><small id="tit-detalhe" style="color:#475569;"></small></div>
</div>
<script>
(function () {
  var CODIGOS = { SP: 1, MG: 2, RJ: 3, RS: 4, BA: 5, PR: 6, CE: 7, PE: 8, SC: 9, GO: 10, MA: 11, PB: 12, PA: 13, ES: 14, PI: 15, RN: 16, AL: 17, MT: 18, MS: 19, DF: 20, SE: 21, AM: 22, RO: 23, AC: 24, AP: 25, RR: 26, TO: 27 };
  var SIGLAS = Object.keys(CODIGOS);
  var estado = document.getElementById('tit-estado');
  var resultado = document.getElementById('tit-resultado');
  var detalhe = document.getElementById('tit-detalhe');
  var caixa = document.getElementById('tit-resposta');
  var btnCopiar = document.getElementById('tit-copiar');
  var atual = '';
  function aleatorio(n) { return Math.floor(Math.random() * n); }
  function digito(soma, uf) {
    var resto = soma % 11;
    if (resto === 10) { return 0; }
    if (resto === 0) {
      if (uf === 1) { return 1; }
      if (uf === 2) { return 1; }
    }
    return resto;
  }
  function gerar() {
    var sigla = estado.value;
    if (sigla === '') { sigla = SIGLAS[aleatorio(SIGLAS.length)]; }
    var uf = CODIGOS[sigla];
    var seq = [];
    var soma = 0;
    var i;
    for (i = 0; i !== 8; i++) {
      seq.push(aleatorio(10));
      soma += seq[i] * (i + 2);
    }
    var dv1 = digito(soma, uf);
    var dv2 = digito(Math.floor(uf / 10) * 7 + (uf % 10) * 8 + dv1 * 9, uf);
    var ufTxt = (uf > 9 ? '' : '0') + uf;
    atual = seq.join('') + ufTxt + dv1 + dv2;
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    resultado.style.fontWeight = '700';
    resultado.style.fontSize = '1.2rem';
    resultado.style.letterSpacing = '1px';
    resultado.textContent = atual;
    detalhe.textContent = 'Estado: ' + sigla + ' (código ' + ufTxt + ') | Dígitos verificadores: ' + dv1 + dv2;
  }
  function feito() {
    btnCopiar.textContent = 'Copiado!';
    setTimeout(function () { btnCopiar.textContent = 'Copiar'; }, 1500);
  }
  function alternativa() {
    var t = document.createElement('textarea');
    t.value = atual;
    t.style.position = 'fixed';
    t.style.opacity = '0';
    document.body.appendChild(t);
    t.select();
    try { document.execCommand('copy'); feito(); } catch (e) {}
    document.body.removeChild(t);
  }
  function copiar() {
    if (atual === '') { return; }
    if (navigator.clipboard) {
      navigator.clipboard.writeText(atual).then(feito, alternativa);
    } else {
      alternativa();
    }
  }
  document.getElementById('tit-gerar').addEventListener('click', gerar);
  btnCopiar.addEventListener('click', copiar);
  estado.addEventListener('focus', function () { estado.style.borderColor = '#6366f1'; });
  estado.addEventListener('blur', function () { estado.style.borderColor = '#c7d2fe'; });
})();
</script>

## Como usar o gerador

1. Escolha o **estado** na lista. Se preferir, deixe em "Qualquer estado (aleatório)" para o gerador sortear um.
2. Clique em **Gerar Título de Eleitor** para criar um novo número.
3. Confira o número na caixa **Resposta**, junto com o estado e os dígitos verificadores usados.
4. Clique em **Copiar** para levar o número para a área de transferência e colá-lo no seu sistema de testes.
5. Clique em **Gerar Título de Eleitor** novamente sempre que precisar de outro número.

Os números são gerados de forma aleatória, seguindo as regras de formação do documento. Eles não pertencem a pessoas reais e devem ser usados somente em testes de software, estudos e validações de formulários. O uso indevido dos dados gerados é de responsabilidade de quem os utiliza.

## Entendendo os termos

- **Título de eleitor:** documento da Justiça Eleitoral que comprova a inscrição da pessoa como eleitora no Brasil. Seu número tem 12 dígitos.
- **Número de inscrição:** os 8 primeiros dígitos do título, que identificam a inscrição do eleitor. No gerador, eles são sorteados.
- **Código do estado (UF):** os 2 dígitos seguintes (9º e 10º), que indicam a unidade da federação de origem da inscrição. Por exemplo, 01 é São Paulo e 02 é Minas Gerais.
- **Dígitos verificadores:** os 2 últimos dígitos, calculados a partir dos anteriores para conferir se o número é válido. Eles evitam que números digitados ao acaso sejam aceitos.
- **Número válido:** número que respeita a regra de cálculo dos dígitos verificadores, mesmo sem pertencer a nenhum eleitor real.
- **Dados de teste:** informações fictícias usadas para testar sistemas, formulários e bancos de dados sem expor dados de pessoas reais.
- **Justiça Eleitoral:** conjunto de órgãos responsável por organizar as eleições e emitir o título de eleitor, com o Tribunal Superior Eleitoral (TSE) no topo.