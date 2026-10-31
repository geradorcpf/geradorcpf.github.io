---
title: "Gerador de Inscrição Estadual do Mato Grosso do Sul (MS)"
seoTitle: "Gerador de Inscrição Estadual do Mato Grosso do Sul (MS)"
description: "Gerador de Inscrição Estadual do Mato Grosso do Sul (MS): gere números válidos para testes de software. Grátis e online."
summary: "Gere inscrições estaduais válidas para testes."
date: 2026-10-31
draft: false
category: "documentos"
tags: ["inscrição estadual", "estados", "empresas", "gerador", "dados de teste", "mato grosso do sul", "documentos"]
keywords: ["gerador de inscrição estadual do mato grosso do sul (ms)", "gerador de inscrição estadual do mato grosso do sul (ms) online", "inscrição estadual", "estados", "empresas"]
compact: true
---

Basta escolher se deseja a pontuação e depois clicar em **Gerar Inscrição Estadual**.

<div id="calc-ie-ms" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🏢 Gerador de Inscrição Estadual (MS)</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Escolha a opção e gere um número válido para testes.</p>
<span style="display:block;margin-bottom:8px;font-weight:600;font-size:0.95rem;">Gerar com pontuação?</span>
<div style="display:flex;gap:10px;flex-wrap:wrap;margin-bottom:20px;">
<label for="ie-pont-sim" style="flex:1;min-width:140px;display:flex;align-items:center;gap:8px;padding:12px 14px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;cursor:pointer;"><input type="radio" id="ie-pont-sim" name="ie-pont" value="sim" checked style="accent-color:#4f46e5;margin:0;"> Sim</label>
<label for="ie-pont-nao" style="flex:1;min-width:140px;display:flex;align-items:center;gap:8px;padding:12px 14px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;cursor:pointer;"><input type="radio" id="ie-pont-nao" name="ie-pont" value="nao" style="accent-color:#4f46e5;margin:0;"> Não</label>
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
  var timer = null;
  function digito() { return Math.floor(Math.random() * 10); }
  function calcularDv(d) {
    var soma = 0;
    for (var i = 0; i !== 8; i++) { soma += d[i] * (9 - i); }
    var resto = soma % 11;
    if (resto === 0) { return 0; }
    var dv = 11 - resto;
    return dv === 10 ? 0 : dv;
  }
  function formatar(s) {
    if (!sim.checked) { return s; }
    return s.substr(0, 2) + '.' + s.substr(2, 3) + '.' + s.substr(5, 3) + '-' + s.substr(8, 1);
  }
  function mostrar() {
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    resultado.style.fontWeight = '700';
    resultado.style.fontSize = '1.3rem';
    resultado.style.letterSpacing = '1px';
    resultado.textContent = formatar(atual);
  }
  function gerar() {
    var d = [2, 8];
    for (var i = 0; i !== 6; i++) { d.push(digito()); }
    d.push(calcularDv(d));
    atual = d.join('');
    mostrar();
  }
  function aviso(txt) {
    btnCopiar.textContent = txt;
    clearTimeout(timer);
    timer = setTimeout(function () { btnCopiar.textContent = 'Copiar'; }, 1500);
  }
  function copiarFallback(texto) {
    var ta = document.createElement('textarea');
    ta.value = texto;
    ta.style.position = 'fixed';
    ta.style.opacity = '0';
    document.body.appendChild(ta);
    ta.select();
    var ok = false;
    try { ok = document.execCommand('copy'); } catch (e) { ok = false; }
    document.body.removeChild(ta);
    aviso(ok ? 'Copiado!' : 'Falhou');
  }
  function copiar() {
    if (atual === '') { aviso('Gere primeiro'); return; }
    var texto = formatar(atual);
    if (navigator.clipboard && navigator.clipboard.writeText) {
      navigator.clipboard.writeText(texto).then(function () { aviso('Copiado!'); }, function () { copiarFallback(texto); });
    } else {
      copiarFallback(texto);
    }
  }
  function limpar() {
    atual = '';
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    resultado.style.color = '#64748b';
    resultado.style.fontWeight = '400';
    resultado.style.fontSize = '1rem';
    resultado.style.letterSpacing = 'normal';
    resultado.textContent = 'clique em "Gerar Inscrição Estadual".';
  }
  document.getElementById('ie-gerar').addEventListener('click', gerar);
  btnCopiar.addEventListener('click', copiar);
  document.getElementById('ie-limpar').addEventListener('click', limpar);
  [sim, document.getElementById('ie-pont-nao')].forEach(function (el) {
    el.addEventListener('change', function () { if (atual !== '') { mostrar(); } });
  });
})();
</script>

