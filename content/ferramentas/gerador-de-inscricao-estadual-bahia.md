---
title: "Gerador de Inscrição Estadual da Bahia (BA)"
seoTitle: "Gerador de Inscrição Estadual da Bahia (BA)"
description: "Gerador de Inscrição Estadual da Bahia (BA): gere números válidos para testes de software. Grátis e online."
summary: "Gere inscrições estaduais válidas para testes."
date: 2026-10-30
draft: false
category: "documentos"
tags: ["inscrição estadual", "estados", "empresas", "gerador", "dados de teste", "bahia", "documentos"]
keywords: ["gerador de inscrição estadual da bahia (ba)", "gerador de inscrição estadual da bahia (ba) online", "inscrição estadual", "estados", "empresas"]
compact: true
---

Basta escolher se deseja a pontuação e clicar em **Gerar Inscrição Estadual**.

<div id="gerador-ie-ba" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🏢 Gerador de Inscrição Estadual da Bahia (BA)</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Gere números válidos para testar o seu software.</p>
<label for="ie-ba-pontuacao" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Gerar com pontuação?</label>
<select id="ie-ba-pontuacao" style="width:100%;padding:12px 14px;margin-bottom:20px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<option value="sim">Sim</option>
<option value="nao">Não</option>
</select>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="ie-ba-gerar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Gerar Inscrição Estadual</button>
<button type="button" id="ie-ba-copiar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Copiar</button>
</div>
<div id="ie-ba-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="ie-ba-resultado">clique em "Gerar Inscrição Estadual".</span></div>
</div>
<script>
(function () {
  var pontuacao = document.getElementById('ie-ba-pontuacao');
  var resultado = document.getElementById('ie-ba-resultado');
  var caixa = document.getElementById('ie-ba-resposta');
  var btnCopiar = document.getElementById('ie-ba-copiar');
  var atual = '';
  function digitoVerificador(digitos, modulo) {
    var peso = digitos.length + 1;
    var soma = 0;
    digitos.forEach(function (d) {
      soma += d * peso;
      peso -= 1;
    });
    var resto = soma % modulo;
    var dv = modulo - resto;
    return dv >= 10 ? 0 : dv;
  }
  function gerar() {
    var base = [];
    for (var i = 0; i !== 6; i++) {
      base.push(Math.floor(Math.random() * 10));
    }
    var modulo = [6, 7, 9].indexOf(base[0]) > -1 ? 11 : 10;
    var dv2 = digitoVerificador(base, modulo);
    var dv1 = digitoVerificador(base.concat([dv2]), modulo);
    var corpo = base.join('');
    var sufixo = String(dv1) + String(dv2);
    atual = pontuacao.value === 'sim' ? corpo + '-' + sufixo : corpo + sufixo;
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    resultado.style.fontWeight = '700';
    resultado.style.fontSize = '1.2rem';
    resultado.textContent = atual;
  }
  function copiadoComSucesso() {
    btnCopiar.textContent = 'Copiado!';
    setTimeout(function () { btnCopiar.textContent = 'Copiar'; }, 1500);
  }
  function copiarAlternativo() {
    var campo = document.createElement('textarea');
    campo.value = atual;
    campo.style.position = 'fixed';
    campo.style.opacity = '0';
    document.body.appendChild(campo);
    campo.select();
    try {
      document.execCommand('copy');
      copiadoComSucesso();
    } catch (e) {}
    document.body.removeChild(campo);
  }
  function copiar() {
    if (atual === '') { return; }
    if (navigator.clipboard && navigator.clipboard.writeText) {
      navigator.clipboard.writeText(atual).then(copiadoComSucesso, copiarAlternativo);
    } else {
      copiarAlternativo();
    }
  }
  document.getElementById('ie-ba-gerar').addEventListener('click', gerar);
  btnCopiar.addEventListener('click', copiar);
  pontuacao.addEventListener('focus', function () { pontuacao.style.borderColor = '#6366f1'; });
  pontuacao.addEventListener('blur', function () { pontuacao.style.borderColor = '#c7d2fe'; });
})();
</script>

## Como usar o gerador

1. Em **Gerar com pontuação?**, escolha **Sim** para receber o número com hífen (por exemplo, `123456-63`) ou **Não** para receber apenas os dígitos (`12345663`).
2. Clique em **Gerar Inscrição Estadual** para criar um novo número. Você pode clicar quantas vezes quiser.
3. Veja o número no campo **Resposta**.
4. Clique em **Copiar** para levar o número para a área de transferência e colá-lo no seu sistema ou formulário de teste.

Os números são gerados de forma aleatória, seguindo a regra de cálculo da Bahia, e servem apenas para testes de software. Eles não pertencem a empresas reais, e o uso indevido dos dados gerados é de responsabilidade de quem os utiliza.

## Entendendo os termos

- **Inscrição Estadual (IE):** número que identifica uma empresa contribuinte do ICMS no cadastro da Secretaria da Fazenda do seu estado.
- **Bahia (BA):** estado para o qual o número é gerado. Cada estado brasileiro tem o seu próprio formato e a sua própria regra de cálculo.
- **Pontuação:** o hífen que separa o corpo do número dos dois últimos dígitos, como em `123456-63`.
- **Dígito verificador:** dígito calculado a partir dos demais, usado para conferir se o número é válido. Na Bahia, os dois últimos dígitos da inscrição são verificadores.
- **Módulo 10 e módulo 11:** operações de divisão usadas no cálculo dos dígitos verificadores. A escolha entre elas depende do primeiro dígito do número.
- **Número válido:** número que passa na regra de cálculo do estado, mesmo sem estar cadastrado em nenhuma empresa real.
- **Dados de teste:** informações fictícias usadas por programadores, analistas e testadores para verificar o funcionamento de sistemas.