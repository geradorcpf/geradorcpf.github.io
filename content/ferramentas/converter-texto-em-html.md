---
title: "Converter Texto para HTML"
seoTitle: "Converter Texto para HTML"
description: "Converter Texto para HTML: transforme texto simples em HTML com parágrafos e quebras. Grátis e online, sem cadastro."
summary: "Transforme texto simples em HTML com parágrafos e quebras."
date: 2026-10-26
draft: false
category: "dev"
tags: ["html", "texto", "conversão", "desenvolvimento"]
keywords: ["converter texto para html", "converter texto para html online", "html", "texto", "conversão"]
---
<!--sudah dikerjakan-->

Basta digitar ou colar o texto abaixo e clicar em **Codificar** para transformar os caracteres especiais em entidades HTML, ou em **Decodificar** para fazer o caminho inverso.

<div id="conv-texto-html" style="max-width:640px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🔤 Converter Texto para HTML</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Converta caracteres especiais em entidades HTML e vice-versa.</p>
<h3 style="margin:0 0 4px;font-size:1.05rem;color:#3730a3;">Codificar Texto para HTML</h3>
<p style="margin:0 0 12px;font-size:0.9rem;color:#64748b;">Digite a frase, depois clique em "Codificar" e confira o resultado abaixo do botão.</p>
<label for="th-cod-entrada" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Texto</label>
<textarea id="th-cod-entrada" rows="4" placeholder="Ex.: Atenção, ação e coração" autocomplete="off" spellcheck="false" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;font-family:inherit;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;resize:vertical;min-height:110px;"></textarea>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="th-cod-btn" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Codificar</button>
<button type="button" id="th-cod-copiar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Copiar</button>
<button type="button" id="th-cod-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="th-cod-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta Codificada:</strong> <span id="th-cod-resultado" style="white-space:pre-wrap;word-break:break-word;">digite o texto e clique em "Codificar".</span></div>
<div style="margin-top:28px;padding-top:24px;border-top:1px solid #c7d2fe;">
<h3 style="margin:0 0 4px;font-size:1.05rem;color:#3730a3;">Decodificar HTML para Texto</h3>
<p style="margin:0 0 12px;font-size:0.9rem;color:#64748b;">Digite a frase, depois clique em "Decodificar" e confira o resultado abaixo do botão.</p>
<label for="th-dec-entrada" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">HTML</label>
<textarea id="th-dec-entrada" rows="4" placeholder="Ex.: Aten&#231;&#227;o, a&#231;&#227;o e cora&#231;&#227;o" autocomplete="off" spellcheck="false" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;font-family:inherit;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;resize:vertical;min-height:110px;"></textarea>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="th-dec-btn" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Decodificar</button>
<button type="button" id="th-dec-copiar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Copiar</button>
<button type="button" id="th-dec-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="th-dec-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta Decodificada:</strong> <span id="th-dec-resultado" style="white-space:pre-wrap;word-break:break-word;">cole o HTML e clique em "Decodificar".</span></div>
</div>
</div>
<script>
(function () {
  var AMP = String.fromCharCode(38);
  var nomes = ('nbsp iexcl cent pound curren yen brvbar sect uml copy ordf laquo not shy reg macr ' +
    'deg plusmn sup2 sup3 acute micro para middot cedil sup1 ordm raquo frac14 frac12 frac34 iquest ' +
    'Agrave Aacute Acirc Atilde Auml Aring AElig Ccedil Egrave Eacute Ecirc Euml Igrave Iacute Icirc Iuml ' +
    'ETH Ntilde Ograve Oacute Ocirc Otilde Ouml times Oslash Ugrave Uacute Ucirc Uuml Yacute THORN szlig ' +
    'agrave aacute acirc atilde auml aring aelig ccedil egrave eacute ecirc euml igrave iacute icirc iuml ' +
    'eth ntilde ograve oacute ocirc otilde ouml divide oslash ugrave uacute ucirc uuml yacute thorn yuml').split(' ');
  var extras = { 8364: 'euro', 8211: 'ndash', 8212: 'mdash', 8230: 'hellip', 8216: 'lsquo', 8217: 'rsquo', 8220: 'ldquo', 8221: 'rdquo', 8226: 'bull', 8482: 'trade' };
  var basicas = { 38: 'amp', 60: 'lt', 62: 'gt', 34: 'quot' };
  function ent(nome) { return AMP + nome + ';'; }
  function num(cp) { return AMP + '#' + cp + ';'; }
  function codificar(texto) {
    return Array.from(texto).map(function (ch) {
      var cp = ch.codePointAt(0);
      if (basicas[cp]) { return ent(basicas[cp]); }
      if (cp === 39) { return num(39); }
      if (cp > 255) { return extras[cp] ? ent(extras[cp]) : num(cp); }
      if (cp >= 160) { return ent(nomes[cp - 160]); }
      if (cp > 127) { return num(cp); }
      return ch;
    }).join('');
  }
  function decodificar(texto) {
    var ta = document.createElement('textarea');
    ta.innerHTML = texto;
    return ta.value;
  }
  function montar(prefixo, funcao, vazio, msgErro) {
    var entrada = document.getElementById(prefixo + '-entrada');
    var caixa = document.getElementById(prefixo + '-resposta');
    var resultado = document.getElementById(prefixo + '-resultado');
    var btnCopiar = document.getElementById(prefixo + '-copiar');
    var saida = '';
    function erro(msg) {
      saida = '';
      caixa.style.borderColor = '#fca5a5';
      caixa.style.background = '#fef2f2';
      resultado.style.color = '#b91c1c';
      resultado.style.fontFamily = 'inherit';
      resultado.textContent = msg;
    }
    function converter() {
      var valor = entrada.value;
      if (valor.trim() === '') { erro(msgErro); return; }
      saida = funcao(valor);
      caixa.style.borderColor = '#86efac';
      caixa.style.background = '#f0fdf4';
      resultado.style.color = '#166534';
      resultado.style.fontFamily = 'ui-monospace,SFMono-Regular,Menlo,Consolas,monospace';
      resultado.textContent = saida;
    }
    function limpar() {
      saida = '';
      entrada.value = '';
      caixa.style.borderColor = '#c7d2fe';
      caixa.style.background = '#ffffff';
      resultado.style.color = '#64748b';
      resultado.style.fontFamily = 'inherit';
      resultado.textContent = vazio;
      entrada.focus();
    }
    function avisoCopiado(ok) {
      var original = btnCopiar.textContent;
      btnCopiar.textContent = ok ? 'Copiado!' : 'Falhou';
      setTimeout(function () { btnCopiar.textContent = original; }, 1500);
    }
    function copiar() {
      if (saida === '') { erro('gere um resultado antes de copiar.'); return; }
      if (navigator.clipboard) {
        if (navigator.clipboard.writeText) {
          navigator.clipboard.writeText(saida).then(function () { avisoCopiado(true); }, function () { avisoCopiado(false); });
          return;
        }
      }
      var tmp = document.createElement('textarea');
      tmp.value = saida;
      document.body.appendChild(tmp);
      tmp.select();
      var ok = false;
      try { ok = document.execCommand('copy'); } catch (e) { ok = false; }
      document.body.removeChild(tmp);
      avisoCopiado(ok);
    }
    document.getElementById(prefixo + '-btn').addEventListener('click', converter);
    document.getElementById(prefixo + '-limpar').addEventListener('click', limpar);
    btnCopiar.addEventListener('click', copiar);
    entrada.addEventListener('keydown', function (e) {
      if (e.key === 'Enter') {
        if (e.ctrlKey || e.metaKey) { converter(); }
      }
    });
    entrada.addEventListener('focus', function () { entrada.style.borderColor = '#6366f1'; });
    entrada.addEventListener('blur', function () { entrada.style.borderColor = '#c7d2fe'; });
  }
  montar('th-cod', codificar, 'digite o texto e clique em "Codificar".', 'digite um texto para codificar.');
  montar('th-dec', decodificar, 'cole o HTML e clique em "Decodificar".', 'digite um HTML para decodificar.');
})();
</script>

