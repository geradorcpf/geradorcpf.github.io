---
title: "Gerador de Inscrição Estadual do Ceará (CE)"
seoTitle: "Gerador de Inscrição Estadual do Ceará (CE)"
description: "Gerador de Inscrição Estadual do Ceará (CE): gere números válidos para testes de software. Grátis e online."
summary: "Gere inscrições estaduais válidas para testes."
date: 2026-10-30
draft: false
category: "documentos"
tags: ["inscrição estadual", "estados", "empresas", "gerador", "dados de teste", "ceará", "documentos"]
keywords: ["gerador de inscrição estadual do ceará (ce)", "gerador de inscrição estadual do ceará (ce) online", "inscrição estadual", "estados", "empresas"]
compact: true
---

Basta escolher se quer a pontuação e depois clicar em **Gerar Inscrição Estadual**.

<div id="calc-ie-ceara" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🏢 Gerador de Inscrição Estadual do Ceará (CE)</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Gere números válidos para testar seus sistemas.</p>
<span style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Gerar com pontuação?</span>
<div style="display:flex;gap:10px;flex-wrap:wrap;margin-bottom:20px;">
<label for="ie-com-pontuacao" style="flex:1;min-width:120px;display:flex;align-items:center;gap:8px;padding:12px 14px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;cursor:pointer;"><input type="radio" id="ie-com-pontuacao" name="ie-pontuacao" value="sim" checked style="accent-color:#4f46e5;margin:0;cursor:pointer;"> Sim</label>
<label for="ie-sem-pontuacao" style="flex:1;min-width:120px;display:flex;align-items:center;gap:8px;padding:12px 14px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;cursor:pointer;"><input type="radio" id="ie-sem-pontuacao" name="ie-pontuacao" value="nao" style="accent-color:#4f46e5;margin:0;cursor:pointer;"> Não</label>
</div>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="ie-gerar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Gerar Inscrição Estadual</button>
<button type="button" id="ie-copiar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Copiar</button>
<button type="button" id="ie-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="ie-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="ie-resultado">escolha a opção e clique em "Gerar Inscrição Estadual".</span></div>
</div>
<script>
(function () {
  var comPontuacao = document.getElementById('ie-com-pontuacao');
  var resultado = document.getElementById('ie-resultado');
  var caixa = document.getElementById('ie-resposta');
  var textoInicial = 'escolha a opção e clique em "Gerar Inscrição Estadual".';
  var ultimo = '';
  function digitoAleatorio() {
    return Math.floor(Math.random() * 10);
  }
  function calcularDV(base) {
    var soma = 0;
    base.split('').forEach(function (d, i) {
      soma += Number(d) * (9 - i);
    });
    var dv = 11 - (soma % 11);
    if (dv === 10 || dv === 11) { dv = 0; }
    return dv;
  }
  function gerarNumero() {
    var base = '06';
    while (base.length !== 8) {
      base += String(digitoAleatorio());
    }
    return base + String(calcularDV(base));
  }
  function formatar(numero) {
    return numero.slice(0, 8) + '-' + numero.slice(8);
  }
  function mostrar(msg, borda, fundo, cor) {
    caixa.style.borderColor = borda;
    caixa.style.background = fundo;
    resultado.style.color = cor;
    resultado.textContent = msg;
  }
  function gerar() {
    var numero = gerarNumero();
    ultimo = comPontuacao.checked ? formatar(numero) : numero;
    mostrar(ultimo, '#86efac', '#f0fdf4', '#166534');
    resultado.style.fontWeight = '700';
    resultado.style.fontSize = '1.2rem';
  }
  function copiarFallback(texto) {
    var area = document.createElement('textarea');
    area.value = texto;
    area.style.position = 'fixed';
    area.style.opacity = '0';
    document.body.appendChild(area);
    area.select();
    try { document.execCommand('copy'); } catch (e) {}
    document.body.removeChild(area);
  }
  function copiar() {
    if (ultimo === '') {
      mostrar('gere uma inscrição estadual antes de copiar.', '#fca5a5', '#fef2f2', '#b91c1c');
      return;
    }
    if (navigator.clipboard && navigator.clipboard.writeText) {
      navigator.clipboard.writeText(ultimo).catch(function () { copiarFallback(ultimo); });
    } else {
      copiarFallback(ultimo);
    }
    var botao = document.getElementById('ie-copiar');
    botao.textContent = 'Copiado!';
    setTimeout(function () { botao.textContent = 'Copiar'; }, 1500);
  }
  function limpar() {
    ultimo = '';
    comPontuacao.checked = true;
    resultado.style.fontWeight = '400';
    resultado.style.fontSize = '1rem';
    mostrar(textoInicial, '#c7d2fe', '#ffffff', '#64748b');
  }
  document.getElementById('ie-gerar').addEventListener('click', gerar);
  document.getElementById('ie-copiar').addEventListener('click', copiar);
  document.getElementById('ie-limpar').addEventListener('click', limpar);
})();
</script>

