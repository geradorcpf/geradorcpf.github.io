---
title: "Tradutor de Código Morse"
seoTitle: "Tradutor de Código Morse"
description: "Tradutor de Código Morse: traduza texto para código Morse e de volta. Grátis e online, sem cadastro."
summary: "Traduza texto para código Morse e de volta."
date: 2026-11-12
draft: false
category: "dev"
tags: ["código morse", "codificação", "texto"]
keywords: ["tradutor de código morse", "tradutor de código morse online", "código morse", "codificação", "texto"]
---

Digite um texto ou cole um código morse nos campos abaixo e depois clique em **Converter para morse** ou **Converter para texto**.

<div id="calc-morse" style="max-width:560px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">📡 Tradutor de Código Morse</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Converta texto em morse, morse em texto e ouça o resultado.</p>
<label for="morse-texto" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Texto</label>
<textarea id="morse-texto" rows="4" placeholder="Ex.: SOS" autocomplete="off" spellcheck="false" style="width:100%;padding:12px 14px;margin-bottom:12px;font-size:1rem;font-family:inherit;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;resize:vertical;"></textarea>
<button type="button" id="morse-para-morse" style="width:100%;padding:13px 18px;margin-bottom:16px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Converter para morse</button>
<label for="morse-codigo" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Código morse</label>
<textarea id="morse-codigo" rows="4" placeholder="Ex.: ... --- ..." autocomplete="off" spellcheck="false" style="width:100%;padding:12px 14px;margin-bottom:12px;font-size:1rem;font-family:ui-monospace,SFMono-Regular,Menlo,Consolas,monospace;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;resize:vertical;"></textarea>
<div style="display:flex;gap:10px;flex-wrap:wrap;margin-bottom:16px;">
<button type="button" id="morse-para-texto" style="flex:1;min-width:160px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Converter para texto</button>
<button type="button" id="morse-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div style="display:flex;gap:10px;flex-wrap:wrap;align-items:center;">
<button type="button" id="morse-ouvir" style="flex:1;min-width:120px;padding:13px 18px;font-size:1rem;font-weight:700;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">🔊 Ouvir</button>
<label for="morse-velocidade" style="font-weight:600;font-size:0.95rem;">Velocidade do som</label>
<select id="morse-velocidade" style="padding:12px 14px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<option value="150">Lento</option>
<option value="80" selected>Normal</option>
<option value="50">Rápido</option>
</select>
</div>
<div id="morse-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="morse-status">digite um texto ou um código morse e escolha uma conversão.</span></div>
</div>
<script>
(function () {
  var texto = document.getElementById('morse-texto');
  var codigo = document.getElementById('morse-codigo');
  var status = document.getElementById('morse-status');
  var caixa = document.getElementById('morse-resposta');
  var botaoOuvir = document.getElementById('morse-ouvir');
  var velocidade = document.getElementById('morse-velocidade');
  var pares = [
    ['A', '.-'], ['B', '-...'], ['C', '-.-.'], ['D', '-..'], ['E', '.'], ['F', '..-.'],
    ['G', '--.'], ['H', '....'], ['I', '..'], ['J', '.---'], ['K', '-.-'], ['L', '.-..'],
    ['M', '--'], ['N', '-.'], ['O', '---'], ['P', '.--.'], ['Q', '--.-'], ['R', '.-.'],
    ['S', '...'], ['T', '-'], ['U', '..-'], ['V', '...-'], ['W', '.--'], ['X', '-..-'],
    ['Y', '-.--'], ['Z', '--..'],
    ['1', '.----'], ['2', '..---'], ['3', '...--'], ['4', '....-'], ['5', '.....'],
    ['6', '-....'], ['7', '--...'], ['8', '---..'], ['9', '----.'], ['0', '-----'],
    ['.', '.-.-.-'], [',', '--..--'], ['?', '..--..'], ['!', '-.-.--'], ['-', '-....-'],
    ['/', '-..-.'], ['@', '.--.-.'], ['(', '-.--.'], [')', '-.--.-'], [':', '---...'],
    [';', '-.-.-.'], ['=', '-...-'], ['+', '.-.-.'], ["'", '.----.'], ['"', '.-..-.'],
    ['\u0026', '.-...'], ['_', '..--.-'], ['$', '...-..-']
  ];
  var paraMorse = {};
  var paraTexto = {};
  pares.forEach(function (p) {
    paraMorse[p[0]] = p[1];
    paraTexto[p[1]] = p[0];
  });
  var contexto = null;
  var tocando = false;
  var temporizador = null;
  function mostrar(msg, tipo) {
    if (tipo === 'erro') {
      caixa.style.borderColor = '#fca5a5';
      caixa.style.background = '#fef2f2';
      status.style.color = '#b91c1c';
    } else if (tipo === 'ok') {
      caixa.style.borderColor = '#86efac';
      caixa.style.background = '#f0fdf4';
      status.style.color = '#166534';
    } else {
      caixa.style.borderColor = '#c7d2fe';
      caixa.style.background = '#ffffff';
      status.style.color = '#64748b';
    }
    status.textContent = msg;
  }
  function semAcento(s) {
    return s.normalize('NFD').replace(/[\u0300-\u036f]/g, '');
  }
  function textoParaMorse(t) {
    var limpo = semAcento(String(t)).toUpperCase();
    var palavras = limpo.split(/\s+/).filter(function (w) { return w !== ''; });
    var ignorados = 0;
    var saida = palavras.map(function (w) {
      var letras = [];
      w.split('').forEach(function (c) {
        if (paraMorse.hasOwnProperty(c)) { letras.push(paraMorse[c]); } else { ignorados += 1; }
      });
      return letras.join(' ');
    }).filter(function (w) { return w !== ''; });
    return { codigo: saida.join(' / '), ignorados: ignorados };
  }
  function morseParaTexto(m) {
    var limpo = String(m).replace(/[\u2022\u00b7]/g, '.').replace(/[\u2014\u2013_]/g, '-');
    var palavras = limpo.split('/').map(function (w) { return w.trim(); }).filter(function (w) { return w !== ''; });
    var invalidos = 0;
    var saida = palavras.map(function (w) {
      return w.split(/\s+/).map(function (c) {
        if (paraTexto.hasOwnProperty(c)) { return paraTexto[c]; }
        invalidos += 1;
        return '?';
      }).join('');
    });
    return { texto: saida.join(' '), invalidos: invalidos };
  }
  function converterParaMorse() {
    if (texto.value.trim() === '') { mostrar('digite um texto para converter.', 'erro'); return; }
    var r = textoParaMorse(texto.value);
    if (r.codigo === '') { mostrar('nenhum caractere do texto possui código morse.', 'erro'); return; }
    codigo.value = r.codigo;
    if (r.ignorados > 0) {
      mostrar('texto convertido. ' + r.ignorados + ' caractere(s) sem código morse foram ignorados.', 'ok');
    } else {
      mostrar('texto convertido para código morse.', 'ok');
    }
  }
  function converterParaTexto() {
    if (codigo.value.trim() === '') { mostrar('digite um código morse para converter.', 'erro'); return; }
    var r = morseParaTexto(codigo.value);
    texto.value = r.texto;
    if (r.invalidos > 0) {
      mostrar('código convertido. ' + r.invalidos + ' sequência(s) inválida(s) foram trocadas por ?.', 'erro');
    } else {
      mostrar('código morse convertido para texto.', 'ok');
    }
  }
  function parar() {
    tocando = false;
    if (temporizador) { clearTimeout(temporizador); temporizador = null; }
    if (contexto) { try { contexto.close(); } catch (e) {} contexto = null; }
    botaoOuvir.textContent = '🔊 Ouvir';
  }
  function ouvir() {
    if (tocando) { parar(); return; }
    if (codigo.value.trim() === '') {
      if (texto.value.trim() === '') { mostrar('digite um texto ou um código morse para ouvir.', 'erro'); return; }
      converterParaMorse();
    }
    var Audio = window.AudioContext || window.webkitAudioContext;
    if (!Audio) { mostrar('seu navegador não suporta reprodução de áudio.', 'erro'); return; }
    var limpo = String(codigo.value).replace(/[\u2022\u00b7]/g, '.').replace(/[\u2014\u2013_]/g, '-');
    var palavras = limpo.split('/').map(function (w) { return w.trim(); }).filter(function (w) { return w !== ''; });
    var unidade = Number(velocidade.value) / 1000;
    contexto = new Audio();
    var osc = contexto.createOscillator();
    var ganho = contexto.createGain();
    osc.type = 'sine';
    osc.frequency.value = 600;
    ganho.gain.value = 0;
    osc.connect(ganho);
    ganho.connect(contexto.destination);
    var t = contexto.currentTime + 0.1;
    palavras.forEach(function (w) {
      w.split(/\s+/).forEach(function (letra) {
        letra.split('').forEach(function (s) {
          if (s === '.' || s === '-') {
            var dur = s === '.' ? unidade : unidade * 3;
            ganho.gain.setValueAtTime(0.4, t);
            ganho.gain.setValueAtTime(0, t + dur);
            t += dur + unidade;
          }
        });
        t += unidade * 2;
      });
      t += unidade * 4;
    });
    osc.start();
    tocando = true;
    botaoOuvir.textContent = '⏹ Parar';
    mostrar('reproduzindo o código morse...', 'ok');
    var total = (t - contexto.currentTime) * 1000;
    temporizador = setTimeout(function () {
      parar();
      mostrar('reprodução concluída.', 'ok');
    }, total);
  }
  function limpar() {
    parar();
    texto.value = '';
    codigo.value = '';
    mostrar('digite um texto ou um código morse e escolha uma conversão.', 'neutro');
    texto.focus();
  }
  document.getElementById('morse-para-morse').addEventListener('click', converterParaMorse);
  document.getElementById('morse-para-texto').addEventListener('click', converterParaTexto);
  document.getElementById('morse-limpar').addEventListener('click', limpar);
  botaoOuvir.addEventListener('click', ouvir);
  [texto, codigo].forEach(function (el) {
    el.addEventListener('focus', function () { el.style.borderColor = '#6366f1'; });
    el.addEventListener('blur', function () { el.style.borderColor = '#c7d2fe'; });
  });
})();
</script>

