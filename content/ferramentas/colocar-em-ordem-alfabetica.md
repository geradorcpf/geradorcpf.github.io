---
title: "Colocar em Ordem Alfabética"
seoTitle: "Colocar em Ordem Alfabética"
description: "Colocar em Ordem Alfabética: ordene uma lista de palavras em ordem alfabética. Grátis e online, sem cadastro."
summary: "Ordene uma lista de palavras em ordem alfabética."
date: 2026-10-24
draft: false
category: "texto"
tags: ["ordem alfabética", "listas", "texto"]
keywords: ["colocar em ordem alfabética", "colocar em ordem alfabética online", "ordem alfabética", "listas", "texto"]
---

<!--sudah dikerjakan-->

Basta colar a sua lista abaixo, escolher as opções e depois clicar em **Ordenar**.

<div id="calc-ordem-alfabetica" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🔤 Colocar em Ordem Alfabética</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Cole a lista, escolha as opções e veja o resultado na hora.</p>
<label for="ord-texto" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">1. Texto original</label>
<textarea id="ord-texto" maxlength="10000" rows="6" placeholder="Ex.: Maçã, banana, abacaxi, Laranja" style="width:100%;min-height:130px;padding:12px 14px;margin-bottom:4px;font-size:1rem;font-family:inherit;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;resize:vertical;"></textarea>
<div id="ord-contador" style="margin-bottom:16px;font-size:0.8rem;color:#64748b;text-align:right;">0/10.000 caracteres</div>
<div style="margin-bottom:6px;font-weight:600;font-size:0.95rem;">2. Tipo de ordenação</div>
<div style="display:flex;gap:8px;flex-wrap:wrap;margin-bottom:16px;">
<label style="display:flex;align-items:center;gap:6px;padding:8px 12px;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;font-size:0.9rem;cursor:pointer;"><input type="radio" name="ord-tipo" value="asc" checked> Ascendente (A-Z)</label>
<label style="display:flex;align-items:center;gap:6px;padding:8px 12px;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;font-size:0.9rem;cursor:pointer;"><input type="radio" name="ord-tipo" value="desc"> Descendente (Z-A)</label>
</div>
<div style="margin-bottom:6px;font-weight:600;font-size:0.95rem;">3. Ordenar por</div>
<div style="display:flex;gap:8px;flex-wrap:wrap;margin-bottom:16px;">
<label style="display:flex;align-items:center;gap:6px;padding:8px 12px;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;font-size:0.9rem;cursor:pointer;"><input type="radio" name="ord-separador" value="linha" checked> Quebra de Linha</label>
<label style="display:flex;align-items:center;gap:6px;padding:8px 12px;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;font-size:0.9rem;cursor:pointer;"><input type="radio" name="ord-separador" value="espaco"> Espaço</label>
<label style="display:flex;align-items:center;gap:6px;padding:8px 12px;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;font-size:0.9rem;cursor:pointer;"><input type="radio" name="ord-separador" value="virgula"> Vírgula ( , )</label>
<label style="display:flex;align-items:center;gap:6px;padding:8px 12px;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;font-size:0.9rem;cursor:pointer;"><input type="radio" name="ord-separador" value="pontovirgula"> Ponto e Vírgula ( ; )</label>
</div>
<div style="margin-bottom:6px;font-weight:600;font-size:0.95rem;">4. Remover Duplicados?</div>
<label style="display:inline-flex;align-items:center;gap:6px;padding:8px 12px;margin-bottom:20px;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;font-size:0.9rem;cursor:pointer;"><input type="checkbox" id="ord-duplicados"> Sim, remover itens repetidos</label>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="ord-ordenar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Ordenar</button>
<button type="button" id="ord-copiar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Copiar</button>
<button type="button" id="ord-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="ord-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="ord-resultado">cole a lista e clique em "Ordenar".</span></div>
<label for="ord-saida" style="display:block;margin:16px 0 6px;font-weight:600;font-size:0.95rem;">Texto ordenado</label>
<textarea id="ord-saida" rows="6" readonly placeholder="O resultado aparece aqui." style="width:100%;min-height:130px;padding:12px 14px;font-size:1rem;font-family:inherit;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;resize:vertical;"></textarea>
</div>
<script>
(function () {
  var texto = document.getElementById('ord-texto');
  var contador = document.getElementById('ord-contador');
  var saida = document.getElementById('ord-saida');
  var resultado = document.getElementById('ord-resultado');
  var caixa = document.getElementById('ord-resposta');
  var duplicados = document.getElementById('ord-duplicados');
  var collator = new Intl.Collator('pt-BR', { numeric: true, sensitivity: 'base' });
  var padrao = 'cole a lista e clique em "Ordenar".';
  function valorRadio(nome) {
    var el = document.querySelector('input[name="' + nome + '"]:checked');
    return el ? el.value : '';
  }
  function atualizarContador() {
    contador.textContent = texto.value.length.toLocaleString('pt-BR') + '/10.000 caracteres';
  }
  function erro(msg) {
    caixa.style.borderColor = '#fca5a5';
    caixa.style.background = '#fef2f2';
    resultado.style.color = '#b91c1c';
    resultado.textContent = msg;
  }
  function sucesso(msg) {
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    resultado.textContent = msg;
  }
  function ordenar() {
    var bruto = texto.value;
    var separador = valorRadio('ord-separador');
    var tipo = valorRadio('ord-tipo');
    var partes;
    if (bruto.trim() === '') {
      saida.value = '';
      erro('digite ou cole uma lista no campo "Texto original".');
      return;
    }
    if (separador === 'espaco') { partes = bruto.split(/\s+/); }
    else if (separador === 'virgula') { partes = bruto.split(','); }
    else if (separador === 'pontovirgula') { partes = bruto.split(';'); }
    else { partes = bruto.split(/\r?\n/); }
    var itens = partes.map(function (p) { return p.trim(); }).filter(function (p) { return p !== ''; });
    var total = itens.length;
    if (duplicados.checked) {
      var vistos = new Set();
      itens = itens.filter(function (p) {
        if (vistos.has(p)) { return false; }
        vistos.add(p);
        return true;
      });
    }
    itens.sort(function (a, b) {
      return tipo === 'desc' ? collator.compare(b, a) : collator.compare(a, b);
    });
    var juntar = { linha: '\n', espaco: ' ', virgula: ', ', pontovirgula: '; ' };
    saida.value = itens.join(juntar[separador] || '\n');
    var msg = itens.length + ' item(ns) em ordem ' + (tipo === 'desc' ? 'descendente (Z-A)' : 'ascendente (A-Z)') + '.';
    if (total !== itens.length) { msg += ' Duplicados removidos: ' + (total - itens.length) + '.'; }
    sucesso(msg);
  }
  function copiar() {
    if (saida.value === '') { erro('não há texto ordenado para copiar.'); return; }
    saida.select();
    try {
      if (navigator.clipboard) { navigator.clipboard.writeText(saida.value); }
      else { document.execCommand('copy'); }
      sucesso('texto ordenado copiado.');
    } catch (e) {
      erro('não foi possível copiar automaticamente. Selecione o texto e copie manualmente.');
    }
  }
  function limpar() {
    texto.value = '';
    saida.value = '';
    duplicados.checked = false;
    document.querySelector('input[name="ord-tipo"][value="asc"]').checked = true;
    document.querySelector('input[name="ord-separador"][value="linha"]').checked = true;
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    resultado.style.color = '#64748b';
    resultado.textContent = padrao;
    atualizarContador();
    texto.focus();
  }
  document.getElementById('ord-ordenar').addEventListener('click', ordenar);
  document.getElementById('ord-copiar').addEventListener('click', copiar);
  document.getElementById('ord-limpar').addEventListener('click', limpar);
  texto.addEventListener('input', atualizarContador);
  [texto, saida].forEach(function (el) {
    el.addEventListener('focus', function () { el.style.borderColor = '#6366f1'; });
    el.addEventListener('blur', function () { el.style.borderColor = '#c7d2fe'; });
  });
})();
</script>

