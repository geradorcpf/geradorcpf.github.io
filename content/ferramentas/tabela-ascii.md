---
title: "Tabela ASCII"
seoTitle: "Tabela ASCII"
description: "Tabela ASCII: consulte a tabela ASCII com códigos decimais, hex e binários. Grátis e online, sem cadastro."
summary: "Consulte a tabela ASCII com códigos decimais, hex e binários."
date: 2026-11-10
draft: false
category: "dev"
tags: ["ascii", "caracteres", "codificação", "desenvolvimento"]
keywords: ["tabela ascii", "tabela ascii online", "ascii", "caracteres", "codificação"]
---

Basta digitar um código, um caractere ou o nome de um código de controle abaixo para filtrar a tabela ASCII completa (0 a 255).

<div id="calc-ascii" style="max-width:760px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🔤 Tabela ASCII</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Pesquise por código ou caractere e veja decimal, hex, octal, binário e HTML.</p>
<label for="asc-busca" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Buscar</label>
<input id="asc-busca" type="text" placeholder="Ex.: 65, 41, A, 01000001 ou ESC" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<label for="asc-grupo" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Grupo de caracteres</label>
<select id="asc-grupo" style="width:100%;padding:12px 14px;margin-bottom:20px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<option value="todos">Todos (0 a 255)</option>
<option value="controle">Controle (0 a 31 e 127)</option>
<option value="padrao">Padrão imprimível (32 a 126)</option>
<option value="estendido">Estendidos (128 a 255)</option>
</select>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="asc-filtrar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Filtrar Tabela</button>
<button type="button" id="asc-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="asc-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="asc-resultado">carregando a tabela...</span></div>
<div id="asc-tabela-box" style="margin-top:16px;max-height:420px;overflow:auto;background:#ffffff;border:2px solid #c7d2fe;border-radius:12px;"><table id="asc-tabela" style="width:100%;border-collapse:collapse;font-size:0.85rem;color:#1e293b;"></table></div>
</div>
<script>
(function () {
  var TRACO = '\u2014';
  var NOMES = ['NUL (Nulo)', 'SOH (Início de cabeçalho)', 'STX (Início de texto)', 'ETX (Fim de texto)', 'EOT (Fim de transmissão)', 'ENQ (Consulta)', 'ACK (Confirmação)', 'BEL (Campainha)', 'BS (Retrocesso)', 'HT (Tabulação horizontal)', 'LF (Nova linha)', 'VT (Tabulação vertical)', 'FF (Avanço de página)', 'CR (Retorno de carro)', 'SO (Shift Out)', 'SI (Shift In)', 'DLE (Escape de link de dados)', 'DC1 (Controle de dispositivo 1 / XON)', 'DC2 (Controle de dispositivo 2)', 'DC3 (Controle de dispositivo 3 / XOFF)', 'DC4 (Controle de dispositivo 4)', 'NAK (Confirmação negativa)', 'SYN (Espera síncrona)', 'ETB (Fim de bloco de transmissão)', 'CAN (Cancelar)', 'EM (Fim do meio)', 'SUB (Substituir)', 'ESC (Escape)', 'FS (Separador de arquivo)', 'GS (Separador de grupo)', 'RS (Separador de registro)', 'US (Separador de unidade)'];
  var busca = document.getElementById('asc-busca');
  var grupoSel = document.getElementById('asc-grupo');
  var tabela = document.getElementById('asc-tabela');
  var resultado = document.getElementById('asc-resultado');
  var caixa = document.getElementById('asc-resposta');
  var dados = [];
  function pad(texto, tamanho) {
    return ('00000000' + texto).slice(-tamanho);
  }
  function caractereEstendido(i) {
    var t;
    try {
      t = new TextDecoder('windows-1252').decode(new Uint8Array([i]));
    } catch (e) {
      t = String.fromCharCode(i);
    }
    var cp = t.charCodeAt(0);
    if (cp === 65533 || (cp >= 128 && 159 >= cp)) { return TRACO; }
    return t;
  }
  function criar(i) {
    var grupo = 'estendido';
    var car = TRACO;
    var desc = 'Caractere estendido (Windows-1252)';
    if (31 >= i) {
      grupo = 'controle';
      desc = NOMES[i];
    } else if (i === 127) {
      grupo = 'controle';
      desc = 'DEL (Apagar)';
    } else if (127 > i) {
      grupo = 'padrao';
      car = String.fromCharCode(i);
      if (i === 32) {
        car = '\u2423';
        desc = 'Espaço';
      } else if (i >= 48 && 57 >= i) {
        desc = 'Dígito ' + car;
      } else if (i >= 65 && 90 >= i) {
        desc = 'Letra maiúscula ' + car;
      } else if (i >= 97 && 122 >= i) {
        desc = 'Letra minúscula ' + car;
      } else {
        desc = 'Símbolo ou pontuação';
      }
    } else {
      car = caractereEstendido(i);
      if (car === TRACO) { desc = 'Não definido no Windows-1252'; }
    }
    return {
      dec: i,
      hex: pad(i.toString(16).toUpperCase(), 2),
      oct: pad(i.toString(8), 3),
      bin: pad(i.toString(2), 8),
      html: car === TRACO ? TRACO : '&#' + i + ';',
      car: car,
      desc: desc,
      grupo: grupo
    };
  }
  for (var i = 0; i !== 256; i++) { dados.push(criar(i)); }
  var CAMPOS = [['Dec', 'dec'], ['Hex', 'hex'], ['Octal', 'oct'], ['Binário', 'bin'], ['HTML', 'html'], ['Char', 'car'], ['Descrição', 'desc']];
  var CSS_TH = 'position:sticky;top:0;padding:10px 8px;background:#eef2ff;color:#3730a3;text-align:left;font-weight:700;border-bottom:2px solid #c7d2fe;white-space:nowrap;';
  var CSS_TD = 'padding:7px 8px;border-bottom:1px solid #e0e7ff;vertical-align:top;';
  var CSS_MONO = CSS_TD + 'font-family:ui-monospace,SFMono-Regular,Menlo,Consolas,monospace;white-space:nowrap;';
  var thead = document.createElement('thead');
  var trh = document.createElement('tr');
  CAMPOS.forEach(function (c) {
    var th = document.createElement('th');
    th.textContent = c[0];
    th.style.cssText = CSS_TH;
    trh.appendChild(th);
  });
  thead.appendChild(trh);
  var tbody = document.createElement('tbody');
  tabela.appendChild(thead);
  tabela.appendChild(tbody);
  function combina(d, bruto) {
    var q = bruto.toLowerCase();
    if (q === '') { return true; }
    var hexq = q.replace(/^0x/, '');
    if (String(d.dec).indexOf(q) === 0) { return true; }
    if (d.hex.toLowerCase() === hexq) { return true; }
    if (d.oct === q) { return true; }
    if (q.length > 3 && /^[01]+$/.test(q) && d.bin.indexOf(q) !== -1) { return true; }
    if (d.car === bruto) { return true; }
    if (q.length > 2 && d.desc.toLowerCase().indexOf(q) !== -1) { return true; }
    return false;
  }
  function pintar(tipo) {
    if (tipo === 'ok') {
      caixa.style.borderColor = '#86efac';
      caixa.style.background = '#f0fdf4';
      resultado.style.color = '#166534';
    } else if (tipo === 'erro') {
      caixa.style.borderColor = '#fca5a5';
      caixa.style.background = '#fef2f2';
      resultado.style.color = '#b91c1c';
    } else {
      caixa.style.borderColor = '#c7d2fe';
      caixa.style.background = '#ffffff';
      resultado.style.color = '#64748b';
    }
  }
  function filtrar() {
    var q = busca.value.trim();
    var g = grupoSel.value;
    var achados = dados.filter(function (d) {
      return (g === 'todos' || d.grupo === g) && combina(d, q);
    });
    tbody.textContent = '';
    achados.forEach(function (d, idx) {
      var tr = document.createElement('tr');
      tr.style.background = idx % 2 === 0 ? '#ffffff' : '#f8fafc';
      CAMPOS.forEach(function (c) {
        var td = document.createElement('td');
        td.textContent = d[c[1]];
        var mono = c[1] !== 'desc';
        td.style.cssText = mono ? CSS_MONO : CSS_TD;
        if (c[1] === 'car') { td.style.fontWeight = '700'; td.style.color = '#4f46e5'; }
        tr.appendChild(td);
      });
      tbody.appendChild(tr);
    });
    if (achados.length === 0) {
      pintar('erro');
      resultado.textContent = 'nenhum caractere encontrado para essa busca.';
      return;
    }
    if (q === '' && g === 'todos') {
      pintar('neutro');
      resultado.textContent = 'exibindo os 256 caracteres. Digite algo para filtrar.';
      return;
    }
    pintar('ok');
    var msg = 'exibindo ' + achados.length + ' de 256 caracteres.';
    if (achados.length === 1) {
      var u = achados[0];
      msg = 'código ' + u.dec + ' (hex ' + u.hex + ', binário ' + u.bin + ') = ' + u.desc + '.';
    }
    resultado.textContent = msg;
  }
  function limpar() {
    busca.value = '';
    grupoSel.value = 'todos';
    filtrar();
    busca.focus();
  }
  document.getElementById('asc-filtrar').addEventListener('click', filtrar);
  document.getElementById('asc-limpar').addEventListener('click', limpar);
  busca.addEventListener('input', filtrar);
  grupoSel.addEventListener('change', filtrar);
  busca.addEventListener('keydown', function (e) { if (e.key === 'Enter') { filtrar(); } });
  [busca, grupoSel].forEach(function (el) {
    el.addEventListener('focus', function () { el.style.borderColor = '#6366f1'; });
    el.addEventListener('blur', function () { el.style.borderColor = '#c7d2fe'; });
  });
  filtrar();
})();
</script>