## Como usar o conversor

1. Para **codificar**, digite ou cole o texto no campo **Texto** da primeira seção.
2. Clique em **Codificar** (ou pressione Ctrl + Enter) e veja a **Resposta Codificada** logo abaixo do botão.
3. Para **decodificar**, cole o código com entidades HTML no campo **HTML** da segunda seção.
4. Clique em **Decodificar** (ou pressione Ctrl + Enter) para ver o texto original na **Resposta Decodificada**.
5. Use o botão **Copiar** para levar o resultado para a área de transferência e **Limpar** para apagar tudo e começar de novo.

A conversão acontece no seu navegador, sem enviar o texto para nenhum servidor. Letras acentuadas, cedilha, símbolos e emojis são convertidos; letras e números comuns permanecem iguais.

## Entendendo os termos

- **Texto simples:** conteúdo escrito sem formatação, exatamente como você digita no teclado.
- **HTML:** linguagem usada para construir páginas da web. Alguns caracteres têm significado especial nela e precisam ser escritos de outra forma.
- **Caractere especial:** qualquer símbolo que não seja letra ou número comum, como acentos (á, ç, ã), aspas, `<`, `>` e `©`.
- **Entidade HTML:** código que representa um caractere especial dentro do HTML. Começa com `&` e termina com `;`.
- **Entidade nomeada:** entidade que usa um nome fácil de lembrar, como `&Aacute;` para "Á" e `&copy;` para "©".
- **Entidade numérica:** entidade que usa o número do caractere, como `&#231;` para "ç". É usada quando o caractere não tem nome.
- **Codificar:** trocar os caracteres especiais do texto pelas entidades HTML correspondentes.
- **Decodificar:** fazer o inverso, trocando as entidades HTML pelos caracteres que elas representam.
- **Caracteres reservados:** `&`, `<`, `>` e aspas. Eles são codificados para que o navegador não os confunda com código HTML.

## Exemplo

O texto **Atenção: ação & reação** fica assim depois de codificado:

`Aten&ccedil;&atilde;o: a&ccedil;&atilde;o &amp; rea&ccedil;&atilde;o`

Ao decodificar esse resultado, você recupera o texto original.