## Como usar o gerador

1. Escolha **Sim** ou **Não** em "Gerar com pontuação?" para definir o formato do número.
2. Clique em **Gerar Inscrição Estadual** para criar um novo número válido do Ceará.
3. Clique em **Copiar** para levar o número para a área de transferência e colar onde precisar.
4. Use o botão **Limpar** para apagar o resultado e voltar às opções iniciais.

Cada clique em **Gerar Inscrição Estadual** cria um número diferente. Os números são aleatórios e seguem a regra de cálculo do dígito verificador do Ceará, por isso servem para testes de software, mas não pertencem a empresas reais.

## Entendendo os termos

- **Inscrição Estadual (IE):** número de cadastro de uma empresa na Secretaria da Fazenda do estado, usado principalmente para contribuintes de ICMS.
- **Gerar com pontuação:** define se o número sai com hífen separando o dígito verificador (`06000001-5`) ou só com dígitos (`060000015`).
- **Ceará (CE):** estado para o qual o número é gerado. Cada estado tem seu próprio tamanho e regra de cálculo.
- **Dígito verificador (DV):** último dígito do número, calculado a partir dos anteriores para detectar erros de digitação.
- **Número válido:** número que passa na conta do dígito verificador, mesmo que não esteja registrado em nenhuma empresa.
- **Dados de teste:** informações fictícias usadas para testar formulários, validações e sistemas em desenvolvimento.
- **ICMS:** Imposto sobre Circulação de Mercadorias e Serviços, cobrado pelos estados e que exige a Inscrição Estadual.

## Como é calculada a Inscrição Estadual do Ceará

A inscrição do Ceará tem 9 dígitos: 8 de base (que normalmente começam com **06**) e 1 dígito verificador. O cálculo segue estes passos:

1. Multiplique cada um dos 8 primeiros dígitos pelos pesos 9, 8, 7, 6, 5, 4, 3 e 2, nessa ordem.
2. Some todos os produtos.
3. Divida a soma por 11 e guarde o resto.
4. Subtraia o resto de 11. Se o resultado for 10 ou 11, o dígito verificador é 0.

## Exemplo resolvido

Vamos calcular o dígito verificador da base **06000001**.

1. Multiplique cada dígito pelo seu peso: 0×9 + 6×8 + 0×7 + 0×6 + 0×5 + 0×4 + 0×3 + 1×2.
2. Some os produtos: 0 + 48 + 0 + 0 + 0 + 0 + 0 + 2 = 50.
3. Resto da divisão por 11: 50 ÷ 11 deixa resto 6.
4. Dígito verificador: 11 − 6 = 5.

**Resposta:** a inscrição estadual é **06000001-5** (ou **060000015**, sem pontuação).

> **Importante:** este gerador serve para estudantes, programadores, analistas e testadores que precisam de números válidos para testar seus softwares. O uso indevido dos dados gerados é de responsabilidade do usuário.