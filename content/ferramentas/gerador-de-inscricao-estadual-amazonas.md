---
title: "Gerador de Inscrição Estadual do Amazonas (AM)"
seoTitle: "Gerador de Inscrição Estadual do Amazonas (AM)"
description: "Gerador de Inscrição Estadual do Amazonas (AM): gere números válidos para testes de software. Grátis e online."
summary: "Gere inscrições estaduais válidas para testes."
date: 2026-10-30
draft: false
category: "documentos"
tags: ["inscrição estadual", "estados", "empresas", "gerador", "dados de teste", "amazonas", "documentos"]
keywords: ["gerador de inscrição estadual do amazonas (am)", "gerador de inscrição estadual do amazonas (am) online", "inscrição estadual", "estados", "empresas"]
compact: true
---

Basta escolher se quer a pontuação e depois clicar em **Gerar Inscrição Estadual**.

<div id="gerador-ie-am" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🏢 Gerador de Inscrição Estadual do Amazonas (AM)</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Gere números válidos para testes de software.</p>
<label style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Gerar com pontuação?</label>
<div style="display:flex;gap:20px;margin-bottom:20px;">
<label for="ie-pont-sim" style="display:flex;align-items:center;gap:6px;font-size:1rem;cursor:pointer;"><input type="radio" id="ie-pont-sim" name="ie-pontuacao" value="sim" checked style="accent-color:#4f46e5;width:18px;height:18px;"> Sim</label>
<label for="ie-pont-nao" style="display:flex;align-items:center;gap:6px;font-size:1rem;cursor:pointer;"><input type="radio" id="ie-pont-nao" name="ie-pontuacao" value="nao" style="accent-color:#4f46e5;width:18px;height:18px;"> Não</label>
</div>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="ie-gerar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Gerar Inscrição Estadual</button>
<button type="button" id="ie-copiar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Copiar</button>
<button type="button" id="ie-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="ie-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="ie-resultado">clique em "Gerar Inscrição Estadual".</span></div>
</div>
<script>
(function () {
  var sim = document.getElementById('ie-pont-sim');
  var resultado = document.getElementById('ie-resultado');
  var caixa = document.getElementById('ie-resposta');
  var btnCopiar = document.getElementById('ie-copiar');
  var atual = '';
  function digitoVerificador(d) {
    var soma = 0;
    for (var i = 0; i !== 8; i++) { soma += d[i] * (9 - i); }
    var resto = soma % 11;
    return (resto === 0 || resto === 1) ? 0 : 11 - resto;
  }
  function gerar() {
    var d = [0, 4];
    for (var i = 2; i !== 8; i++) { d.push(Math.floor(Math.random() * 10)); }
    var dv = digitoVerificador(d);
    var corpo = d.join('');
    if (sim.checked) {
      atual = corpo.slice(0, 2) + '.' + corpo.slice(2, 5) + '.' + corpo.slice(5, 8) + '-' + dv;
    } else {
      atual = corpo + dv;
    }
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    resultado.innerHTML = '<strong style="font-size:1.3rem;letter-spacing:1px;">' + atual + '</strong>';
    btnCopiar.textContent = 'Copiar';
  }
  function copiar() {
    if (atual === '') { return; }
    function ok() { btnCopiar.textContent = 'Copiado!'; }
    function alternativo() {
      var t = document.createElement('textarea');
      t.value = atual;
      document.body.appendChild(t);
      t.select();
      try { document.execCommand('copy'); ok(); } catch (e) {}
      document.body.removeChild(t);
    }
    if (navigator.clipboard && navigator.clipboard.writeText) {
      navigator.clipboard.writeText(atual).then(ok, alternativo);
    } else {
      alternativo();
    }
  }
  function limpar() {
    atual = '';
    sim.checked = true;
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    resultado.style.color = '#64748b';
    resultado.textContent = 'clique em "Gerar Inscrição Estadual".';
    btnCopiar.textContent = 'Copiar';
  }
  document.getElementById('ie-gerar').addEventListener('click', gerar);
  btnCopiar.addEventListener('click', copiar);
  document.getElementById('ie-limpar').addEventListener('click', limpar);
})();
</script>

## Como usar o gerador

1. Escolha **Sim** em "Gerar com pontuação?" para receber o número formatado (por exemplo, `04.123.456-7`) ou **Não** para receber apenas os dígitos.
2. Clique em **Gerar Inscrição Estadual** para criar um novo número válido.
3. Clique em **Copiar** para levar o número para a área de transferência e colá-lo no seu sistema ou formulário de teste.
4. Use o botão **Limpar** para apagar o resultado e voltar às opções iniciais.

Cada clique gera um número diferente, criado de forma aleatória, mas respeitando a regra de cálculo do dígito verificador do Amazonas. Use os números apenas em testes de software: eles são válidos na regra, mas não pertencem a nenhuma empresa real.

## Entendendo os termos

- **Inscrição Estadual (IE):** número de identificação de empresas contribuintes do ICMS, atribuído pela Secretaria da Fazenda de cada estado.
- **Amazonas (AM):** estado para o qual o gerador segue a regra de formação da inscrição estadual. No Amazonas, ela tem 9 dígitos.
- **Pontuação:** pontos e hífen usados na formatação do número. No Amazonas, o formato é `99.999.999-9`.
- **Dígito verificador (DV):** último dígito do número, calculado a partir dos 8 primeiros para confirmar que a inscrição é válida.
- **Módulo 11:** cálculo em que cada dígito é multiplicado por um peso (de 9 a 2), os resultados são somados e o total é dividido por 11 para obter o dígito verificador.
- **Dados de teste:** informações fictícias usadas por estudantes, programadores e testadores para validar sistemas em desenvolvimento.
- **Copiar:** botão que envia o número gerado para a área de transferência do seu dispositivo.

## Como o dígito verificador é calculado

1. Multiplique os 8 primeiros dígitos pelos pesos 9, 8, 7, 6, 5, 4, 3 e 2, nessa ordem.
2. Some todos os resultados.
3. Divida a soma por 11 e pegue o resto.
4. Se o resto for 0 ou 1, o dígito verificador é **0**. Caso contrário, o dígito verificador é **11 − resto**.

## Exemplo resolvido

Considere os 8 primeiros dígitos **04123456**.

1. Multiplique pelos pesos: 0×9 + 4×8 + 1×7 + 2×6 + 3×5 + 4×4 + 5×3 + 6×2.
2. Calcule: 0 + 32 + 7 + 12 + 15 + 16 + 15 + 12 = 109.
3. Divida por 11: 109 ÷ 11 = 9, com resto 10.
4. Como o resto é maior que 1, o dígito verificador é 11 − 10 = 1.

**Resposta:** a inscrição estadual é **04.123.456-1** (ou **041234561** sem pontuação).

> **Importante:** este gerador tem a intenção de ajudar estudantes, programadores, analistas e testadores a obter inscrições estaduais válidas para testar seus softwares. A má utilização dos dados gerados é de total responsabilidade do usuário.