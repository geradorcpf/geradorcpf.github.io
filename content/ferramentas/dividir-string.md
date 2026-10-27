---
title: "Dividir String"
seoTitle: "Dividir String"
description: "Dividir String: divida um texto em partes usando um separador. Grátis e online, sem cadastro."
summary: "Divida um texto em partes usando um separador."
date: 2026-10-27
draft: false
category: "texto"
tags: ["string", "desenvolvimento", "texto"]
keywords: ["dividir string", "dividir string online", "string", "desenvolvimento", "texto"]
---
<!--sudah dikerjakan-->

Basta digitar o texto e a palavra (ou separador) abaixo e depois clicar em **Dividir o Texto**.

<div id="div-string" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">✂️ Dividir String</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Informe o texto e o separador e veja as partes na hora.</p>
<label for="div-texto" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Digite o texto</label>
<textarea id="div-texto" rows="5" placeholder="Ex.: maçã, banana, laranja, uva" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;font-family:inherit;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;resize:vertical;"></textarea>
<label for="div-separador" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Dividir usando esta palavra</label>
<input id="div-separador" type="text" placeholder="Ex.: , (vírgula)" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<div style="margin-bottom:20px;">
<div style="margin-bottom:8px;font-weight:600;font-size:0.95rem;">Opções</div>
<label for="div-ignorar-caixa" style="display:flex;align-items:center;gap:8px;margin-bottom:8px;font-size:0.95rem;cursor:pointer;"><input id="div-ignorar-caixa" type="checkbox" style="width:18px;height:18px;accent-color:#4f46e5;"> Ignorar maiúsculas e minúsculas</label>
<label for="div-aparar" style="display:flex;align-items:center;gap:8px;margin-bottom:8px;font-size:0.95rem;cursor:pointer;"><input id="div-aparar" type="checkbox" style="width:18px;height:18px;accent-color:#4f46e5;"> Remover espaços do início e do fim de cada parte</label>
<label for="div-remover-vazios" style="display:flex;align-items:center;gap:8px;font-size:0.95rem;cursor:pointer;"><input id="div-remover-vazios" type="checkbox" style="width:18px;height:18px;accent-color:#4f46e5;"> Remover partes vazias</label>
</div>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="div-dividir" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Dividir o Texto</button>
<button type="button" id="div-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="div-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="div-resultado">preencha os campos e clique em "Dividir o Texto".</span><div id="div-lista" style="margin-top:10px;"></div></div>
</div>
<script>
(function () {
  var texto = document.getElementById('div-texto');
  var sep = document.getElementById('div-separador');
  var optCaixa = document.getElementById('div-ignorar-caixa');
  var optAparar = document.getElementById('div-aparar');
  var optVazios = document.getElementById('div-remover-vazios');
  var resultado = document.getElementById('div-resultado');
  var lista = document.getElementById('div-lista');
  var caixa = document.getElementById('div-resposta');
  function interpretar(s) {
    return s.split('\\n').join('\n').split('\\t').join('\t');
  }
  function dividir(t, s, ignorar) {
    var partes = [];
    var base = ignorar ? t.toLowerCase() : t;
    var chave = ignorar ? s.toLowerCase() : s;
    var inicio = 0;
    while (true) {
      var pos = base.indexOf(chave, inicio);
      if (pos === -1) {
        partes.push(t.substring(inicio));
        break;
      }
      partes.push(t.substring(inicio, pos));
      inicio = pos + chave.length;
    }
    return partes;
  }
  function erro(msg) {
    caixa.style.borderColor = '#fca5a5';
    caixa.style.background = '#fef2f2';
    resultado.style.color = '#b91c1c';
    resultado.textContent = msg;
    lista.textContent = '';
  }
  function dividirTexto() {
    var t = texto.value;
    var s = interpretar(sep.value);
    if (t === '') { erro('digite o texto que deseja dividir.'); return; }
    if (s === '') { erro('informe a palavra ou o separador.'); return; }
    var partes = dividir(t, s, optCaixa.checked);
    if (optAparar.checked) {
      partes = partes.map(function (p) { return p.trim(); });
    }
    if (optVazios.checked) {
      partes = partes.filter(function (p) { return p !== ''; });
    }
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    lista.textContent = '';
    if (partes.length === 0) {
      resultado.textContent = 'nenhuma parte encontrada.';
      return;
    }
    resultado.textContent = 'o texto foi dividido em ' + partes.length + (partes.length === 1 ? ' parte:' : ' partes:');
    partes.forEach(function (p, i) {
      var linha = document.createElement('div');
      linha.style.cssText = 'padding:8px 10px;margin-bottom:6px;background:#eef2ff;border:1px solid #c7d2fe;border-radius:8px;color:#1e293b;white-space:pre-wrap;word-break:break-word;font-size:0.95rem;';
      var num = document.createElement('strong');
      num.style.color = '#3730a3';
      num.textContent = (i + 1) + '. ';
      var conteudo = document.createElement('span');
      conteudo.textContent = p === '' ? '(vazio)' : p;
      linha.appendChild(num);
      linha.appendChild(conteudo);
      lista.appendChild(linha);
    });
  }
  function limpar() {
    texto.value = '';
    sep.value = '';
    optCaixa.checked = false;
    optAparar.checked = false;
    optVazios.checked = false;
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    resultado.style.color = '#64748b';
    resultado.textContent = 'preencha os campos e clique em "Dividir o Texto".';
    lista.textContent = '';
    texto.focus();
  }
  document.getElementById('div-dividir').addEventListener('click', dividirTexto);
  document.getElementById('div-limpar').addEventListener('click', limpar);
  sep.addEventListener('keydown', function (e) { if (e.key === 'Enter') { dividirTexto(); } });
  [texto, sep].forEach(function (el) {
    el.addEventListener('focus', function () { el.style.borderColor = '#6366f1'; });
    el.addEventListener('blur', function () { el.style.borderColor = '#c7d2fe'; });
  });
})();
</script>

