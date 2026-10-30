---
title: "Gerador de Inscrição Estadual do Distrito Federal (DF)"
seoTitle: "Gerador de Inscrição Estadual do Distrito Federal (DF)"
description: "Gerador de Inscrição Estadual do Distrito Federal (DF): gere números válidos para testes de software. Grátis e online."
summary: "Gere inscrições estaduais válidas para testes."
date: 2026-10-30
draft: false
category: "documentos"
tags: ["inscrição estadual", "estados", "empresas", "gerador", "dados de teste", "distrito federal", "documentos"]
keywords: ["gerador de inscrição estadual do distrito federal (df)", "gerador de inscrição estadual do distrito federal (df) online", "inscrição estadual", "estados", "empresas"]
compact: true
---
<!--INI SUDAH DIKERJAKAN-->

Basta escolher se quer a pontuação e depois clicar em **Gerar Inscrição Estadual**.

<div id="gerador-ie-df" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🏢 Gerador de Inscrição Estadual do DF</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Gere números válidos do Distrito Federal para testes.</p>
<span style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Gerar com pontuação?</span>
<div style="display:flex;gap:10px;flex-wrap:wrap;margin-bottom:20px;">
<label for="ie-pont-sim" style="flex:1;min-width:120px;display:flex;align-items:center;gap:8px;padding:12px 14px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;cursor:pointer;box-sizing:border-box;"><input id="ie-pont-sim" type="radio" name="ie-pontuacao" value="sim" checked style="margin:0;cursor:pointer;"> Sim</label>
<label for="ie-pont-nao" style="flex:1;min-width:120px;display:flex;align-items:center;gap:8px;padding:12px 14px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;cursor:pointer;box-sizing:border-box;"><input id="ie-pont-nao" type="radio" name="ie-pontuacao" value="nao" style="margin:0;cursor:pointer;"> Não</label>
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
  var botaoGerar = document.getElementById('ie-gerar');
  var botaoCopiar = document.getElementById('ie-copiar');
  var botaoLimpar = document.getElementById('ie-limpar');
  var resultado = document.getElementById('ie-resultado');
  var caixa = document.getElementById('ie-resposta');
  var textoInicial = 'clique em "Gerar Inscrição Estadual".';
  var atual = '';
  function digitoAleatorio() {
    return Math.floor(Math.random() * 10);
  }
  function calcularDV(digitos) {
    var soma = 0;
    var peso = 2;
    digitos.slice().reverse().forEach(function (d) {
      soma += d * peso;
      peso = (peso === 9) ? 2 : peso + 1;
    });
    var dv = 11 - (soma % 11);
    return (dv === 10 || dv === 11) ? 0 : dv;
  }
  function gerar() {
    var base = [0, 7];
    var i = 0;
    while (i !== 6) {
      base.push(digitoAleatorio());
      i += 1;
    }
    base.push(0, 0, 1);
    var dv1 = calcularDV(base);
    var dv2 = calcularDV(base.concat([dv1]));
    var corpo = base.join('');
    var comPontuacao = document.getElementById('ie-pont-sim').checked;
    atual = comPontuacao ? (corpo + '-' + dv1 + dv2) : (corpo + dv1 + dv2);
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    resultado.style.fontSize = '1.2rem';
    resultado.style.fontWeight = '700';
    resultado.style.letterSpacing = '1px';
    resultado.textContent = atual;
  }
  function aviso(msg, cor) {
    resultado.style.color = cor;
    resultado.style.fontSize = '1rem';
    resultado.style.fontWeight = '400';
    resultado.style.letterSpacing = 'normal';
    resultado.textContent = msg;
  }
  function copiarFallback() {
    var area = document.createElement('textarea');
    area.value = atual;
    area.style.position = 'fixed';
    area.style.opacity = '0';
    document.body.appendChild(area);
    area.select();
    var ok = false;
    try { ok = document.execCommand('copy'); } catch (e) { ok = false; }
    document.body.removeChild(area);
    return ok;
  }
  function copiar() {
    if (atual === '') {
      caixa.style.borderColor = '#fca5a5';
      caixa.style.background = '#fef2f2';
      aviso('gere uma inscrição estadual antes de copiar.', '#b91c1c');
      return;
    }
    var original = atual;
    function feito(ok) {
      botaoCopiar.textContent = ok ? 'Copiado!' : 'Falhou';
      setTimeout(function () { botaoCopiar.textContent = 'Copiar'; }, 1500);
    }
    if (navigator.clipboard && navigator.clipboard.writeText) {
      navigator.clipboard.writeText(original).then(function () { feito(true); }, function () { feito(copiarFallback()); });
    } else {
      feito(copiarFallback());
    }
  }
  function limpar() {
    atual = '';
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    aviso(textoInicial, '#64748b');
  }
  botaoGerar.addEventListener('click', gerar);
  botaoCopiar.addEventListener('click', copiar);
  botaoLimpar.addEventListener('click', limpar);
})();
</script>

