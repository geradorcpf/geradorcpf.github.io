---
title: "Texto de Cabeça para Baixo"
seoTitle: "Texto de Cabeça para Baixo"
description: "Texto de Cabeça para Baixo: vire seu texto de cabeça para baixo. Grátis e online, sem cadastro."
summary: "Vire seu texto de cabeça para baixo."
date: 2026-11-12
draft: false
category: "texto"
tags: ["texto invertido", "divertido", "texto"]
keywords: ["texto de cabeça para baixo", "texto de cabeça para baixo online", "texto invertido", "divertido", "texto"]
---

Basta digitar ou colar o texto abaixo e o resultado de cabeça para baixo aparece na hora. Depois, clique em **Copiar** para usar onde quiser.

<div id="calc-cabeca-baixo" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🙃 Texto de Cabeça para Baixo</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Digite o texto e veja o resultado na hora.</p>
<label for="cpb-entrada" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Digite ou cole o texto</label>
<textarea id="cpb-entrada" rows="4" placeholder="Ex.: Olá, mundo!" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;font-family:inherit;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;resize:vertical;"></textarea>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="cpb-converter" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Virar Texto</button>
<button type="button" id="cpb-copiar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Copiar</button>
<button type="button" id="cpb-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="cpb-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resultado:</strong> <span id="cpb-resultado" style="word-break:break-word;white-space:pre-wrap;">digite um texto para ver o resultado.</span></div>
</div>
<script>
(function () {
  var entrada = document.getElementById('cpb-entrada');
  var resultado = document.getElementById('cpb-resultado');
  var caixa = document.getElementById('cpb-resposta');
  var btnCopiar = document.getElementById('cpb-copiar');
  var textoPadrao = 'digite um texto para ver o resultado.';
  var textoAtual = '';
  var mapa = {
    'a': '\u0250', 'b': 'q', 'c': '\u0254', 'd': 'p', 'e': '\u01DD', 'f': '\u025F', 'g': '\u0183', 'h': '\u0265', 'i': '\u1D09',
    'j': '\u027E', 'k': '\u029E', 'l': 'l', 'm': '\u026F', 'n': 'u', 'o': 'o', 'p': 'd', 'q': 'b', 'r': '\u0279', 's': 's',
    't': '\u0287', 'u': 'n', 'v': '\u028C', 'w': '\u028D', 'x': 'x', 'y': '\u028E', 'z': 'z',
    'A': '\u2200', 'B': '\u15FA', 'C': '\u0186', 'D': '\u15E1', 'E': '\u018E', 'F': '\u2132', 'G': '\u2141', 'H': 'H', 'I': 'I',
    'J': '\u017F', 'K': '\uA4D8', 'L': '\u02E5', 'M': 'W', 'N': 'N', 'O': 'O', 'P': '\u0500', 'Q': '\u038C', 'R': '\u1D1A',
    'S': 'S', 'T': '\u22A5', 'U': '\u2229', 'V': '\u039B', 'W': 'M', 'X': 'X', 'Y': '\u2144', 'Z': 'Z',
    '0': '0', '1': '\u0196', '2': '\u1105', '3': '\u0190', '4': '\u3123', '5': '\u03DB', '6': '9', '7': '\u3125', '8': '8', '9': '6',
    '.': '\u02D9', ',': '\u0027', '\u0027': ',', '"': '\u201E', '!': '\u00A1', '?': '\u00BF', ';': '\u061B', '_': '\u203E',
    '(': ')', ')': '(', '[': ']', ']': '[', '{': '}', '}': '{', '\u003C': '\u003E', '\u003E': '\u003C', '\u0026': '\u214B'
  };
  var acentos = {
    '\u0300': '\u0316', '\u0301': '\u0317', '\u0302': '\u032D', '\u0303': '\u0330', '\u0308': '\u0324', '\u0327': '\u0312'
  };
  function ehMarca(c) {
    return /[\u0300-\u036f]/.test(c);
  }
  function virar(texto) {
    var letras = Array.from(texto.normalize('NFD'));
    var grupos = [];
    letras.forEach(function (c) {
      if (ehMarca(c) && grupos.length > 0) {
        grupos[grupos.length - 1].marcas += (acentos[c] || c);
      } else {
        grupos.push({ base: (mapa[c] !== undefined ? mapa[c] : c), marcas: '' });
      }
    });
    return grupos.reverse().map(function (g) { return g.base + g.marcas; }).join('').normalize('NFC');
  }
  function atualizar() {
    var valor = entrada.value;
    if (valor.trim() === '') {
      textoAtual = '';
      caixa.style.borderColor = '#c7d2fe';
      caixa.style.background = '#ffffff';
      resultado.style.color = '#64748b';
      resultado.textContent = textoPadrao;
      return;
    }
    textoAtual = virar(valor);
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    resultado.style.fontSize = '1.2rem';
    resultado.textContent = textoAtual;
  }
  function copiar() {
    if (textoAtual === '') {
      entrada.focus();
      return;
    }
    function feito() {
      btnCopiar.textContent = 'Copiado!';
      setTimeout(function () { btnCopiar.textContent = 'Copiar'; }, 1500);
    }
    if (navigator.clipboard && navigator.clipboard.writeText) {
      navigator.clipboard.writeText(textoAtual).then(feito, function () {});
    } else {
      var area = document.createElement('textarea');
      area.value = textoAtual;
      document.body.appendChild(area);
      area.select();
      try { document.execCommand('copy'); feito(); } catch (e) {}
      document.body.removeChild(area);
    }
  }
  function limpar() {
    entrada.value = '';
    atualizar();
    entrada.focus();
  }
  document.getElementById('cpb-converter').addEventListener('click', atualizar);
  btnCopiar.addEventListener('click', copiar);
  document.getElementById('cpb-limpar').addEventListener('click', limpar);
  entrada.addEventListener('input', atualizar);
  entrada.addEventListener('focus', function () { entrada.style.borderColor = '#6366f1'; });
  entrada.addEventListener('blur', function () { entrada.style.borderColor = '#c7d2fe'; });
})();
</script>

