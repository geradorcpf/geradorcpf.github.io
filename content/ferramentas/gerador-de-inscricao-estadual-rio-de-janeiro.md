---
title: "Gerador de Inscrição Estadual do Rio de Janeiro (RJ)"
seoTitle: "Gerador de Inscrição Estadual do Rio de Janeiro (RJ)"
description: "Gerador de Inscrição Estadual do Rio de Janeiro (RJ): gere números válidos para testes de software. Grátis e online."
summary: "Gere inscrições estaduais válidas para testes."
date: 2026-11-01
draft: false
category: "documentos"
tags: ["inscrição estadual", "estados", "empresas", "gerador", "dados de teste", "rio de janeiro", "documentos"]
keywords: ["gerador de inscrição estadual do rio de janeiro (rj)", "gerador de inscrição estadual do rio de janeiro (rj) online", "inscrição estadual", "estados", "empresas"]
compact: true
---

Escolha se deseja o número com ou sem pontuação e clique em **Gerar Inscrição Estadual**.

<div id="gerador-ie-rj" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🏢 Gerador de Inscrição Estadual do RJ</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Gere números válidos do Rio de Janeiro para testes de software.</p>
<span style="display:block;margin-bottom:8px;font-weight:600;font-size:0.95rem;">Gerar com pontuação?</span>
<div style="display:flex;gap:20px;margin-bottom:20px;flex-wrap:wrap;">
<label for="ie-pontuacao-sim" style="display:flex;align-items:center;gap:8px;font-size:1rem;cursor:pointer;"><input type="radio" id="ie-pontuacao-sim" name="ie-pontuacao" value="sim" checked style="width:18px;height:18px;accent-color:#4f46e5;cursor:pointer;">Sim</label>
<label for="ie-pontuacao-nao" style="display:flex;align-items:center;gap:8px;font-size:1rem;cursor:pointer;"><input type="radio" id="ie-pontuacao-nao" name="ie-pontuacao" value="nao" style="width:18px;height:18px;accent-color:#4f46e5;cursor:pointer;">Não</label>
</div>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="ie-gerar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Gerar Inscrição Estadual</button>
<button type="button" id="ie-copiar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Copiar</button>
</div>
<div id="ie-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="ie-resultado">clique em "Gerar Inscrição Estadual".</span></div>
</div>
<script>
(function () {
  var resultado = document.getElementById('ie-resultado');
  var caixa = document.getElementById('ie-resposta');
  var botaoCopiar = document.getElementById('ie-copiar');
  var atual = '';
  function digitoVerificador(digitos) {
    var pesos = [2, 7, 6, 5, 4, 3, 2];
    var soma = 0;
    for (var i = 0; i !== 7; i++) {
      soma += digitos[i] * pesos[i];
    }
    var resto = soma % 11;
    return resto > 1 ? 11 - resto : 0;
  }
  function gerar() {
    var digitos = [1 + Math.floor(Math.random() * 9)];
    for (var i = 1; i !== 7; i++) {
      digitos.push(Math.floor(Math.random() * 10));
    }
    digitos.push(digitoVerificador(digitos));
    var s = digitos.join('');
    var comPontuacao = document.getElementById('ie-pontuacao-sim').checked;
    if (comPontuacao) {
      s = s.substring(0, 2) + '.' + s.substring(2, 5) + '.' + s.substring(5, 7) + '-' + s.substring(7);
    }
    return s;
  }
  function mostrar() {
    atual = gerar();
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    resultado.innerHTML = '<strong id="ie-numero" style="font-size:1.3rem;letter-spacing:1px;"></strong>';
    document.getElementById('ie-numero').textContent = atual;
    botaoCopiar.textContent = 'Copiar';
  }
  function copiar() {
    if (atual === '') { return; }
    function ok() { botaoCopiar.textContent = 'Copiado!'; }
    if (navigator.clipboard) {
      navigator.clipboard.writeText(atual).then(ok, function () { alternativa(); });
    } else {
      alternativa();
    }
    function alternativa() {
      var t = document.createElement('textarea');
      t.value = atual;
      t.style.position = 'fixed';
      t.style.opacity = '0';
      document.body.appendChild(t);
      t.select();
      try { document.execCommand('copy'); ok(); } catch (e) { }
      document.body.removeChild(t);
    }
  }
  document.getElementById('ie-gerar').addEventListener('click', mostrar);
  botaoCopiar.addEventListener('click', copiar);
  document.getElementById('ie-pontuacao-sim').addEventListener('change', function () { if (atual !== '') { mostrar(); } });
  document.getElementById('ie-pontuacao-nao').addEventListener('change', function () { if (atual !== '') { mostrar(); } });
})();
</script>

## Como usar o gerador

1. Escolha **Sim** em "Gerar com pontuação?" para obter o número no formato `XX.XXX.XX-X`, ou **Não** para receber apenas os 8 dígitos.
2. Clique em **Gerar Inscrição Estadual** para criar um novo número válido do Rio de Janeiro.
3. Clique em **Copiar** para levar o número para a área de transferência.
4. Clique em **Gerar Inscrição Estadual** novamente sempre que precisar de outro número.

Os números são gerados de forma aleatória, respeitando a regra de cálculo do dígito verificador do estado. Eles servem apenas para testes de software e não pertencem a empresas reais. O uso indevido dos dados gerados é de responsabilidade de quem os utiliza.

## Entendendo os termos

- **Inscrição Estadual (IE):** número de identificação de empresas contribuintes do ICMS, emitido pela Secretaria de Fazenda de cada estado.
- **RJ:** sigla do estado do Rio de Janeiro. A inscrição estadual do RJ tem 8 dígitos.
- **Pontuação:** pontos e hífen usados para separar os dígitos, como em `12.345.67-4`.
- **Dígito verificador:** último dígito do número, calculado a partir dos sete primeiros para confirmar que a inscrição é válida.
- **Número válido:** número que passa na regra matemática de validação, mesmo sem existir de fato na Receita estadual.
- **ICMS:** Imposto sobre Circulação de Mercadorias e Serviços, cobrado pelos estados.
- **Dados de teste:** informações fictícias usadas por programadores e testadores para verificar formulários e sistemas.

## Como o dígito verificador é calculado

Os sete primeiros dígitos são multiplicados, da esquerda para a direita, pelos pesos **2, 7, 6, 5, 4, 3 e 2**. Some os resultados e divida a soma por 11. Se o resto for 0 ou 1, o dígito verificador é **0**. Nos demais casos, ele é **11 menos o resto**.

## Exemplo resolvido

Vamos calcular o dígito verificador para a base `1234567`.

1. Multiplique pelos pesos: 1×2 + 2×7 + 3×6 + 4×5 + 5×4 + 6×3 + 7×2.
2. Some: 2 + 14 + 18 + 20 + 20 + 18 + 14 = 106.
3. Divida por 11: o resto é 7 (106 = 9 × 11 + 7).
4. Como o resto é maior que 1, o dígito verificador é 11 − 7 = 4.

**Resposta:** a inscrição estadual completa é `12345674`, ou **12.345.67-4** com pontuação.