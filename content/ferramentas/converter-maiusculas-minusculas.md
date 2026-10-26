---
title: "Converter Maiúsculas e Minúsculas"
seoTitle: "Converter Maiúsculas e Minúsculas"
description: "Converter Maiúsculas e Minúsculas: troque o texto entre maiúsculas, minúsculas e título. Grátis e online, sem cadastro."
summary: "Troque o texto entre maiúsculas, minúsculas e título."
date: 2026-10-26
draft: false
category: "texto"
tags: ["maiúsculas e minúsculas", "formatação", "texto"]
keywords: ["converter maiúsculas e minúsculas", "converter maiúsculas e minúsculas online", "maiúsculas e minúsculas", "formatação", "texto"]
---
<!--sudah dikerjakan-->

Basta digitar ou colar o texto abaixo e depois clicar no botão da conversão que você quer.

<div id="calc-maiusculas" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🔠 Converter Maiúsculas e Minúsculas</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Digite o texto, escolha a conversão e veja o resultado na hora.</p>
<label for="cmm-texto" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Texto</label>
<textarea id="cmm-texto" rows="6" placeholder="Ex.: digite ou cole seu texto aqui" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;font-family:inherit;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;resize:vertical;"></textarea>
<div style="margin-bottom:20px;padding:14px;background:#ffffff;border:1px solid #c7d2fe;border-radius:12px;">
<p style="margin:0 0 12px;font-weight:600;font-size:0.95rem;color:#3730a3;">Opções da primeira letra de cada palavra</p>
<label for="cmm-minimo" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.9rem;">Ignorar palavras menores que n letra(s)</label>
<input id="cmm-minimo" type="text" inputmode="numeric" value="0" placeholder="Ex.: 3" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:14px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<label for="cmm-ignorar" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.9rem;">Ignorar as palavras (separadas por vírgula)</label>
<input id="cmm-ignorar" type="text" placeholder="Ex.: de, da, do, e" autocomplete="off" style="width:100%;padding:12px 14px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
</div>
<div style="display:flex;gap:10px;flex-wrap:wrap;margin-bottom:10px;">
<button type="button" id="cmm-maiusculas" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">MAIÚSCULAS</button>
<button type="button" id="cmm-minusculas" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">minúsculas</button>
</div>
<div style="display:flex;gap:10px;flex-wrap:wrap;margin-bottom:10px;">
<button type="button" id="cmm-frases" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Primeira Letra da Frase</button>
<button type="button" id="cmm-palavras" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Primeira Letra da Palavra</button>
</div>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="cmm-inverter" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Inverter Maiúsculas/Minúsculas</button>
<button type="button" id="cmm-copiar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Copiar</button>
<button type="button" id="cmm-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="cmm-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="cmm-resultado">digite um texto e clique em uma das conversões.</span>
<textarea id="cmm-saida" rows="6" readonly placeholder="O texto convertido aparece aqui" style="width:100%;margin-top:12px;padding:12px 14px;font-size:1rem;font-family:inherit;border:2px solid #c7d2fe;border-radius:10px;background:#f8fafc;color:#1e293b;box-sizing:border-box;outline:none;resize:vertical;"></textarea>
</div>
</div>
<script>
(function () {
  var texto = document.getElementById('cmm-texto');
  var minimo = document.getElementById('cmm-minimo');
  var ignorar = document.getElementById('cmm-ignorar');
  var saida = document.getElementById('cmm-saida');
  var resultado = document.getElementById('cmm-resultado');
  var caixa = document.getElementById('cmm-resposta');
  var padrao = 'digite um texto e clique em uma das conversões.';
  function status(msg, tipo) {
    if (tipo === 'erro') {
      caixa.style.borderColor = '#fca5a5';
      caixa.style.background = '#fef2f2';
      resultado.style.color = '#b91c1c';
    } else if (tipo === 'ok') {
      caixa.style.borderColor = '#86efac';
      caixa.style.background = '#f0fdf4';
      resultado.style.color = '#166534';
    } else {
      caixa.style.borderColor = '#c7d2fe';
      caixa.style.background = '#ffffff';
      resultado.style.color = '#64748b';
    }
    resultado.textContent = msg;
  }
  function pegarTexto() {
    var t = texto.value;
    if (t.trim() === '') {
      saida.value = '';
      status('digite ou cole um texto no campo acima.', 'erro');
      return null;
    }
    return t;
  }
  function maiusculas(t) {
    return t.toUpperCase();
  }
  function minusculas(t) {
    return t.toLowerCase();
  }
  function frases(t) {
    return t.toLowerCase().replace(/(^\s*|[.!?…]\s+|\n\s*)(\p{L})/gu, function (m, antes, letra) {
      return antes + letra.toUpperCase();
    });
  }
  function palavras(t) {
    var n = parseInt(minimo.value, 10);
    if (isNaN(n)) { n = 0; }
    var lista = ignorar.value.split(',').map(function (p) {
      return p.trim().toLowerCase();
    }).filter(function (p) {
      return p !== '';
    });
    return t.toLowerCase().replace(/[\p{L}\p{M}\p{N}]+/gu, function (w) {
      if (n > w.length) { return w; }
      if (lista.indexOf(w) > -1) { return w; }
      return w.charAt(0).toUpperCase() + w.slice(1);
    });
  }
  function inverter(t) {
    return Array.from(t).map(function (c) {
      var u = c.toUpperCase();
      return c === u ? c.toLowerCase() : u;
    }).join('');
  }
  function aplicar(fn, rotulo) {
    var t = pegarTexto();
    if (t === null) { return; }
    saida.value = fn(t);
    status('texto convertido para ' + rotulo + '.', 'ok');
  }
  function copiar() {
    if (saida.value === '') {
      status('não há resultado para copiar. Converta um texto primeiro.', 'erro');
      return;
    }
    function feito() {
      status('resultado copiado para a área de transferência.', 'ok');
    }
    function alternativa() {
      saida.select();
      var ok = false;
      try { ok = document.execCommand('copy'); } catch (e) { ok = false; }
      if (ok) {
        feito();
      } else {
        status('não foi possível copiar automaticamente. Selecione o texto e copie manualmente.', 'erro');
      }
    }
    if (navigator.clipboard) {
      if (navigator.clipboard.writeText) {
        navigator.clipboard.writeText(saida.value).then(feito, alternativa);
        return;
      }
    }
    alternativa();
  }
  function limpar() {
    texto.value = '';
    saida.value = '';
    minimo.value = '0';
    ignorar.value = '';
    status(padrao, 'neutro');
    texto.focus();
  }
  document.getElementById('cmm-maiusculas').addEventListener('click', function () { aplicar(maiusculas, 'MAIÚSCULAS'); });
  document.getElementById('cmm-minusculas').addEventListener('click', function () { aplicar(minusculas, 'minúsculas'); });
  document.getElementById('cmm-frases').addEventListener('click', function () { aplicar(frases, 'primeira letra maiúscula em cada frase'); });
  document.getElementById('cmm-palavras').addEventListener('click', function () { aplicar(palavras, 'primeira letra maiúscula em cada palavra'); });
  document.getElementById('cmm-inverter').addEventListener('click', function () { aplicar(inverter, 'maiúsculas e minúsculas invertidas'); });
  document.getElementById('cmm-copiar').addEventListener('click', copiar);
  document.getElementById('cmm-limpar').addEventListener('click', limpar);
  [texto, minimo, ignorar].forEach(function (el) {
    el.addEventListener('focus', function () { el.style.borderColor = '#6366f1'; });
    el.addEventListener('blur', function () { el.style.borderColor = '#c7d2fe'; });
  });
})();
</script>