## Como usar a ferramenta

1. Digite ou cole o texto que você quer virar no campo **Digite ou cole o texto**.
2. O resultado aparece na hora em **Resultado**, já de cabeça para baixo. Se preferir, clique em **Virar Texto** para atualizar manualmente.
3. Clique em **Copiar** para copiar o texto virado e colar em redes sociais, mensagens, bios e comentários.
4. Use o botão **Limpar** para apagar o campo e começar um novo texto.

Você pode usar letras com acento (como á, ã, ç, é e õ), números e pontuação. O texto é virado de trás para frente e cada caractere é trocado pelo símbolo parecido com ele de cabeça para baixo.

## Entendendo os termos

- **Texto de cabeça para baixo:** texto escrito de forma que, ao girar a tela em 180°, pareça estar de ponta-cabeça. Também é chamado de texto invertido.
- **Texto invertido:** outro nome para o texto virado, em que a ordem das letras é revertida e cada letra é substituída por um símbolo equivalente.
- **Caractere:** qualquer letra, número, símbolo ou sinal de pontuação que compõe o texto.
- **Unicode:** padrão internacional que reúne milhares de símbolos, inclusive os usados para imitar letras viradas (como ɐ, ǝ e ʇ). Por isso o texto pode ser copiado e colado sem instalar fontes.
- **Acento:** sinal gráfico colocado sobre ou sob a letra (como ´, ~ e ^). Na ferramenta, ele é movido para o lado oposto da letra, acompanhando a inversão.
- **Copiar:** ação de levar o resultado para a área de transferência, para colar em outro lugar.

## Exemplo

Texto digitado: **Olá, mundo!**

Resultado: **¡opunɯ 'ɐ̗lO**

Veja que a ordem das letras foi invertida e cada símbolo foi trocado pelo seu equivalente de cabeça para baixo.