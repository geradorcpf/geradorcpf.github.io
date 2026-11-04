---
title: "Informações de Caractere"
seoTitle: "Informações de Caractere"
description: "Informações de Caractere: veja código, Unicode e HTML de qualquer caractere. Grátis e online, sem cadastro."
summary: "Veja código, Unicode e HTML de qualquer caractere."
date: 2026-11-04
draft: false
category: "dev"
tags: ["caracteres", "unicode", "ascii", "desenvolvimento"]
keywords: ["informações de caractere", "informações de caractere online", "caracteres", "unicode", "ascii"]
---

Basta digitar o caractere abaixo e depois clicar em **Informações do Caractere** para ver o código ASCII (decimal), hexadecimal, Unicode, HTML e mais.

<div id="info-caractere" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🔤 Informações de Caractere</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Digite um caractere e veja o resultado na hora.</p>
<label for="car-entrada" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Digite o caractere</label>
<input id="car-entrada" type="text" placeholder="Ex.: A" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:20px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="car-calcular" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Informações do Caractere</button>
<button type="button" id="car-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="car-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <div id="car-resultado">preencha o campo e clique em "Informações do Caractere".</div></div>
</div>
<script>
(function () {
  var entrada = document.getElementById('car-entrada');
  var resultado = document.getElementById('car-resultado');
  var caixa = document.getElementById('car-resposta');
  var E = String.fromCharCode(38);
  var BARRA = String.fromCharCode(92);
  var MSG_PADRAO = 'preencha o campo e clique em "Informações do Caractere".';
  function pad(s, n) {
    s = String(s);
    while (n > s.length) { s = '0' + s; }
    return s;
  }
  function hexa(n) { return n.toString(16).toUpperCase(); }
  function binario(n) {
    var s = n.toString(2);
    while (s.length % 8 !== 0) { s = '0' + s; }
    return s;
  }
  function utf8(ch) {
    var bytes = new TextEncoder().encode(ch);
    var out = [];
    for (var i = 0; i !== bytes.length; i++) { out.push(pad(hexa(bytes[i]), 2)); }
    return out.join(' ');
  }
  function nomeEspecial(cp) {
    if (cp === 32) { return '(espaço)'; }
    if (cp === 9) { return '(tabulação)'; }
    if (cp === 10) { return '(quebra de linha)'; }
    if (cp === 13) { return '(retorno de carro)'; }
    if (cp === 160) { return '(espaço sem quebra)'; }
    if (31 >= cp) { return '(caractere de controle)'; }
    if (cp >= 127) { if (159 >= cp) { return '(caractere de controle)'; } }
    return '';
  }
  function texto(msg, cor) {
    resultado.textContent = msg;
    resultado.style.color = cor;
  }
  function erro(msg) {
    caixa.style.borderColor = '#fca5a5';
    caixa.style.background = '#fef2f2';
    texto(msg, '#b91c1c');
  }
  function linha(rotulo, valor) {
    var l = document.createElement('div');
    l.style.cssText = 'display:flex;justify-content:space-between;gap:12px;flex-wrap:wrap;padding:8px 0;border-bottom:1px solid #e2e8f0;';
    var a = document.createElement('span');
    a.style.cssText = 'font-weight:600;color:#475569;';
    a.textContent = rotulo;
    var b = document.createElement('span');
    b.style.cssText = 'font-family:ui-monospace,Menlo,Consolas,monospace;color:#166534;word-break:break-all;text-align:right;';
    b.textContent = valor;
    l.appendChild(a);
    l.appendChild(b);
    return l;
  }
  function calcular() {
    var v = entrada.value;
    if (v === '') { erro('digite um caractere.'); return; }
    var chars = Array.from(v);
    var ch = chars[0];
    var cp = ch.codePointAt(0);
    var especial = nomeEspecial(cp);
    var linhas = [];
    linhas.push(['Caractere', especial === '' ? ch : especial]);
    linhas.push(['Está na tabela ASCII?', 127 >= cp ? 'Sim' : 'Não (fora de 0–127)']);
    linhas.push(['Decimal', String(cp)]);
    linhas.push(['Hexadecimal', '0x' + hexa(cp)]);
    linhas.push(['Octal', cp.toString(8)]);
    linhas.push(['Binário', binario(cp)]);
    linhas.push(['Unicode', 'U+' + pad(hexa(cp), 4)]);
    linhas.push(['UTF-8 (bytes)', utf8(ch)]);
    linhas.push(['HTML decimal', E + '#' + cp + ';']);
    linhas.push(['HTML hexadecimal', E + '#x' + hexa(cp) + ';']);
    linhas.push(['Escape JavaScript', cp > 65535 ? BARRA + 'u{' + hexa(cp) + '}' : BARRA + 'u' + pad(hexa(cp), 4)]);
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    while (resultado.firstChild) { resultado.removeChild(resultado.firstChild); }
    for (var i = 0; i !== linhas.length; i++) {
      resultado.appendChild(linha(linhas[i][0], linhas[i][1]));
    }
    if (chars.length > 1) {
      var nota = document.createElement('div');
      nota.style.cssText = 'margin-top:10px;font-size:0.85rem;color:#475569;';
      nota.textContent = 'Você digitou ' + chars.length + ' caracteres. Apenas o primeiro foi analisado.';
      resultado.appendChild(nota);
    }
  }
  function limpar() {
    entrada.value = '';
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    texto(MSG_PADRAO, '#64748b');
    entrada.focus();
  }
  document.getElementById('car-calcular').addEventListener('click', calcular);
  document.getElementById('car-limpar').addEventListener('click', limpar);
  entrada.addEventListener('keydown', function (e) { if (e.key === 'Enter') { calcular(); } });
  entrada.addEventListener('focus', function () { entrada.style.borderColor = '#6366f1'; });
  entrada.addEventListener('blur', function () { entrada.style.borderColor = '#c7d2fe'; });
})();
</script>

