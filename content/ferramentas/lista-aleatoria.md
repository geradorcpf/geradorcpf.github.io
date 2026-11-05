---
title: "Lista Aleatória"
seoTitle: "Lista Aleatória"
description: "Lista Aleatória: embaralhe uma lista em ordem aleatória. Grátis e online, sem cadastro."
summary: "Embaralhe uma lista em ordem aleatória."
date: 2026-11-05
draft: false
category: "aleatorio"
tags: ["sorteio", "listas", "embaralhar"]
keywords: ["lista aleatória", "lista aleatória online", "sorteio", "listas", "embaralhar"]
---

Digite ou cole sua lista abaixo (um item por linha) e clique em **Embaralhar Lista**.

<div id="calc-lista" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🔀 Lista Aleatória</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Cole os itens, um por linha, e embaralhe na hora.</p>
<label for="lis-texto" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Digite ou cole o texto</label>
<textarea id="lis-texto" rows="8" placeholder="Ex.:&#10;Ana&#10;Bruno&#10;Carla&#10;Diego" style="width:100%;padding:12px 14px;margin-bottom:12px;font-size:1rem;font-family:inherit;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;resize:vertical;"></textarea>
<label for="lis-enumerar" style="display:flex;align-items:center;gap:8px;margin-bottom:20px;font-weight:600;font-size:0.95rem;cursor:pointer;"><input id="lis-enumerar" type="checkbox" style="width:18px;height:18px;accent-color:#4f46e5;cursor:pointer;"> Enumerar lista aleatória</label>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="lis-embaralhar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Embaralhar Lista</button>
<button type="button" id="lis-copiar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Copiar</button>
<button type="button" id="lis-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="lis-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resultado:</strong><div id="lis-resultado" style="margin-top:6px;white-space:pre-wrap;word-break:break-word;">preencha a lista e clique em "Embaralhar Lista".</div></div>
</div>
<script>
(function () {
  var texto = document.getElementById('lis-texto');
  var enumerar = document.getElementById('lis-enumerar');
  var resultado = document.getElementById('lis-resultado');
  var caixa = document.getElementById('lis-resposta');
  var ultimo = '';
  var padrao = 'preencha a lista e clique em "Embaralhar Lista".';
  function erro(msg) {
    caixa.style.borderColor = '#fca5a5';
    caixa.style.background = '#fef2f2';
    resultado.style.color = '#b91c1c';
    resultado.textContent = msg;
    ultimo = '';
  }
  function sortear(max) {
    if (window.crypto && window.crypto.getRandomValues) {
      var buf = new Uint32Array(1);
      window.crypto.getRandomValues(buf);
      return buf[0] % max;
    }
    return Math.floor(Math.random() * max);
  }
  function embaralhar() {
    var linhas = texto.value.split(/\r?\n/).map(function (l) { return l.trim(); }).filter(function (l) { return l !== ''; });
    if (linhas.length === 0) { erro('digite pelo menos um item na lista.'); return; }
    for (var i = linhas.length - 1; i > 0; i--) {
      var j = sortear(i + 1);
      var tmp = linhas[i];
      linhas[i] = linhas[j];
      linhas[j] = tmp;
    }
    if (enumerar.checked) {
      linhas = linhas.map(function (l, idx) { return (idx + 1) + '. ' + l; });
    }
    ultimo = linhas.join('\n');
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    resultado.textContent = ultimo;
  }
  function copiar() {
    if (ultimo === '') { return; }
    if (navigator.clipboard && navigator.clipboard.writeText) {
      navigator.clipboard.writeText(ultimo);
    } else {
      var area = document.createElement('textarea');
      area.value = ultimo;
      document.body.appendChild(area);
      area.select();
      document.execCommand('copy');
      document.body.removeChild(area);
    }
    var btn = document.getElementById('lis-copiar');
    btn.textContent = 'Copiado!';
    setTimeout(function () { btn.textContent = 'Copiar'; }, 1500);
  }
  function limpar() {
    texto.value = '';
    enumerar.checked = false;
    ultimo = '';
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    resultado.style.color = '#64748b';
    resultado.textContent = padrao;
    texto.focus();
  }
  document.getElementById('lis-embaralhar').addEventListener('click', embaralhar);
  document.getElementById('lis-copiar').addEventListener('click', copiar);
  document.getElementById('lis-limpar').addEventListener('click', limpar);
  texto.addEventListener('focus', function () { texto.style.borderColor = '#6366f1'; });
  texto.addEventListener('blur', function () { texto.style.borderColor = '#c7d2fe'; });
})();
</script>

## Como usar a ferramenta

1. Digite ou cole sua lista no campo de texto, com **um item por linha**.
2. Se quiser que os itens saiam numerados, marque a opção **Enumerar lista aleatória**.
3. Clique em **Embaralhar Lista** para misturar os itens e ver o resultado.
4. Clique em **Embaralhar Lista** novamente para gerar uma nova ordem aleatória.
5. Use o botão **Copiar** para copiar o resultado e o botão **Limpar** para começar de novo.

Linhas em branco são ignoradas, e espaços extras no início e no fim de cada item são removidos. Itens repetidos são mantidos como você digitou.

## Entendendo os termos

- **Lista aleatória:** lista cujos itens foram colocados em uma ordem sorteada, sem seguir um padrão.
- **Embaralhar:** misturar os itens de uma lista, como se fossem cartas de baralho, para mudar a posição de cada um.
- **Item:** cada linha da lista, como um nome, uma palavra, um número ou uma frase.
- **Enumerar:** colocar um número na frente de cada item, mostrando a posição dele na lista (1., 2., 3. etc.).
- **Resultado:** a lista já embaralhada, que aparece abaixo dos botões.
- **Sorteio:** escolha feita ao acaso. Na lista embaralhada, o item que ficou em primeiro lugar pode ser usado como o sorteado.

## Exemplo

Suponha que você queira definir a ordem de apresentação de um grupo. Digite os nomes:

```
Ana
Bruno
Carla
Diego
```

Marque **Enumerar lista aleatória** e clique em **Embaralhar Lista**. Um resultado possível seria:

```
1. Carla
2. Ana
3. Diego
4. Bruno
```

Como a ordem é sorteada, cada clique pode gerar um resultado diferente.