## Como usar a ferramenta

1. Digite ou cole o **texto** que você quer dividir no primeiro campo.
2. No segundo campo, informe a **palavra ou o separador** que marca onde o texto deve ser cortado (por exemplo, `,` ou `e`).
3. Se precisar, marque as **opções**: ignorar maiúsculas e minúsculas, remover espaços das pontas e remover partes vazias.
4. Clique em **Dividir o Texto** (ou pressione Enter no campo do separador) para ver as partes numeradas abaixo do botão.
5. Use o botão **Limpar** para apagar tudo e começar de novo.

Para dividir por quebra de linha ou tabulação, digite `\n` ou `\t` no campo do separador. O separador em si não aparece no resultado: ele só indica onde o texto é cortado.

## Entendendo os termos

- **String:** sequência de caracteres, ou seja, qualquer texto formado por letras, números, espaços e símbolos.
- **Dividir string:** cortar um texto em pedaços menores toda vez que um determinado trecho aparece.
- **Separador (delimitador):** palavra, caractere ou símbolo usado como ponto de corte, como vírgula, ponto e vírgula, espaço ou uma palavra inteira.
- **Parte:** cada pedaço de texto que sobra depois da divisão. Se o separador aparece 2 vezes, o texto é dividido em 3 partes.
- **Ignorar maiúsculas e minúsculas:** faz o separador ser encontrado independentemente da caixa das letras. Por exemplo, `e` também corta nos pontos onde aparece `E`.
- **Espaços do início e do fim:** espaços sobrando antes ou depois de cada parte. A opção de remover limpa esses espaços.
- **Parte vazia:** pedaço sem nenhum conteúdo, que surge quando há dois separadores seguidos ou quando o texto começa ou termina com o separador.
- **Quebra de linha (`\n`):** caractere especial que passa o texto para a linha seguinte.
- **Tabulação (`\t`):** caractere especial que cria um espaço largo, usado para alinhar colunas.