## Como usar a ferramenta

1. Digite (ou cole) um caractere no campo **Digite o caractere**. Pode ser letra, número, símbolo, acento ou até um emoji.
2. Clique em **Informações do Caractere** (ou pressione Enter) para ver o resultado.
3. Confira a lista de valores logo abaixo: decimal, hexadecimal, Unicode, HTML e outros.
4. Use o botão **Limpar** para apagar o campo e consultar outro caractere.

Se você digitar mais de um caractere, a ferramenta analisa apenas o primeiro e avisa na resposta. Por exemplo, ao digitar `A`, o resultado mostra decimal 65, hexadecimal 0x41 e Unicode U+0041.

## Entendendo os termos

- **Caractere:** qualquer símbolo individual de um texto, como letra, número, pontuação, espaço ou emoji.
- **Tabela ASCII:** padrão antigo que associa um número de 0 a 127 a letras sem acento, números, pontuação e caracteres de controle.
- **Decimal:** o código do caractere escrito na base 10, a numeração do dia a dia. Para letras da tabela ASCII, é o próprio código ASCII.
- **Hexadecimal:** o mesmo código escrito na base 16 (0 a 9 e A a F), muito usado em programação. Aparece com o prefixo `0x`.
- **Octal:** o mesmo código escrito na base 8 (dígitos de 0 a 7).
- **Binário:** o mesmo código escrito na base 2 (apenas 0 e 1), do jeito que o computador guarda a informação.
- **Unicode:** padrão universal que dá um código único a praticamente todo caractere de todos os idiomas, além de símbolos e emojis. É escrito como `U+` seguido do código em hexadecimal.
- **Ponto de código (code point):** o número que identifica um caractere no Unicode, o mesmo valor mostrado em decimal e hexadecimal.
- **UTF-8 (bytes):** forma de gravar o caractere em bytes. Caracteres ASCII usam 1 byte e os demais usam de 2 a 4 bytes.
- **HTML decimal e hexadecimal:** códigos como `&#65;` e `&#x41;` que exibem o caractere em uma página HTML, mesmo que ele não esteja no teclado ou no arquivo.
- **Escape JavaScript:** forma de escrever o caractere dentro de um texto em JavaScript, como `\u0041`, ou `\u{1F600}` para códigos acima de FFFF.
- **Caractere de controle:** código que não representa um símbolo visível, mas uma ação, como tabulação, quebra de linha ou retorno de carro.