## Como usar o tradutor

1. Para **transformar texto em morse**, digite ou cole o texto no campo **Texto** e clique em **Converter para morse**. O resultado aparece no campo **Código morse**.
2. Para **transformar morse em texto**, cole o código no campo **Código morse** e clique em **Converter para texto**. O resultado aparece no campo **Texto**.
3. Para **ouvir o código**, clique em **Ouvir** e escolha a **Velocidade do som** (Lento, Normal ou Rápido). Se o campo do código estiver vazio, o texto é convertido antes. Clique em **Parar** para interromper o som.
4. Use o botão **Limpar** para apagar os dois campos e começar de novo.

No código morse, separe as letras com **espaço** e as palavras com uma **barra** (`/`). Você também pode colar morse escrito com • e · (ponto) ou — e – (traço). O código morse internacional não tem letras acentuadas nem o ç, então o tradutor remove os acentos: "Ação" vira `.- -.-. .- ---`, que volta como "ACAO".

## Entendendo os termos

- **Código morse:** sistema que representa letras, números e sinais por meio de sequências de pontos e traços.
- **Ponto (.):** sinal curto, a menor unidade de tempo do código morse.
- **Traço (-):** sinal longo, com duração de três pontos.
- **Barra (/):** símbolo usado na escrita para separar uma palavra da outra.
- **Pausa:** silêncio entre sinais. Entre os sinais de uma letra dura um ponto, entre letras dura três pontos e entre palavras dura sete pontos.
- **SOS:** pedido internacional de socorro, escrito como `... --- ...`.
- **Velocidade do som:** ritmo da reprodução do áudio, que pode ser lento, normal ou rápido.
- **Texto:** mensagem escrita em letras, números e pontuação, antes de ser convertida em morse.

