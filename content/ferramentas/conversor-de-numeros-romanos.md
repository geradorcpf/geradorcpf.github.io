---
title: "Conversor de Números Romanos"
seoTitle: "Conversor de Números Romanos"
description: "Conversor de Números Romanos: converta números romanos em arábicos e vice-versa. Grátis e online, sem cadastro."
summary: "Converta números romanos em arábicos e vice-versa."
date: 2026-10-26
draft: false
category: "matematica"
tags: ["números romanos", "conversão", "matemática"]
keywords: ["conversor de números romanos", "conversor de números romanos online", "números romanos", "conversão", "matemática"]
---
<!--sudah dikerjakan-->

Basta digitar um número decimal ou um número romano abaixo e depois clicar no botão de conversão correspondente.

<div id="conv-romanos" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🏛️ Conversor de Números Romanos</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Converta decimal em romano e vice-versa (de 1 a 3999).</p>
<label for="rom-decimal" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Decimal</label>
<input id="rom-decimal" type="text" inputmode="numeric" placeholder="Ex.: 1994" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:12px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<button type="button" id="rom-para-romano" style="width:100%;padding:13px 18px;margin-bottom:20px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Converter para Romano</button>
<label for="rom-romano" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Romano</label>
<input id="rom-romano" type="text" inputmode="text" placeholder="Ex.: MCMXCIV" autocomplete="off" autocapitalize="characters" style="width:100%;padding:12px 14px;margin-bottom:12px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="rom-para-decimal" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Converter para Decimal</button>
<button type="button" id="rom-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="rom-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="rom-resultado">preencha um dos campos e clique no botão de conversão.</span></div>
</div>
<script>
(function () {
  var dec = document.getElementById('rom-decimal');
  var rom = document.getElementById('rom-romano');
  var resultado = document.getElementById('rom-resultado');
  var caixa = document.getElementById('rom-resposta');
  var VALORES = [1000, 900, 500, 400, 100, 90, 50, 40, 10, 9, 5, 4, 1];
  var SIMBOLOS = ['M', 'CM', 'D', 'CD', 'C', 'XC', 'L', 'XL', 'X', 'IX', 'V', 'IV', 'I'];
  var PADRAO = /^M{0,3}(CM|CD|D?C{0,3})(XC|XL|L?X{0,3})(IX|IV|V?I{0,3})$/;
  var MSG_INICIAL = 'preencha um dos campos e clique no botão de conversão.';
  function estilo(borda, fundo, cor) {
    caixa.style.borderColor = borda;
    caixa.style.background = fundo;
    resultado.style.color = cor;
  }
  function erro(msg) {
    estilo('#fca5a5', '#fef2f2', '#b91c1c');
    resultado.textContent = msg;
  }
  function sucesso(rotulo, valor, detalhe) {
    estilo('#86efac', '#f0fdf4', '#166534');
    resultado.textContent = '';
    var texto = document.createTextNode(rotulo + ' ');
    var forte = document.createElement('strong');
    forte.style.fontSize = '1.2rem';
    forte.textContent = valor;
    var quebra = document.createElement('br');
    var pequeno = document.createElement('small');
    pequeno.style.color = '#475569';
    pequeno.textContent = detalhe;
    resultado.appendChild(texto);
    resultado.appendChild(forte);
    resultado.appendChild(quebra);
    resultado.appendChild(pequeno);
  }
  function paraRomano() {
    var t = dec.value.trim();
    if (t === '') { erro('digite um número decimal.'); return; }
    if (!/^[0-9]+$/.test(t)) { erro('informe apenas números inteiros positivos.'); return; }
    var n = parseInt(t, 10);
    if (Math.max(1, Math.min(3999, n)) !== n) { erro('o número deve estar entre 1 e 3999.'); return; }
    var original = n;
    var saida = '';
    VALORES.forEach(function (v, i) {
      var vezes = Math.floor(n / v);
      saida += SIMBOLOS[i].repeat(vezes);
      n -= vezes * v;
    });
    rom.value = saida;
    sucesso('O número romano é', saida, original.toLocaleString('pt-BR') + ' = ' + saida);
  }
  function paraDecimal() {
    var t = rom.value.trim().toUpperCase();
    if (t === '') { erro('digite um número romano.'); return; }
    if (!PADRAO.test(t)) { erro('número romano inválido. Use apenas I, V, X, L, C, D e M em uma sequência válida (até MMMCMXCIX).'); return; }
    var resto = t;
    var total = 0;
    VALORES.forEach(function (v, i) {
      while (resto.indexOf(SIMBOLOS[i]) === 0) {
        total += v;
        resto = resto.slice(SIMBOLOS[i].length);
      }
    });
    rom.value = t;
    dec.value = String(total);
    sucesso('O número decimal é', total.toLocaleString('pt-BR'), t + ' = ' + total.toLocaleString('pt-BR'));
  }
  function limpar() {
    dec.value = '';
    rom.value = '';
    estilo('#c7d2fe', '#ffffff', '#64748b');
    resultado.textContent = MSG_INICIAL;
    dec.focus();
  }
  document.getElementById('rom-para-romano').addEventListener('click', paraRomano);
  document.getElementById('rom-para-decimal').addEventListener('click', paraDecimal);
  document.getElementById('rom-limpar').addEventListener('click', limpar);
  dec.addEventListener('keydown', function (e) { if (e.key === 'Enter') { paraRomano(); } });
  rom.addEventListener('keydown', function (e) { if (e.key === 'Enter') { paraDecimal(); } });
  [dec, rom].forEach(function (el) {
    el.addEventListener('focus', function () { el.style.borderColor = '#6366f1'; });
    el.addEventListener('blur', function () { el.style.borderColor = '#c7d2fe'; });
  });
})();
</script>

