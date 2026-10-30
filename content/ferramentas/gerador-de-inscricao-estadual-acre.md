---
title: "Gerador de Inscrição Estadual do Acre (AC)"
seoTitle: "Gerador de Inscrição Estadual do Acre (AC)"
description: "Gerador de Inscrição Estadual do Acre (AC): gere números válidos para testes de software. Grátis e online."
summary: "Gere inscrições estaduais válidas para testes."
date: 2026-10-30
draft: false
category: "documentos"
tags: ["inscrição estadual", "estados", "empresas", "gerador", "dados de teste", "acre", "documentos"]
keywords: ["gerador de inscrição estadual do acre (ac)", "gerador de inscrição estadual do acre (ac) online", "inscrição estadual", "estados", "empresas"]
compact: true
---

Basta escolher se deseja a pontuação e clicar em **Gerar Inscrição Estadual**.

<div id="gerador-ie-acre" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🏢 Gerador de Inscrição Estadual do Acre (AC)</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Gere números válidos para testes de software.</p>
<span style="display:block;margin-bottom:8px;font-weight:600;font-size:0.95rem;">Gerar com Pontuação?</span>
<div style="display:flex;gap:20px;margin-bottom:20px;flex-wrap:wrap;">
<label for="ie-ac-pont-sim" style="display:flex;align-items:center;gap:8px;font-size:1rem;cursor:pointer;"><input type="radio" name="ie-ac-pont" id="ie-ac-pont-sim" value="sim" checked style="width:18px;height:18px;accent-color:#4f46e5;cursor:pointer;">Sim</label>
<label for="ie-ac-pont-nao" style="display:flex;align-items:center;gap:8px;font-size:1rem;cursor:pointer;"><input type="radio" name="ie-ac-pont" id="ie-ac-pont-nao" value="nao" style="width:18px;height:18px;accent-color:#4f46e5;cursor:pointer;">Não</label>
</div>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="ie-ac-gerar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Gerar Inscrição Estadual</button>
<button type="button" id="ie-ac-copiar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Copiar</button>
</div>
<div id="ie-ac-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="ie-ac-resultado">clique em "Gerar Inscrição Estadual".</span></div>
</div>
<script>
(function () {
  var radSim = document.getElementById('ie-ac-pont-sim');
  var btnGerar = document.getElementById('ie-ac-gerar');
  var btnCopiar = document.getElementById('ie-ac-copiar');
  var resultado = document.getElementById('ie-ac-resultado');
  var caixa = document.getElementById('ie-ac-resposta');
  var atual = '';
  function digitoVerificador(digitos, pesos) {
    var soma = 0;
    for (var i = 0; i !== digitos.length; i++) { soma += digitos[i] * pesos[i]; }
    var dv = (11 - (soma % 11)) % 11;
    if (dv === 10) { dv = 0; }
    return dv;
  }
  function gerarNumero() {
    var d = [0, 1];
    for (var i = 0; i !== 9; i++) { d.push(Math.floor(Math.random() * 10)); }
    d.push(digitoVerificador(d, [4, 3, 2, 9, 8, 7, 6, 5, 4, 3, 2]));
    d.push(digitoVerificador(d, [5, 4, 3, 2, 9, 8, 7, 6, 5, 4, 3, 2]));
    return d.join('');
  }
  function formatar(s) {
    return s.slice(0, 2) + '.' + s.slice(2, 5) + '.' + s.slice(5, 8) + '/' + s.slice(8, 11) + '-' + s.slice(11, 13);
  }
  function gerar() {
    var numero = gerarNumero();
    if (radSim.checked) { numero = formatar(numero); }
    atual = numero;
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    resultado.style.fontWeight = '700';
    resultado.style.fontSize = '1.2rem';
    resultado.style.fontFamily = 'ui-monospace,SFMono-Regular,Menlo,Consolas,monospace';
    resultado.style.letterSpacing = '0.5px';
    resultado.textContent = numero;
    btnCopiar.textContent = 'Copiar';
  }
  function copiadoOk() {
    btnCopiar.textContent = 'Copiado!';
    setTimeout(function () { btnCopiar.textContent = 'Copiar'; }, 1500);
  }
  function copiarFallback() {
    var campo = document.createElement('textarea');
    campo.value = atual;
    campo.setAttribute('readonly', 'readonly');
    campo.style.position = 'fixed';
    campo.style.opacity = '0';
    document.body.appendChild(campo);
    campo.select();
    try { document.execCommand('copy'); copiadoOk(); } catch (e) { btnCopiar.textContent = 'Erro ao copiar'; }
    document.body.removeChild(campo);
  }
  function copiar() {
    if (atual === '') { gerar(); }
    if (navigator.clipboard) {
      if (navigator.clipboard.writeText) {
        navigator.clipboard.writeText(atual).then(copiadoOk, copiarFallback);
        return;
      }
    }
    copiarFallback();
  }
  btnGerar.addEventListener('click', gerar);
  btnCopiar.addEventListener('click', copiar);
})();
</script>

## Como usar o gerador

1. Em **Gerar com Pontuação?**, escolha **Sim** para receber o número formatado (por exemplo, `01.004.823/001-12`) ou **Não** para receber apenas os dígitos.
2. Clique em **Gerar Inscrição Estadual** para criar um novo número válido para o Acre. A cada clique, um novo número aleatório é gerado.
3. Clique em **Copiar** para enviar o número para a área de transferência e colá-lo no sistema que você está testando.

Os números são gerados de forma aleatória, seguindo a regra de formação da Inscrição Estadual do Acre. Eles servem para testes de software e não correspondem a empresas reais.

## Entendendo os termos

- **Inscrição Estadual (IE):** número de registro de uma empresa na Secretaria da Fazenda do seu estado, usado para contribuintes do ICMS (imposto sobre circulação de mercadorias e serviços).
- **Acre (AC):** estado cuja regra de formação é usada neste gerador. Cada estado brasileiro tem seu próprio tamanho e cálculo de Inscrição Estadual.
- **Pontuação:** pontos, barra e hífen usados para separar os grupos de dígitos. No Acre, o formato é `NN.NNN.NNN/NNN-NN`.
- **Prefixo 01:** os dois primeiros dígitos da Inscrição Estadual do Acre, que identificam o tipo de cadastro e são sempre `01`.
- **Dígitos verificadores:** os dois últimos dígitos, calculados a partir dos anteriores, que servem para conferir se o número é válido.
- **Número válido:** número que respeita a estrutura e o cálculo dos dígitos verificadores. Isso não significa que ele esteja cadastrado na Receita Estadual.
- **Dados de teste:** informações fictícias usadas por estudantes, programadores, analistas e testadores para verificar o funcionamento de sistemas em desenvolvimento.

**Importante:** a má utilização dos dados gerados aqui é de total responsabilidade do usuário.