## Como funciona o código morse

O código morse foi criado na década de 1830 por Samuel Morse e Alfred Vail para o telégrafo. Ainda é usado por radioamadores, na aviação e em situações de emergência, porque pode ser transmitido por som, luz ou batidas.

## Alfabeto morse

| Letra | Código | Letra | Código | Letra | Código |
|-------|--------|-------|--------|-------|--------|
| A | `.-` | J | `.---` | S | `...` |
| B | `-...` | K | `-.-` | T | `-` |
| C | `-.-.` | L | `.-..` | U | `..-` |
| D | `-..` | M | `--` | V | `...-` |
| E | `.` | N | `-.` | W | `.--` |
| F | `..-.` | O | `---` | X | `-..-` |
| G | `--.` | P | `.--.` | Y | `-.--` |
| H | `....` | Q | `--.-` | Z | `--..` |
| I | `..` | R | `.-.` | | |

## Números em morse

| Número | Código | Número | Código |
|--------|--------|--------|--------|
| 1 | `.----` | 6 | `-....` |
| 2 | `..---` | 7 | `--...` |
| 3 | `...--` | 8 | `---..` |
| 4 | `....-` | 9 | `----.` |
| 5 | `.....` | 0 | `-----` |

## Exemplo resolvido

Como escrever a palavra **SOS** em código morse?

1. Separe as letras: S, O e S.
2. Procure cada letra no alfabeto: S = `...` e O = `---`.
3. Junte os códigos separando as letras com espaço: `... --- ...`.

**Resposta:** SOS em código morse é `... --- ...`.