## Como usar o conversor

1. Para converter **decimal em romano**, digite um número inteiro entre 1 e 3999 no campo **Decimal** (por exemplo, `1994`).
2. Clique em **Converter para Romano** (ou pressione Enter) para ver o resultado (`MCMXCIV`).
3. Para converter **romano em decimal**, digite o número romano no campo **Romano** (por exemplo, `MCMXCIV`). Letras minúsculas também funcionam.
4. Clique em **Converter para Decimal** (ou pressione Enter) para ver o resultado (`1.994`).
5. Use o botão **Limpar** para apagar os campos e fazer uma nova conversão.

Depois de cada conversão, o campo correspondente é preenchido automaticamente com o valor equivalente. Se o número romano estiver escrito fora das regras (como `IIII` ou `VX`), o conversor avisa que ele é inválido.

## Entendendo os termos

- **Número romano:** sistema de numeração criado na Roma Antiga que representa valores com letras do alfabeto latino, como I, V, X, L, C, D e M.
- **Número decimal (arábico):** sistema de numeração que usamos no dia a dia, com os algarismos de 0 a 9, como 5, 42 ou 1994.
- **Algarismo romano:** cada letra usada para formar um número romano. Os valores são I = 1, V = 5, X = 10, L = 50, C = 100, D = 500 e M = 1000.
- **Princípio aditivo:** quando uma letra de menor ou igual valor vem depois de outra, os valores são somados. Exemplos: VI = 5 + 1 = 6 e XXX = 30.
- **Princípio subtrativo:** quando uma letra de menor valor vem antes de outra maior, o valor menor é subtraído. Exemplos: IV = 5 − 1 = 4 e XC = 100 − 10 = 90. Só I, X e C podem ser usadas dessa forma.
- **Repetição de símbolos:** uma letra pode se repetir até três vezes seguidas (III = 3). Já V, L e D nunca se repetem.
- **Limite do conversor:** a notação romana padrão vai de 1 (I) a 3999 (MMMCMXCIX). O zero não tem representação em números romanos.
- **Conversão:** processo de transformar um número de um sistema de numeração para outro, sem alterar o seu valor.