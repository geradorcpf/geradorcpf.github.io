---
title: "Remover Linhas Duplicadas"
seoTitle: "Remover Linhas Duplicadas"
description: "Remover Linhas Duplicadas: elimine linhas repetidas de uma lista ou texto. Grátis e online, sem cadastro."
summary: "Elimine linhas repetidas de uma lista ou texto."
date: 2026-11-08
draft: false
category: "texto"
tags: ["listas", "formatação", "texto"]
keywords: ["remover linhas duplicadas", "remover linhas duplicadas online", "listas", "formatação", "texto"]
---
<!--INI SUDAH DIKERJAKAN-->

Basta colar o texto ou a lista no campo abaixo e depois clicar em **Remover Duplicadas**.

<div id="calc-linhas" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🧹 Remover Linhas Duplicadas</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Digite ou cole o texto e elimine as linhas repetidas na hora.</p>
<label for="rld-entrada" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Texto original</label>
<textarea id="rld-entrada" rows="8" placeholder="Cole aqui o texto ou a lista, uma linha por item." autocomplete="off" spellcheck="false" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;font-family:inherit;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;resize:vertical;"></textarea>
<div style="display:flex;gap:10px;flex-wrap:wrap;margin-bottom:20px;">
<button type="button" id="rld-remover" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Remover Duplicadas</button>
<button type="button" id="rld-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<label for="rld-saida" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Resultado</label>
<textarea id="rld-saida" rows="8" readonly placeholder="O texto sem linhas duplicadas aparece aqui." style="width:100%;padding:12px 14px;margin-bottom:12px;font-size:1rem;font-family:inherit;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;resize:vertical;"></textarea>
<button type="button" id="rld-copiar" style="width:100%;padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Copiar Resultado</button>
<div id="rld-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="rld-info">cole o texto e clique em "Remover Duplicadas".</span></div>
</div>
<script>
(function () {
  var entrada = document.getElementById('rld-entrada');
  var saida = document.getElementById('rld-saida');
  var info = document.getElementById('rld-info');
  var caixa = document.getElementById('rld-resposta');
  var botaoCopiar = document.getElementById('rld-copiar');
  function estado(borda, fundo, cor, msg) {
    caixa.style.borderColor = borda;
    caixa.style.background = fundo;
    info.style.color = cor;
    info.textContent = msg;
  }
  function erro(msg) {
    estado('#fca5a5', '#fef2f2', '#b91c1c', msg);
  }
  function plural(n, singular, pluralTxt) {
    return n.toLocaleString('pt-BR') + ' ' + (n === 1 ? singular : pluralTxt);
  }
  function remover() {
    var texto = entrada.value;
    if (texto.trim() === '') {
      saida.value = '';
      erro('digite ou cole um texto no campo de cima.');
      return;
    }
    var linhas = texto.split(/\r?\n/);
    var vistas = new Set();
    var unicas = [];
    linhas.forEach(function (linha) {
      if (!vistas.has(linha)) {
        vistas.add(linha);
        unicas.push(linha);
      }
    });
    var removidas = linhas.length - unicas.length;
    saida.value = unicas.join('\n');
    var msg;
    if (removidas === 0) {
      msg = 'nenhuma linha duplicada encontrada. O texto tem ' + plural(linhas.length, 'linha', 'linhas') + '.';
    } else {
      msg = plural(removidas, 'linha duplicada removida', 'linhas duplicadas removidas') + '. O texto passou de ' + plural(linhas.length, 'linha', 'linhas') + ' para ' + plural(unicas.length, 'linha', 'linhas') + '.';
    }
    estado('#86efac', '#f0fdf4', '#166534', msg);
  }
  function limpar() {
    entrada.value = '';
    saida.value = '';
    estado('#c7d2fe', '#ffffff', '#64748b', 'cole o texto e clique em "Remover Duplicadas".');
    entrada.focus();
  }
  function copiar() {
    if (saida.value === '') {
      erro('não há resultado para copiar. Clique em "Remover Duplicadas" primeiro.');
      return;
    }
    function ok() {
      var original = botaoCopiar.textContent;
      botaoCopiar.textContent = 'Copiado!';
      setTimeout(function () { botaoCopiar.textContent = original; }, 1500);
    }
    function alternativa() {
      saida.focus();
      saida.select();
      try {
        document.execCommand('copy');
        ok();
      } catch (e) {
        erro('não foi possível copiar. Selecione o texto e copie manualmente.');
      }
    }
    if (navigator.clipboard && navigator.clipboard.writeText) {
      navigator.clipboard.writeText(saida.value).then(ok, alternativa);
    } else {
      alternativa();
    }
  }
  document.getElementById('rld-remover').addEventListener('click', remover);
  document.getElementById('rld-limpar').addEventListener('click', limpar);
  botaoCopiar.addEventListener('click', copiar);
  [entrada, saida].forEach(function (el) {
    el.addEventListener('focus', function () { el.style.borderColor = '#6366f1'; });
    el.addEventListener('blur', function () { el.style.borderColor = '#c7d2fe'; });
  });
})();
</script>

## Como usar a ferramenta

1. Digite ou cole o texto (ou a lista) no campo **Texto original**, com um item por linha.
2. Clique em **Remover Duplicadas** para eliminar as linhas repetidas.
3. Confira o texto limpo no campo **Resultado** e veja quantas linhas foram removidas.
4. Clique em **Copiar Resultado** para levar o texto para outro lugar.
5. Use o botão **Limpar** para apagar os campos e começar de novo.

A ferramenta mantém a primeira ocorrência de cada linha e preserva a ordem original. Linhas só são consideradas iguais quando têm exatamente o mesmo conteúdo, incluindo maiúsculas, minúsculas, acentos e espaços. Por isso, "Maçã" e "maçã" contam como linhas diferentes.

## Entendendo os termos

- **Linha:** trecho de texto que termina em uma quebra de linha (tecla Enter). Em uma lista, cada item costuma ocupar uma linha.
- **Linha duplicada:** linha com exatamente o mesmo conteúdo de outra que já apareceu antes no texto.
- **Lista:** conjunto de itens organizados um embaixo do outro, como nomes, e-mails, palavras-chave ou endereços.
- **Quebra de linha:** caractere invisível que separa uma linha da seguinte, criado ao pressionar Enter.
- **Primeira ocorrência:** a primeira vez que uma linha aparece no texto. Essa é a versão que fica no resultado.
- **Maiúsculas e minúsculas:** diferença entre letras grandes (A) e pequenas (a). Para esta ferramenta, elas fazem a linha ser diferente.
- **Linha vazia:** linha sem nenhum caractere. Se houver várias, apenas a primeira é mantida.