## Como usar a ferramenta

1. Cole ou digite a sua lista no campo **Texto original** (até 10.000 caracteres).
2. Em **Tipo de ordenação**, escolha **Ascendente (A-Z)** ou **Descendente (Z-A)**.
3. Em **Ordenar por**, indique como os itens estão separados: quebra de linha, espaço, vírgula ou ponto e vírgula.
4. Marque **Remover Duplicados?** se quiser eliminar os itens repetidos.
5. Clique em **Ordenar** e veja o resultado no campo **Texto ordenado**.
6. Use **Copiar** para levar o resultado para a área de transferência e **Limpar** para começar uma nova lista.

A ordenação segue o alfabeto português: acentos e letras maiúsculas ou minúsculas não mudam a posição (por exemplo, "Álvaro" fica junto de "alvaro"). Números dentro dos itens são comparados pelo valor, então "item 2" vem antes de "item 10". Espaços extras no início e no fim de cada item e itens vazios são ignorados. O resultado usa o mesmo separador escolhido na entrada.

## Entendendo os termos

- **Ordem alfabética:** organização dos itens seguindo a sequência das letras do alfabeto, de A a Z.
- **Texto original:** a lista que você cola na ferramenta, com os itens que serão organizados.
- **Ascendente (A-Z):** ordenação do início ao fim do alfabeto, da letra A até a letra Z.
- **Descendente (Z-A):** ordenação inversa, da letra Z até a letra A.
- **Ordenar por:** define o caractere que separa um item do outro no texto original.
- **Quebra de Linha:** cada item fica em uma linha própria, separado pela tecla Enter.
- **Espaço:** os itens são palavras separadas por um ou mais espaços.
- **Vírgula ( , ):** os itens são separados por vírgula, como em "banana, maçã, uva".
- **Ponto e Vírgula ( ; ):** os itens são separados por ponto e vírgula, como em "banana; maçã; uva".
- **Remover Duplicados:** opção que mantém apenas uma ocorrência de cada item repetido na lista.
- **Texto ordenado:** o resultado final, com a lista já organizada conforme as opções escolhidas.

## Exemplo resolvido

Suponha a lista abaixo, separada por vírgula, com a ordenação **Ascendente (A-Z)**:

`Maçã, banana, abacaxi, Laranja`

1. Escolha **Vírgula ( , )** em **Ordenar por** e **Ascendente (A-Z)** em **Tipo de ordenação**.
2. Clique em **Ordenar**.
3. Os itens são comparados letra a letra, sem diferenciar maiúsculas de minúsculas.

**Resposta:** `abacaxi, banana, Laranja, Maçã`