## Como usar a ferramenta

1. Digite no campo **Buscar** um código decimal (`65`), um valor em hexadecimal (`41`), um caractere (`A`), um valor binário (`01000001`) ou o nome de um código de controle (`ESC`, `nova linha`).
2. Se quiser, escolha um **Grupo de caracteres** para ver só os códigos de controle, os caracteres imprimíveis ou os estendidos.
3. A tabela é filtrada enquanto você digita. Você também pode clicar em **Filtrar Tabela** ou pressionar Enter.
4. Quando a busca retorna um único caractere, a caixa **Resposta** mostra o código decimal, o hex e o binário correspondentes.
5. Use o botão **Limpar** para apagar a busca e voltar a ver os 256 caracteres.

Para ver só o conjunto ASCII padrão, use os grupos **Controle** e **Padrão imprimível** (códigos 0 a 127). O grupo **Estendidos** mostra os códigos de 128 a 255, que variam conforme a codificação usada. Aqui eles aparecem na codificação Windows-1252.

## Entendendo os termos

- **ASCII:** sigla de *American Standard Code for Information Interchange*. Padrão que associa um número a cada letra, dígito, símbolo e código de controle.
- **Código decimal:** número do caractere na base 10, de 0 a 255. Por exemplo, a letra `A` é o código 65.
- **Hexadecimal (hex):** o mesmo número na base 16, usando os dígitos 0 a 9 e as letras A a F. A letra `A` é `41` em hex.
- **Octal:** o mesmo número na base 8. A letra `A` é `101` em octal.
- **Binário:** o mesmo número na base 2, com 8 bits por caractere. A letra `A` é `01000001`.
- **Entidade HTML:** forma de escrever o caractere em uma página web pelo código, como `&#65;` para a letra `A`.
- **Código de controle:** código de 0 a 31 (e o 127) que não gera um símbolo visível. Serve para comandos como nova linha, tabulação ou campainha.
- **Caractere imprimível:** caractere de 32 a 126 que aparece na tela, como letras, dígitos, pontuação e o espaço.
- **Caracteres estendidos:** códigos de 128 a 255 que acrescentam letras acentuadas e símbolos. Não são padronizados e mudam conforme a codificação.
- **Byte:** unidade de 8 bits. Cada caractere da tabela cabe em 1 byte, o que dá 256 posições (0 a 255).
- **Windows-1252:** codificação comum no Windows para os códigos de 128 a 255, usada aqui para exibir os caracteres estendidos.
- **Unicode:** padrão moderno que inclui o ASCII nas suas primeiras 128 posições e acrescenta milhares de outros caracteres.