---
title: "Gerador de Inscrição Estadual do Rio Grande do Sul (RS)"
seoTitle: "Gerador de Inscrição Estadual do Rio Grande do Sul (RS)"
description: "Gerador de Inscrição Estadual do Rio Grande do Sul (RS): gere números válidos para testes de software. Grátis e online."
summary: "Gere inscrições estaduais válidas para testes."
date: 2026-11-01
draft: false
category: "documentos"
tags: ["inscrição estadual", "estados", "empresas", "gerador", "dados de teste", "rio grande do sul", "documentos"]
keywords: ["gerador de inscrição estadual do rio grande do sul (rs)", "gerador de inscrição estadual do rio grande do sul (rs) online", "inscrição estadual", "estados", "empresas"]
compact: true
---

Basta escolher se deseja a pontuação e depois clicar em **Gerar Inscrição Estadual**.

<div id="gerador-ie-rs" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🧾 Gerador de Inscrição Estadual do RS</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Gere números válidos do Rio Grande do Sul para testes de software.</p>
<span style="display:block;margin-bottom:8px;font-weight:600;font-size:0.95rem;">Gerar com pontuação?</span>
<div style="display:flex;gap:10px;flex-wrap:wrap;margin-bottom:20px;">
<label for="ie-pont-sim" style="flex:1;min-width:120px;display:flex;align-items:center;gap:8px;padding:12px 14px;font-size:1rem;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;color:#1e293b;cursor:pointer;box-sizing:border-box;"><input type="radio" id="ie-pont-sim" name="ie-pontuacao" value="sim" checked style="accent-color:#4f46e5;margin:0;"> Sim</label>
<label for="ie-pont-nao" style="flex:1;min-width:120px;display:flex;align-items:center;gap:8px;padding:12px 14px;font-size:1rem;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;color:#1e293b;cursor:pointer;box-sizing:border-box;"><input type="radio" id="ie-pont-nao" name="ie-pontuacao" value="nao" style="accent-color:#4f46e5;margin:0;"> Não</label>
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
  var resultado = document.getElementById('ie-resultado');
  var caixa = document.getElementById('ie-resposta');
  var btnCopiar = document.getElementById('ie-copiar');
  var textoPadrao = 'clique em "Gerar Inscrição Estadual".';
  var atual = '';
  function pad(n, tam) {
    var s = String(n);
    while (s.length !== tam) { s = '0' + s; }
    return s;
  }
  function aleatorio(max) {
    return Math.floor(Math.random() * max);
  }
  function calcularDv(base) {
    var pesos = [2, 9, 8, 7, 6, 5, 4, 3, 2];
    var soma = 0;
    for (var i = 0; i !== 9; i++) {
      soma += Number(base.charAt(i)) * pesos[i];
    }
    var dv = 11 - (soma % 11);
    if (dv >= 10) { dv = 0; }
    return dv;
  }
  function gerar() {
    var municipio = pad(aleatorio(467) + 1, 3);
    var sequencia = pad(aleatorio(1000000), 6);
    var base = municipio + sequencia;
    var numero = base + String(calcularDv(base));
    var comPontuacao = document.getElementById('ie-pont-sim').checked;
    if (comPontuacao) {
      atual = numero.substring(0, 3) + '/' + numero.substring(3);
    } else {
      atual = numero;
    }
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    resultado.style.fontSize = '1.3rem';
    resultado.style.fontWeight = '700';
    resultado.style.letterSpacing = '1px';
    resultado.textContent = atual;
  }
  function copiar() {
    if (atual === '') { return; }
    function ok() {
      btnCopiar.textContent = 'Copiado!';
      setTimeout(function () { btnCopiar.textContent = 'Copiar'; }, 1500);
    }
    if (navigator.clipboard && navigator.clipboard.writeText) {
      navigator.clipboard.writeText(atual).then(ok);
      return;
    }
    var campo = document.createElement('textarea');
    campo.value = atual;
    document.body.appendChild(campo);
    campo.select();
    try {
      document.execCommand('copy');
      ok();
    } catch (e) {}
    document.body.removeChild(campo);
  }
  function limpar() {
    atual = '';
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    resultado.style.color = '#64748b';
    resultado.style.fontSize = '1rem';
    resultado.style.fontWeight = '400';
    resultado.style.letterSpacing = 'normal';
    resultado.textContent = textoPadrao;
  }
  document.getElementById('ie-gerar').addEventListener('click', gerar);
  btnCopiar.addEventListener('click', copiar);
  document.getElementById('ie-limpar').addEventListener('click', limpar);
})();
</script>

## Como usar o gerador

1. Escolha **Sim** em "Gerar com pontuação?" se quiser o número no formato com barra (por exemplo, `224/3658792`), ou **Não** para receber apenas os dígitos (por exemplo, `2243658792`).
2. Clique em **Gerar Inscrição Estadual** para criar um novo número válido do Rio Grande do Sul.
3. Clique em **Copiar** para levar o número para a área de transferência e colá-lo no seu sistema ou formulário de teste.
4. Use o botão **Limpar** para apagar o resultado e começar de novo. A cada clique em **Gerar Inscrição Estadual** um novo número aleatório é criado.

Os números são gerados de forma aleatória, respeitando a regra de formação da inscrição estadual do RS. Servem apenas para testes de software, e o uso indevido dos dados gerados é de responsabilidade de quem os utiliza.

## Entendendo os termos

- **Inscrição Estadual (IE):** número de identificação de uma empresa contribuinte do ICMS perante a Secretaria da Fazenda do seu estado. Cada estado tem sua própria regra de formação.
- **Rio Grande do Sul (RS):** estado cuja regra é usada por este gerador. A inscrição estadual do RS tem 10 dígitos.
- **Pontuação:** separador visual do número. No RS, a barra aparece após o terceiro dígito, no formato `000/0000000`.
- **Código do município:** os três primeiros dígitos, que identificam o município de cadastro da empresa (de 001 a 467).
- **Número sequencial:** os seis dígitos seguintes, que distinguem uma empresa da outra dentro do mesmo município.
- **Dígito verificador (DV):** o último dígito, calculado a partir dos nove anteriores. Ele serve para conferir se o número é válido.
- **Número válido:** número cujo dígito verificador confere com o cálculo oficial. Isso não significa que a empresa exista de fato.
- **Dados de teste:** informações fictícias usadas por estudantes, programadores e testadores para verificar o funcionamento de sistemas.

## Como o dígito verificador é calculado

Cada um dos nove primeiros dígitos é multiplicado por um peso, na ordem **2, 9, 8, 7, 6, 5, 4, 3, 2**. Some os resultados e divida a soma por 11. O dígito verificador é **11 menos o resto** dessa divisão. Se o resultado for 10 ou 11, o dígito verificador passa a ser **0**.

## Exemplo resolvido

Considere a base `224365879`.

1. Multiplique cada dígito pelo seu peso: 2×2 + 2×9 + 4×8 + 3×7 + 6×6 + 5×5 + 8×4 + 7×3 + 9×2.
2. Some os resultados: 4 + 18 + 32 + 21 + 36 + 25 + 32 + 21 + 18 = 207.
3. Divida por 11: 207 ÷ 11 deixa resto 9.
4. Calcule o dígito: 11 − 9 = 2.

**Resposta:** a inscrição estadual completa é **224/3658792**.