## Como usar a ferramenta

1. Digite ou cole o seu texto no campo **Texto**.
2. Se for usar **Primeira Letra da Palavra**, ajuste as opções, se quiser: informe o tamanho mínimo das palavras e/ou uma lista de palavras a ignorar, separadas por vírgula (por exemplo, `de, da, do, e`).
3. Clique no botão da conversão desejada: **MAIÚSCULAS**, **minúsculas**, **Primeira Letra da Frase**, **Primeira Letra da Palavra** ou **Inverter Maiúsculas/Minúsculas**.
4. Veja o texto convertido no campo de resposta e clique em **Copiar** para levá-lo para a área de transferência.
5. Use o botão **Limpar** para apagar tudo e começar uma nova conversão.

A conversão é feita no seu navegador, e o texto não é enviado para nenhum servidor. Letras com acento, como á, ç e õ, também são convertidas.

## Entendendo os termos

- **Maiúsculas (caixa alta):** todas as letras do texto ficam grandes, como em "OLÁ, MUNDO".
- **Minúsculas (caixa baixa):** todas as letras do texto ficam pequenas, como em "olá, mundo".
- **Primeira Letra da Frase:** deixa o texto em minúsculas e coloca em maiúscula apenas a primeira letra de cada frase, ou seja, a letra que vem no início do texto, depois de ponto final, exclamação, interrogação ou quebra de linha.
- **Primeira Letra da Palavra:** coloca em maiúscula a primeira letra de cada palavra, no estilo de título, como em "Olá, Mundo".
- **Inverter Maiúsculas/Minúsculas:** troca o tipo de cada letra, e o que era maiúsculo vira minúsculo e vice-versa, como em "oLÁ" que vira "OlÁ".
- **Ignorar palavras menores que n letra(s):** palavras com menos letras do que o número informado ficam em minúsculas. Com o valor 3, por exemplo, "de" e "da" não recebem maiúscula. Use 0 para não ignorar nenhuma palavra.
- **Ignorar as palavras:** lista de palavras, separadas por vírgula, que devem continuar em minúsculas na opção Primeira Letra da Palavra, como artigos e preposições ("de, da, do, e").
- **Frase:** trecho do texto que termina em ponto final, exclamação ou interrogação.
- **Caixa do texto:** modo como as letras são escritas, em maiúsculas ou em minúsculas. Em inglês, é chamado de *case*.
- **Copiar:** envia o texto convertido para a área de transferência, pronto para colar em outro lugar.