## Como usar o gerador

1. Escolha **Sim** em "Gerar com pontuação?" se quiser o número com hífen (ex.: `07300001001-09`) ou **Não** para receber só os dígitos (ex.: `0730000100109`).
2. Clique em **Gerar Inscrição Estadual** para criar um novo número válido do Distrito Federal.
3. Clique em **Copiar** para levar o número para a área de transferência e colar no seu sistema ou formulário de teste.
4. Use o botão **Limpar** para apagar o resultado.

Cada clique gera um número diferente. Os números são aleatórios e seguem apenas a regra de formação, então servem para testes de software e **não correspondem a empresas reais**.

## Entendendo os termos

- **Inscrição Estadual (IE):** número de registro de uma empresa na Secretaria da Fazenda do seu estado, usado principalmente para o controle do ICMS.
- **Distrito Federal (DF):** unidade federativa onde fica Brasília. Lá, a inscrição estadual também é conhecida como CF/DF (Cadastro Fiscal do Distrito Federal).
- **ICMS:** Imposto sobre Circulação de Mercadorias e Serviços, cobrado pelos estados e pelo DF.
- **Estrutura do número:** a IE do DF tem 13 dígitos: 11 dígitos de base (começando em 07) seguidos de 2 dígitos verificadores.
- **Dígito verificador:** os dois últimos dígitos, calculados a partir dos anteriores, que servem para conferir se o número é válido.
- **Módulo 11:** cálculo usado para obter cada dígito verificador, com pesos de 2 a 9 aplicados da direita para a esquerda.
- **Pontuação:** formatação do número com hífen antes dos dois dígitos verificadores, para facilitar a leitura.
- **Dados de teste:** informações fictícias, mas com formato válido, usadas para testar sistemas sem expor dados reais.

## Como a inscrição estadual do DF é calculada

O número é montado em três partes: o prefixo **07**, uma sequência aleatória e o código **001**, formando 11 dígitos. Em seguida, calculam-se os dois dígitos verificadores:

1. Multiplique cada dígito, da direita para a esquerda, pelos pesos 2, 3, 4, 5, 6, 7, 8, 9, voltando ao 2 quando acabarem.
2. Some os resultados.
3. Calcule **11 − (soma dividida por 11, pegando o resto)**. Se o resultado for 10 ou 11, o dígito é 0.
4. Repita o processo com os 12 dígitos (incluindo o primeiro dígito verificador) para obter o segundo.

## Exemplo resolvido

Base: `07300001001`.

1. Soma dos produtos: 1×2 + 0×3 + 0×4 + 1×5 + 0×6 + 0×7 + 0×8 + 0×9 + 3×2 + 7×3 + 0×4 = 34.
2. Resto de 34 ÷ 11 = 1, então 11 − 1 = 10, e o primeiro dígito verificador é **0**.
3. Com a base `073000010010`, a soma dos produtos é 46, o resto de 46 ÷ 11 é 2, e 11 − 2 = 9. O segundo dígito é **9**.

**Resposta:** a inscrição estadual completa é `07300001001-09`.