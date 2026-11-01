---
title: "Gerador de Inscrição Estadual do Rio Grande do Norte (RN)"
seoTitle: "Gerador de Inscrição Estadual do Rio Grande do Norte (RN)"
description: "Gerador de Inscrição Estadual do Rio Grande do Norte (RN): gere números válidos para testes de software. Grátis e online."
summary: "Gere inscrições estaduais válidas para testes."
date: 2026-11-01
draft: false
category: "documentos"
tags: ["inscrição estadual", "estados", "empresas", "gerador", "dados de teste", "rio grande do norte", "documentos"]
keywords: ["gerador de inscrição estadual do rio grande do norte (rn)", "gerador de inscrição estadual do rio grande do norte (rn) online", "inscrição estadual", "estados", "empresas"]
compact: true
---

Escolha se deseja o número com ou sem pontuação e depois clique em **Gerar Inscrição Estadual**.

<div id="gerador-ie-rn" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🏢 Gerador de Inscrição Estadual do RN</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Gere números válidos do Rio Grande do Norte para testes de software.</p>
<span style="display:block;margin-bottom:8px;font-weight:600;font-size:0.95rem;">Gerar com pontuação?</span>
<div style="display:flex;gap:10px;flex-wrap:wrap;margin-bottom:20px;">
<label for="ie-pont-sim" style="flex:1;min-width:140px;display:flex;align-items:center;gap:8px;padding:12px 14px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;cursor:pointer;"><input type="radio" id="ie-pont-sim" name="ie-pontuacao" value="sim" checked style="accent-color:#4f46e5;margin:0;"> Sim</label>
<label for="ie-pont-nao" style="flex:1;min-width:140px;display:flex;align-items:center;gap:8px;padding:12px 14px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;cursor:pointer;"><input type="radio" id="ie-pont-nao" name="ie-pontuacao" value="nao" style="accent-color:#4f46e5;margin:0;"> Não</label>
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
  var radioSim = document.getElementById('ie-pont-sim');
  var resultado = document.getElementById('ie-resultado');
  var caixa = document.getElementById('ie-resposta');
  var botaoCopiar = document.getElementById('ie-copiar');
  var ultimo = '';
  var textoInicial = 'clique em "Gerar Inscrição Estadual".';
  function digitoAleatorio() {
    return Math.floor(Math.random() * 10);
  }
  function calcularDigito(base) {
    var soma = 0;
    var i;
    for (i = 0; i !== base.length; i++) {
      soma += base[i] * (9 - i);
    }
    var resto = (soma * 10) % 11;
    if (resto === 10) { return 0; }
    return resto;
  }
  function gerarNumero() {
    var base = [2, 0];
    var i;
    for (i = 0; i !== 6; i++) {
      base.push(digitoAleatorio());
    }
    base.push(calcularDigito(base));
    return base.join('');
  }
  function formatar(n) {
    return n.substring(0, 2) + '.' + n.substring(2, 5) + '.' + n.substring(5, 8) + '-' + n.substring(8, 9);
  }
  function gerar() {
    var numero = gerarNumero();
    if (radioSim.checked) { numero = formatar(numero); }
    ultimo = numero;
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    resultado.textContent = '';
    var forte = document.createElement('strong');
    forte.style.fontSize = '1.2rem';
    forte.style.letterSpacing = '0.5px';
    forte.textContent = numero;
    resultado.appendChild(forte);
    botaoCopiar.textContent = 'Copiar';
  }
  function copiarFallback(texto) {
    var campo = document.createElement('textarea');
    campo.value = texto;
    campo.style.position = 'fixed';
    campo.style.opacity = '0';
    document.body.appendChild(campo);
    campo.select();
    try { document.execCommand('copy'); } catch (e) { }
    document.body.removeChild(campo);
  }
  function copiar() {
    if (ultimo === '') {
      caixa.style.borderColor = '#fca5a5';
      caixa.style.background = '#fef2f2';
      resultado.style.color = '#b91c1c';
      resultado.textContent = 'gere uma inscrição estadual antes de copiar.';
      return;
    }
    if (navigator.clipboard) {
      navigator.clipboard.writeText(ultimo).catch(function () { copiarFallback(ultimo); });
    } else {
      copiarFallback(ultimo);
    }
    botaoCopiar.textContent = 'Copiado!';
  }
  function limpar() {
    ultimo = '';
    radioSim.checked = true;
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    resultado.style.color = '#64748b';
    resultado.textContent = textoInicial;
    botaoCopiar.textContent = 'Copiar';
  }
  document.getElementById('ie-gerar').addEventListener('click', gerar);
  botaoCopiar.addEventListener('click', copiar);
  document.getElementById('ie-limpar').addEventListener('click', limpar);
})();
</script>

## Como usar o gerador

1. Escolha **Sim** em "Gerar com pontuação?" se quiser o número com pontos e hífen (exemplo: `20.123.456-7`), ou **Não** para receber só os dígitos (exemplo: `201234567`).
2. Clique em **Gerar Inscrição Estadual** para criar um novo número válido do Rio Grande do Norte.
3. Clique em **Copiar** para levar o número para a área de transferência e colá-lo no seu sistema ou formulário de teste.
4. Use **Limpar** para apagar o resultado e voltar às opções iniciais. Para obter outro número, basta clicar em gerar de novo.

Os números são criados de forma aleatória, seguindo a regra de composição e de cálculo do dígito verificador usada no estado. Eles servem para testes e desenvolvimento, não para uso em documentos reais.

## Entendendo os termos

- **Inscrição Estadual (IE):** número de registro de uma empresa na Secretaria da Fazenda do estado, usado para controlar o ICMS e emitir notas fiscais.
- **Rio Grande do Norte (RN):** estado cujas regras de formação do número são aplicadas por este gerador. Toda IE potiguar começa com os dígitos 20.
- **Pontuação:** pontos e hífen usados para separar os grupos de dígitos e facilitar a leitura, como em `20.123.456-7`.
- **Dígito verificador:** último dígito do número, calculado a partir dos anteriores para confirmar que a inscrição é válida.
- **Número válido:** número que respeita o formato e passa no cálculo do dígito verificador, mesmo sem estar cadastrado de fato na Receita estadual.
- **Dados de teste:** informações fictícias usadas por programadores, analistas e testadores para verificar o funcionamento de sistemas.
- **Validação:** conferência automática do formato e do dígito verificador de um documento, feita pelo sistema que recebe o número.
- **ICMS:** Imposto sobre Circulação de Mercadorias e Serviços, cobrado pelos estados e ligado à inscrição estadual das empresas.

## Aviso importante

Este gerador existe para ajudar estudantes, programadores, analistas e testadores a obter inscrições estaduais com formato válido para testar softwares em desenvolvimento. O uso indevido dos números gerados é de total responsabilidade de quem os utiliza.