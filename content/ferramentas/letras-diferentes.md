---
title: "Letras Diferentes"
seoTitle: "Letras Diferentes"
description: "Letras Diferentes: converta seu texto em letras diferentes para bio e perfis. Grátis e online, sem cadastro."
summary: "Converta seu texto em letras diferentes para bio e perfis."
date: 2026-11-04
draft: false
category: "texto"
tags: ["letras personalizadas", "fontes", "redes sociais", "texto"]
keywords: ["letras diferentes", "letras diferentes online", "letras personalizadas", "fontes", "redes sociais"]
---

Basta digitar seu texto abaixo e copiar o estilo de letra que você mais gostou.

<div id="calc-letras" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">✨ Gerador de Letras Diferentes</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Digite seu texto e veja todos os estilos na hora.</p>
<label for="ld-texto" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Digite seu texto</label>
<input id="ld-texto" type="text" placeholder="Ex.: Letras Diferentes" autocomplete="off" maxlength="200" style="width:100%;padding:12px 14px;margin-bottom:20px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="ld-gerar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Gerar Letras</button>
<button type="button" id="ld-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="ld-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="ld-aviso">digite um texto para ver os estilos de letras.</span><div id="ld-lista" style="margin-top:12px;"></div></div>
</div>
<script>
(function () {
  var entrada = document.getElementById('ld-texto');
  var lista = document.getElementById('ld-lista');
  var aviso = document.getElementById('ld-aviso');
  var caixa = document.getElementById('ld-resposta');
  var UP = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ';
  var LO = 'abcdefghijklmnopqrstuvwxyz';
  var DI = '0123456789';
  var AVISO_PADRAO = 'digite um texto para ver os estilos de letras.';
  function cp(n) { return String.fromCodePoint(n); }
  function alfabeto(up, lo, di, exc) {
    var mapa = {};
    Array.from(UP).forEach(function (c, i) { mapa[c] = cp(up + i); });
    Array.from(LO).forEach(function (c, i) { mapa[c] = cp(lo + i); });
    if (di) { Array.from(DI).forEach(function (c, i) { mapa[c] = cp(di + i); }); }
    if (exc) { Object.keys(exc).forEach(function (k) { mapa[k] = cp(exc[k]); }); }
    return mapa;
  }
  function listaParaMapa(alvo, destino, maiusculas) {
    var mapa = {};
    Array.from(alvo).forEach(function (c, i) {
      mapa[LO.charAt(i)] = destino[i];
      if (maiusculas) { mapa[UP.charAt(i)] = destino[i]; }
    });
    return mapa;
  }
  var circuloNum = { '0': 0x24EA, '1': 0x2460, '2': 0x2461, '3': 0x2462, '4': 0x2463, '5': 0x2464, '6': 0x2465, '7': 0x2466, '8': 0x2467, '9': 0x2468 };
  var duploExc = { 'C': 0x2102, 'H': 0x210D, 'N': 0x2115, 'P': 0x2119, 'Q': 0x211A, 'R': 0x211D, 'Z': 0x2124 };
  var versalete = listaParaMapa(LO, Array.from('ᴀʙᴄᴅᴇꜰɢʜɪᴊᴋʟᴍɴᴏᴘǫʀsᴛᴜᴠᴡxʏᴢ'), true);
  var invertido = listaParaMapa(LO, Array.from('ɐqɔpǝɟƃɥᴉɾʞlɯuodbɹsʇnʌʍxʎz'), true);
  var circulo = alfabeto(0x24B6, 0x24D0, 0, circuloNum);
  var fullwidth = alfabeto(0xFF21, 0xFF41, 0xFF10, { ' ': 0x3000 });
  var italico = alfabeto(0x1D434, 0x1D44E, 0, { 'h': 0x210E });
  var estilos = [
    { n: 'Negrito', m: alfabeto(0x1D400, 0x1D41A, 0x1D7CE) },
    { n: 'Itálico', m: italico },
    { n: 'Negrito itálico', m: alfabeto(0x1D468, 0x1D482, 0x1D7CE) },
    { n: 'Cursiva elegante', m: alfabeto(0x1D4D0, 0x1D4EA, 0x1D7CE) },
    { n: 'Gótico', m: alfabeto(0x1D56C, 0x1D586, 0x1D7CE) },
    { n: 'Sem serifa', m: alfabeto(0x1D5A0, 0x1D5BA, 0x1D7E2) },
    { n: 'Sem serifa negrito', m: alfabeto(0x1D5D4, 0x1D5EE, 0x1D7EC) },
    { n: 'Sem serifa itálico', m: alfabeto(0x1D608, 0x1D622, 0x1D7E2) },
    { n: 'Monoespaçada', m: alfabeto(0x1D670, 0x1D68A, 0x1D7F6) },
    { n: 'Contornada', m: alfabeto(0x1D538, 0x1D552, 0x1D7D8, duploExc) },
    { n: 'Em círculos', m: circulo },
    { n: 'Círculos pretos', m: alfabeto(0x1F150, 0x1F150, 0) },
    { n: 'Quadrados', m: alfabeto(0x1F130, 0x1F130, 0) },
    { n: 'Quadrados pretos', m: alfabeto(0x1F170, 0x1F170, 0) },
    { n: 'Largura total', m: fullwidth },
    { n: 'Versalete', m: versalete },
    { n: 'De cabeça para baixo', m: invertido, inverter: true },
    { n: 'Riscado', marca: '\u0336' },
    { n: 'Sublinhado', marca: '\u0332' }
  ];
  var ehMarca = /[\u0300-\u036f]/;
  function converter(texto, estilo) {
    var chars = Array.from(texto.normalize('NFD'));
    if (estilo.marca) {
      return chars.map(function (c) { return ehMarca.test(c) ? c : c + estilo.marca; }).join('');
    }
    var saida = chars.map(function (c) {
      return Object.prototype.hasOwnProperty.call(estilo.m, c) ? estilo.m[c] : c;
    });
    if (estilo.inverter) { saida.reverse(); }
    return saida.join('');
  }
  function copiarAlternativo(txt) {
    var t = document.createElement('textarea');
    t.value = txt;
    t.style.position = 'fixed';
    t.style.opacity = '0';
    document.body.appendChild(t);
    t.select();
    try { document.execCommand('copy'); } catch (e) {}
    document.body.removeChild(t);
  }
  function copiar(txt, btn) {
    function ok() {
      btn.textContent = 'Copiado!';
      setTimeout(function () { btn.textContent = 'Copiar'; }, 1500);
    }
    if (navigator.clipboard && navigator.clipboard.writeText) {
      navigator.clipboard.writeText(txt).then(ok, function () { copiarAlternativo(txt); ok(); });
    } else {
      copiarAlternativo(txt);
      ok();
    }
  }
  function linha(nome, txt) {
    var row = document.createElement('div');
    row.style.cssText = 'display:flex;align-items:center;gap:10px;padding:10px 12px;margin-bottom:8px;background:#f8fafc;border:2px solid #c7d2fe;border-radius:12px;';
    var corpo = document.createElement('div');
    corpo.style.cssText = 'flex:1;min-width:0;';
    var rotulo = document.createElement('div');
    rotulo.style.cssText = 'font-size:0.75rem;font-weight:600;color:#64748b;margin-bottom:2px;';
    rotulo.textContent = nome;
    var valor = document.createElement('div');
    valor.style.cssText = 'font-size:1.1rem;color:#1e293b;word-break:break-word;';
    valor.textContent = txt;
    corpo.appendChild(rotulo);
    corpo.appendChild(valor);
    var btn = document.createElement('button');
    btn.type = 'button';
    btn.textContent = 'Copiar';
    btn.style.cssText = 'padding:8px 14px;font-size:0.9rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:8px;cursor:pointer;flex-shrink:0;';
    btn.addEventListener('click', function () { copiar(txt, btn); });
    row.appendChild(corpo);
    row.appendChild(btn);
    return row;
  }
  function gerar() {
    var texto = entrada.value;
    lista.textContent = '';
    if (texto.trim() === '') {
      caixa.style.borderColor = '#c7d2fe';
      caixa.style.background = '#ffffff';
      aviso.style.color = '#64748b';
      aviso.textContent = AVISO_PADRAO;
      return;
    }
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    aviso.style.color = '#166534';
    aviso.textContent = estilos.length + ' estilos gerados. Clique em "Copiar" no que preferir.';
    estilos.forEach(function (e) { lista.appendChild(linha(e.n, converter(texto, e))); });
  }
  function limpar() {
    entrada.value = '';
    gerar();
    entrada.focus();
  }
  document.getElementById('ld-gerar').addEventListener('click', gerar);
  document.getElementById('ld-limpar').addEventListener('click', limpar);
  entrada.addEventListener('input', gerar);
  entrada.addEventListener('keydown', function (e) { if (e.key === 'Enter') { gerar(); } });
  entrada.addEventListener('focus', function () { entrada.style.borderColor = '#6366f1'; });
  entrada.addEventListener('blur', function () { entrada.style.borderColor = '#c7d2fe'; });
})();
</script>

