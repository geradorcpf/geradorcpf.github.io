---
title: "Letras Personalizadas"
seoTitle: "Letras Personalizadas"
description: "Letras Personalizadas: transforme texto em letras estilizadas para copiar e colar. Grátis e online, sem cadastro."
summary: "Transforme texto em letras estilizadas para copiar e colar."
date: 2026-11-05
draft: false
category: "texto"
tags: ["letras personalizadas", "fontes", "redes sociais", "texto"]
keywords: ["letras personalizadas", "letras personalizadas online", "fontes", "redes sociais"]
---

Basta digitar o seu texto abaixo e clicar em **Gerar Letras**. Depois, é só clicar no estilo que você gostou para copiar.

<div id="lp-ferramenta" style="max-width:640px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">✨ Letras Personalizadas</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Digite o texto e veja todos os estilos na hora.</p>
<label for="lp-texto" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Digite seu Texto</label>
<input id="lp-texto" type="text" maxlength="120" placeholder="Ex.: Meu Nick" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:20px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="lp-gerar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Gerar Letras</button>
<button type="button" id="lp-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="lp-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong id="lp-titulo" style="color:#3730a3;">Resposta:</strong> <span id="lp-mensagem">digite um texto e clique em "Gerar Letras".</span><div id="lp-lista" style="margin-top:12px;"></div></div>
</div>
<script>
(function () {
  var campo = document.getElementById('lp-texto');
  var caixa = document.getElementById('lp-resposta');
  var mensagem = document.getElementById('lp-mensagem');
  var lista = document.getElementById('lp-lista');
  function between(c, lo, hi) {
    if (lo > c) { return false; }
    if (c > hi) { return false; }
    return true;
  }
  function cp(n) { return String.fromCodePoint(n); }
  function chars(t) { return Array.from(t); }
  function pos(ch) {
    var c = ch.charCodeAt(0);
    if (between(c, 65, 90)) { return c - 65; }
    if (between(c, 97, 122)) { return c - 97; }
    return -1;
  }
  function dig(ch) {
    var c = ch.charCodeAt(0);
    if (between(c, 48, 57)) { return c - 48; }
    return -1;
  }
  function semAcento(t) {
    return t.normalize('NFD').replace(/[\u0300-\u036f]/g, '');
  }
  function zip(de, para) {
    var tabela = {};
    var destino = chars(para);
    chars(de).forEach(function (k, i) { tabela[k] = destino[i]; });
    return tabela;
  }
  function porTabela(t, tabela, minusculo) {
    return chars(semAcento(t)).map(function (ch) {
      var k = minusculo ? ch.toLowerCase() : ch;
      if (Object.prototype.hasOwnProperty.call(tabela, k)) { return tabela[k]; }
      return ch;
    }).join('');
  }
  function porFaixa(t, maiusc, minusc, digitos, excecoes) {
    return chars(semAcento(t)).map(function (ch) {
      var c = ch.charCodeAt(0);
      if (excecoes) {
        if (Object.prototype.hasOwnProperty.call(excecoes, ch)) { return excecoes[ch]; }
      }
      if (between(c, 65, 90)) { return maiusc === null ? ch : cp(maiusc + c - 65); }
      if (between(c, 97, 122)) { return minusc === null ? ch : cp(minusc + c - 97); }
      if (between(c, 48, 57)) { return digitos === null ? ch : cp(digitos + c - 48); }
      return ch;
    }).join('');
  }
  function porLetra(t, base) {
    return chars(semAcento(t)).map(function (ch) {
      var p = pos(ch);
      if (p === -1) { return ch; }
      return cp(base + p);
    }).join('');
  }
  var invertida = zip("abcdefghijklmnopqrstuvwxyz?!.,'0123456789", "ɐqɔpǝɟƃɥᴉɾʞlɯuodbɹsʇnʌʍxʎz¿¡˙',0ƖᄅƐㄣϛ9ㄥ86");
  var arabe = zip("abcdefghijklmnopqrstuvwxyz", "ابكدیفغهيجقلمنوبقرستوفوكيز");
  var livre = zip("abcdefghijklmnopqrstuvwxyz", "αв¢∂єƒgнιנкℓмησρqяѕтυνωχуz");
  var numeros = zip("aeiostbgz", "431057892");
  var versaletes = zip("abcdefghijklmnopqrstuvwxyz", "ᴀʙᴄᴅᴇꜰɢʜɪᴊᴋʟᴍɴᴏᴘǫʀꜱᴛᴜᴠᴡxʏᴢ");
  var duplo = { C: 'ℂ', H: 'ℍ', N: 'ℕ', P: 'ℙ', Q: 'ℚ', R: 'ℝ', Z: 'ℤ' };
  var estilos = [
    { nome: 'Sexy', fn: function (t) { return porFaixa(t, 0x1D4D0, 0x1D4EA, 0x1D7CE); } },
    { nome: 'Simples', fn: function (t) { return porFaixa(t, 0x1D5A0, 0x1D5BA, 0x1D7E2); } },
    { nome: "Rock 'N Roll", fn: function (t) { return porFaixa(t, 0x1D56C, 0x1D586, null); } },
    { nome: 'Maiúsculo & Minúsculo', fn: function (t) {
      var n = 0;
      return chars(t).map(function (ch) {
        if (pos(ch) === -1) { return ch; }
        n = n + 1;
        return n % 2 === 1 ? ch.toLowerCase() : ch.toUpperCase();
      }).join('');
    } },
    { nome: 'Crazy', fn: function (t) { return porFaixa(t, 0x1D538, 0x1D552, 0x1D7D8, duplo); } },
    { nome: '¿ Árabe ?', fn: function (t) { return porTabela(t, arabe, true); } },
    { nome: 'Future', fn: function (t) { return porFaixa(t, 0x1D670, 0x1D68A, 0x1D7F6); } },
    { nome: 'A redondinho', fn: function (t) {
      return chars(semAcento(t)).map(function (ch) {
        var p = pos(ch);
        var d = dig(ch);
        if (p !== -1) { return cp((ch === ch.toUpperCase() ? 0x24B6 : 0x24D0) + p); }
        if (d === 0) { return cp(0x24EA); }
        if (d > 0) { return cp(0x2460 + d - 1); }
        return ch;
      }).join('');
    } },
    { nome: 'Fechado', fn: function (t) { return porLetra(t, 0x1F170); } },
    { nome: 'BIG', fn: function (t) {
      return chars(semAcento(t)).map(function (ch) {
        if (ch === ' ') { return cp(0x3000); }
        var c = ch.charCodeAt(0);
        if (between(c, 33, 126)) { return cp(0xFF01 + c - 33); }
        return ch;
      }).join('');
    } },
    { nome: 'AlieN', fn: function (t) {
      return semAcento(t).split(' ').map(function (palavra) {
        var cs = chars(palavra.toLowerCase());
        if (cs.length === 0) { return ''; }
        cs[0] = cs[0].toUpperCase();
        cs[cs.length - 1] = cs[cs.length - 1].toUpperCase();
        return cs.join('');
      }).join(' ');
    } },
    { nome: 'Free Style', fn: function (t) { return porTabela(t, livre, true); } },
    { nome: 'De cabeça pra baixo', fn: function (t) {
      return chars(porTabela(t, invertida, true)).reverse().join('');
    } },
    { nome: 'Invertido', fn: function (t) { return chars(t).reverse().join(''); } },
    { nome: 'BIG 2', fn: function (t) { return porLetra(t, 0x1F130); } },
    { nome: 'Number', fn: function (t) { return porTabela(t, numeros, true); } },
    { nome: 'Ball', fn: function (t) {
      return chars(semAcento(t)).map(function (ch) {
        var p = pos(ch);
        var d = dig(ch);
        if (p !== -1) { return cp(0x1F150 + p); }
        if (d === 0) { return cp(0x24FF); }
        if (d > 0) { return cp(0x2776 + d - 1); }
        return ch;
      }).join('');
    } },
    { nome: 'Metamorfose', fn: function (t) { return porFaixa(t, 0x1D468, 0x1D482, 0x1D7CE); } },
    { nome: 'Cake', fn: function (t) { return porTabela(t, versaletes, true); } },
    { nome: 'Riscado', fn: function (t) {
      return chars(t).map(function (ch) {
        if (ch === ' ') { return ch; }
        return ch + '\u0336';
      }).join('');
    } }
  ];
  function alternativa(txt) {
    var area = document.createElement('textarea');
    area.value = txt;
    area.style.cssText = 'position:fixed;top:0;left:0;opacity:0;';
    document.body.appendChild(area);
    area.select();
    try { document.execCommand('copy'); } catch (e) { }
    document.body.removeChild(area);
  }
  function copiar(txt, botao) {
    function pronto() {
      botao.textContent = 'Copiado!';
      botao.style.background = '#166534';
      setTimeout(function () {
        botao.textContent = 'Copiar';
        botao.style.background = 'linear-gradient(135deg,#4f46e5,#6366f1)';
      }, 1500);
    }
    if (navigator.clipboard) {
      if (navigator.clipboard.writeText) {
        navigator.clipboard.writeText(txt).then(pronto, function () { alternativa(txt); pronto(); });
        return;
      }
    }
    alternativa(txt);
    pronto();
  }
  function erro(msg) {
    caixa.style.borderColor = '#fca5a5';
    caixa.style.background = '#fef2f2';
    mensagem.style.color = '#b91c1c';
    mensagem.textContent = msg;
    lista.textContent = '';
  }
  function linha(estilo, texto) {
    var item = document.createElement('div');
    item.style.cssText = 'display:flex;align-items:center;justify-content:space-between;gap:12px;padding:12px 14px;margin-bottom:10px;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;';
    var bloco = document.createElement('div');
    bloco.style.cssText = 'min-width:0;flex:1;';
    var rotulo = document.createElement('div');
    rotulo.style.cssText = 'font-size:0.75rem;font-weight:600;color:#64748b;margin-bottom:4px;';
    rotulo.textContent = estilo;
    var saida = document.createElement('div');
    saida.style.cssText = 'font-size:1.15rem;color:#1e293b;word-break:break-word;';
    saida.textContent = texto;
    var botao = document.createElement('button');
    botao.type = 'button';
    botao.textContent = 'Copiar';
    botao.style.cssText = 'padding:8px 14px;font-size:0.85rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:8px;cursor:pointer;';
    bloco.appendChild(rotulo);
    bloco.appendChild(saida);
    item.appendChild(bloco);
    item.appendChild(botao);
    item.addEventListener('click', function () { copiar(texto, botao); });
    return item;
  }
  function gerar() {
    var t = campo.value;
    if (t.trim() === '') { erro('digite um texto para gerar as letras.'); return; }
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    mensagem.style.color = '#166534';
    mensagem.textContent = 'clique em um estilo para copiar.';
    lista.textContent = '';
    estilos.forEach(function (e) { lista.appendChild(linha(e.nome, e.fn(t))); });
  }
  function limpar() {
    campo.value = '';
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    mensagem.style.color = '#64748b';
    mensagem.textContent = 'digite um texto e clique em "Gerar Letras".';
    lista.textContent = '';
    campo.focus();
  }
  document.getElementById('lp-gerar').addEventListener('click', gerar);
  document.getElementById('lp-limpar').addEventListener('click', limpar);
  campo.addEventListener('keydown', function (e) { if (e.key === 'Enter') { gerar(); } });
  campo.addEventListener('focus', function () { campo.style.borderColor = '#6366f1'; });
  campo.addEventListener('blur', function () { campo.style.borderColor = '#c7d2fe'; });
})();
</script>