## Como usar o gerador

1. Escolha **Sim** em "Gerar com pontuação?" para receber o número formatado (por exemplo, `28.123.456-7`) ou **Não** para receber só os dígitos (`281234567`).
2. Clique em **Gerar Inscrição Estadual** para criar um novo número válido.
3. Clique em **Copiar** para levar o resultado para a área de transferência e colar no seu sistema ou formulário de teste.
4. Use o botão **Limpar** para apagar o resultado. Você pode clicar em **Gerar Inscrição Estadual** quantas vezes quiser; cada clique cria um número diferente.

Se você trocar a opção de pontuação depois de gerar, o número exibido é reformatado na hora, sem mudar os dígitos.

## Entendendo os termos

- **Inscrição Estadual (IE):** número de cadastro de uma empresa na Secretaria da Fazenda do seu estado. Em geral é exigido de contribuintes do ICMS, como comércio, indústria e alguns serviços.
- **Mato Grosso do Sul (MS):** estado cujas regras de formação da inscrição estadual este gerador segue. Cada estado brasileiro tem o seu próprio formato e cálculo.
- **ICMS:** Imposto sobre Circulação de Mercadorias e Serviços, imposto estadual que motiva a existência da inscrição estadual.
- **Pontuação:** pontos e hífen usados para facilitar a leitura. No MS o formato é `28.XXX.XXX-D`. Sem pontuação, ficam apenas os 9 dígitos.
- **Prefixo 28:** os dois primeiros dígitos de toda inscrição estadual do MS.
- **Dígito verificador (DV):** último dígito do número, calculado a partir dos 8 anteriores. Serve para detectar erros de digitação e validar o número.
- **Módulo 11:** método de cálculo do dígito verificador, baseado no resto de uma divisão por 11.
- **Número válido:** número que passa na regra matemática de validação. Isso não significa que ele esteja cadastrado na Sefaz ou pertença a uma empresa real.
- **Dados de teste:** informações fictícias usadas para testar sistemas, formulários e bancos de dados sem expor dados reais.

## Como o número é calculado

A inscrição estadual do MS tem 9 dígitos: o prefixo **28**, seis dígitos aleatórios e o dígito verificador. O cálculo do DV segue estes passos:

1. Multiplique os 8 primeiros dígitos pelos pesos 9, 8, 7, 6, 5, 4, 3 e 2, nessa ordem.
2. Some todos os resultados.
3. Calcule o resto da divisão da soma por 11.
4. Se o resto for 0, o DV é 0. Caso contrário, o DV é 11 menos o resto. Se esse valor for 10, o DV passa a ser 0.

### Exemplo resolvido

Vamos calcular o DV da base **28000000**.

1. Multiplique pelos pesos: 2×9 + 8×8 + 0×7 + 0×6 + 0×5 + 0×4 + 0×3 + 0×2.
2. Some: 18 + 64 = 82.
3. Divida por 11: 82 = 7×11 + 5, então o resto é 5.
4. Calcule o DV: 11 − 5 = 6.

**Resposta:** a inscrição estadual completa é **280000006**, ou **28.000.000-6** com pontuação.

## Aviso importante

Este gerador serve para ajudar estudantes, programadores, analistas e testadores a obter inscrições estaduais com formato válido para testar softwares em desenvolvimento. Os números são aleatórios e não representam empresas reais. O uso indevido dos dados gerados é de responsabilidade de quem os utiliza.