## Como usar o gerador de letras diferentes

1. Digite ou cole a frase que você quer converter no campo **Digite seu texto**.
2. Veja a lista de estilos que aparece logo abaixo. Ela é atualizada a cada letra digitada (ou ao clicar em **Gerar Letras**).
3. Clique em **Copiar** ao lado do estilo que você gostou.
4. Cole o texto (Ctrl+V no Windows ou Command+V no Mac) na sua bio, nome de perfil, legenda, mensagem ou nick.
5. Use o botão **Limpar** para apagar o texto e começar de novo.

Atenção: nem toda plataforma aceita todos os estilos. Instagram, X, WhatsApp, Facebook e jogos como Free Fire podem exibir alguns caracteres como quadradinhos, ou não aceitar letras com acento e cedilha. Se isso acontecer, teste outro estilo.

## Entendendo os termos

- **Letras diferentes:** textos escritos com caracteres especiais que imitam outras fontes, como negrito, cursiva ou círculos.
- **Unicode:** padrão internacional que reúne milhares de caracteres e símbolos. É ele que permite essas letras funcionarem em qualquer lugar onde se cola texto.
- **Estilo (ou fonte):** o visual aplicado às letras, como negrito, itálico ou gótico. Na prática, cada estilo é um conjunto de caracteres Unicode diferentes.
- **Negrito:** letras mais grossas e com destaque.
- **Itálico:** letras inclinadas para a direita.
- **Cursiva elegante:** letras que imitam a escrita à mão, com traços decorativos.
- **Gótico:** letras com visual medieval, parecidas com as de jornais antigos.
- **Sem serifa:** letras limpas, sem os pequenos traços nas pontas.
- **Monoespaçada:** letras com a mesma largura, como em máquina de escrever.
- **Em círculos e quadrados:** letras e números dentro de círculos ou quadrados, ótimos para destacar palavras curtas.
- **Largura total:** letras largas e espaçadas, no estilo visual japonês.
- **Versalete:** letras minúsculas desenhadas com formato de maiúsculas pequenas.
- **Riscado e sublinhado:** texto com uma linha cortando ou passando por baixo das letras.
- **Copiar e colar:** o texto gerado é comum, então basta copiar e colar onde quiser, sem instalar nada.
- **Compatibilidade:** capacidade de um app ou site de exibir corretamente esses caracteres. Varia de plataforma para plataforma.