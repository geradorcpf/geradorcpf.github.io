---
title: "Gerador de Certidões de Casamento"
seoTitle: "Gerador de Certidões de Casamento"
description: "Gerador de Certidões de Casamento: gere números válidos de certidão de casamento. Grátis e online, sem cadastro."
summary: "Gere números válidos de certidão de casamento."
date: 2026-10-28
draft: false
category: "documentos"
tags: ["certidões", "cartório", "gerador", "dados de teste", "documentos"]
keywords: ["gerador de certidões de casamento", "gerador de certidões de casamento online", "certidões", "cartório", "gerador"]
---

Basta escolher as opções abaixo e depois clicar em **Gerar Certidão**.

<div id="calc-certidao" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">💍 Gerador de Certidões de Casamento</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Escolha as opções e gere um número válido na hora.</p>
<label for="cert-pontuacao" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Gerar com pontuação?</label>
<select id="cert-pontuacao" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<option value="sim">Sim</option>
<option value="nao">Não</option>
</select>
<label for="cert-tipo" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Qual certidão?</label>
<select id="cert-tipo" style="width:100%;padding:12px 14px;margin-bottom:20px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<option value="0">Indiferente</option>
<option value="1">Nascimento</option>
<option value="2" selected>Casamento</option>
<option value="3">Casamento Efeito Religioso</option>
<option value="4">Óbito</option>
</select>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="cert-gerar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Gerar Certidão</button>
<button type="button" id="cert-copiar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Copiar</button>
</div>
<div id="cert-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;word-break:break-all;"><strong style="color:#3730a3;">Certidão Gerada:</strong> <span id="cert-resultado">clique em "Gerar Certidão".</span></div>
</div>
<script>
(function () {
  var pontuacao = document.getElementById('cert-pontuacao');
  var tipo = document.getElementById('cert-tipo');
  var resultado = document.getElementById('cert-resultado');
  var caixa = document.getElementById('cert-resposta');
  var ultimo = '';
  function pad(n, tam) { return ('0000000000' + n).slice(-tam); }
  function rand(min, max) { return Math.floor(Math.random() * (max - min + 1)) + min; }
  function soma(digitos) {
    var total = 0;
    var mult = 32 - digitos.length;
    for (var i = 0; i !== digitos.length; i++) {
      total += Number(digitos.charAt(i)) * mult;
      mult += 1;
      if (mult > 10) { mult = 0; }
    }
    return total;
  }
  function digitos(base) {
    var d1 = soma(base) % 11;
    if (d1 > 9) { d1 = 1; }
    var d2 = soma(base + String(d1)) % 11;
    if (d2 > 9) { d2 = 1; }
    return String(d1) + String(d2);
  }
  function mostrar(texto, ok) {
    caixa.style.borderColor = ok ? '#86efac' : '#fca5a5';
    caixa.style.background = ok ? '#f0fdf4' : '#fef2f2';
    resultado.style.color = ok ? '#166534' : '#b91c1c';
    resultado.textContent = texto;
  }
  function gerar() {
    var livroTipo = tipo.value;
    if (livroTipo === '0') { livroTipo = String(rand(1, 4)); }
    var p = [
      pad(rand(100000, 999999), 6),
      '01',
      '55',
      String(rand(2010, new Date().getFullYear())),
      livroTipo,
      pad(rand(1, 99999), 5),
      pad(rand(1, 299), 3),
      pad(rand(1, 500), 7)
    ];
    var dv = digitos(p.join(''));
    if (pontuacao.value === 'sim') {
      ultimo = p.join('.') + '-' + dv;
    } else {
      ultimo = p.join('') + dv;
    }
    mostrar(ultimo, true);
  }
  function copiar() {
    if (ultimo === '') { mostrar('gere uma certidão primeiro.', false); return; }
    var feito = function () { mostrar(ultimo + ' (copiado!)', true); };
    var alternativo = function () {
      var campo = document.createElement('textarea');
      campo.value = ultimo;
      document.body.appendChild(campo);
      campo.select();
      try { document.execCommand('copy'); feito(); } catch (e) { mostrar('não foi possível copiar. Selecione o número manualmente.', false); }
      document.body.removeChild(campo);
    };
    if (navigator.clipboard && navigator.clipboard.writeText) {
      navigator.clipboard.writeText(ultimo).then(feito, alternativo);
    } else {
      alternativo();
    }
  }
  document.getElementById('cert-gerar').addEventListener('click', gerar);
  document.getElementById('cert-copiar').addEventListener('click', copiar);
  [pontuacao, tipo].forEach(function (el) {
    el.addEventListener('focus', function () { el.style.borderColor = '#6366f1'; });
    el.addEventListener('blur', function () { el.style.borderColor = '#c7d2fe'; });
  });
})();
</script>

**Importante:** Os números são gerados de forma aleatória, seguindo a estrutura oficial da matrícula. Eles servem para testar sistemas, formulários e validações, e não correspondem a registros reais. O uso indevido é de responsabilidade do usuário.

## Como usar o gerador

1. Em **Gerar com pontuação?**, escolha **Sim** para o número com pontos e hífen ou **Não** para apenas dígitos.
2. Em **Qual certidão?**, escolha o tipo: **Indiferente**, **Nascimento**, **Casamento**, **Casamento Efeito Religioso** ou **Óbito**.
3. Clique em **Gerar Certidão** para criar um novo número válido.
4. Clique em **Copiar** para levar o número para a área de transferência.
5. Clique em **Gerar Certidão** de novo sempre que precisar de outro número.

## Entendendo os termos

- **Certidão de casamento:** documento emitido pelo cartório que comprova o casamento civil de duas pessoas.
- **Matrícula:** número de 32 dígitos que identifica a certidão e o registro de onde ela foi extraída.
- **Pontuação:** pontos e hífen que separam as partes da matrícula, no formato `XXXXXX.XX.XX.XXXX.X.XXXXX.XXX.XXXXXXX-XX`.
- **Código do cartório:** 6 primeiros dígitos, que identificam o cartório (serventia) responsável pelo registro.
- **Código do acervo:** 2 dígitos que indicam a origem do registro. O valor `01` é usado para acervo próprio do cartório.
- **Código do serviço:** 2 dígitos fixos em `55`, que indicam o serviço de Registro Civil das Pessoas Naturais.
- **Ano de registro:** 4 dígitos com o ano em que o ato foi registrado.
- **Tipo de livro:** 1 dígito que indica o tipo de registro: `1` nascimento, `2` casamento, `3` casamento religioso com efeito civil e `4` óbito.
- **Casamento Efeito Religioso:** casamento celebrado em cerimônia religiosa e depois registrado para ter validade civil.
- **Número do livro:** 5 dígitos que indicam o livro do cartório onde o ato foi registrado.
- **Folha:** 3 dígitos que indicam a página do livro em que o registro está.
- **Termo:** 7 dígitos que indicam o número do registro dentro da folha.
- **Dígito verificador:** 2 últimos dígitos, calculados a partir dos 30 anteriores (módulo 11), usados para conferir se a matrícula é válida.
- **Indiferente:** opção que sorteia o tipo de certidão em vez de fixar um.