## Como usar o gerador

1. Digite o seu texto no campo **Digite seu Texto** (por exemplo, o seu nick ou uma frase curta).
2. Clique em **Gerar Letras** (ou pressione Enter) para ver o texto em todos os estilos disponíveis.
3. Clique no estilo que você gostou, ou no botão **Copiar**, para copiar o texto.
4. Cole o resultado onde quiser: bio do Instagram, nick de jogo, status do WhatsApp, post no Facebook ou no X (Twitter).
5. Use o botão **Limpar** para apagar o texto e começar de novo.

Alguns estilos funcionam melhor com letras e números sem acento, por isso os acentos são removidos nesses casos (por exemplo, "ação" vira "acao"). Se um estilo aparecer com quadradinhos, o aparelho ou o aplicativo não tem suporte para aqueles caracteres; escolha outro estilo.

## Entendendo os termos

- **Letras personalizadas:** texto escrito com caracteres de aparência diferente do normal, usado para dar destaque a nicks, bios e mensagens.
- **Unicode:** padrão internacional que reúne milhares de caracteres, incluindo letras decoradas e símbolos. É ele que torna possível copiar e colar essas letras em qualquer lugar.
- **Fonte:** conjunto de desenho das letras. Aqui, os estilos não trocam a fonte do texto: eles usam caracteres Unicode que já têm outra aparência.
- **Nick:** apelido usado em jogos, redes sociais e aplicativos de mensagem.
- **Bio:** pequeno texto de apresentação do perfil em redes sociais.
- **Copiar e colar:** o resultado é texto de verdade, então basta copiar e colar no campo desejado, sem instalar nada.
- **Sexy:** letras cursivas, com traços elegantes e arredondados.
- **Simples:** letras sem serifa, limpas e fáceis de ler.
- **Rock 'N Roll:** letras góticas (fraktur) em negrito, com visual medieval e pesado.
- **Maiúsculo & Minúsculo:** alterna uma letra minúscula e uma maiúscula ao longo do texto.
- **Crazy:** letras de traço duplo, com contorno vazado.
- **¿ Árabe ?:** troca as letras por caracteres árabes de som parecido, só para dar o efeito visual de escrita árabe. O resultado não forma palavras em árabe.
- **Future:** letras monoespaçadas, todas com a mesma largura, com ar de código e tecnologia.
- **A redondinho:** letras e números dentro de círculos.
- **Fechado:** letras brancas sobre quadrados pretos preenchidos.
- **BIG:** letras largas de largura total (fullwidth), que ocupam mais espaço na linha.
- **AlieN:** primeira e última letra de cada palavra em maiúscula, e o resto em minúscula.
- **Free Style:** mistura de letras gregas e cirílicas parecidas com as latinas, para um visual livre.
- **De cabeça pra baixo:** letras giradas em 180° e escritas de trás para frente, como se o texto estivesse virado.
- **Invertido:** o texto na ordem contrária, da última letra para a primeira.
- **BIG 2:** letras maiúsculas dentro de quadrados vazados.
- **Number:** troca letras por números parecidos, como 4 no lugar de A e 3 no lugar de E (estilo leet).
- **Ball:** letras e números brancos sobre círculos pretos preenchidos.
- **Metamorfose:** letras serifadas em negrito e itálico ao mesmo tempo.
- **Cake:** letras em versalete (small caps), que lembram maiúsculas em tamanho pequeno.
- **Riscado:** texto com uma linha cortando cada letra.