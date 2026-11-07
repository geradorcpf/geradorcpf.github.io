---
title: "Prefixo e Sufixo"
seoTitle: "Prefixo e Sufixo"
description: "Prefixo e Sufixo: adicione prefixo e sufixo a cada linha de uma lista. Grátis e online, sem cadastro."
summary: "Adicione prefixo e sufixo a cada linha de uma lista."
date: 2026-11-07
draft: false
category: "texto"
tags: ["listas", "formatação", "texto"]
keywords: ["prefixo e sufixo", "prefixo e sufixo online", "listas", "formatação", "texto"]
---

Basta digitar sua lista abaixo (um item por linha), informar o prefixo e o sufixo e depois clicar em **Adicionar Prefixo/Sufixo**.

<div id="calc-prefixo-sufixo" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">✍️ Prefixo e Sufixo</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Adicione prefixo e sufixo a cada linha da sua lista.</p>
<label for="ps-texto" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Seu texto</label>
<textarea id="ps-texto" rows="6" placeholder="Um item por linha" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;font-family:inherit;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;resize:vertical;"></textarea>
<label for="ps-prefixo" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Prefixo</label>
<input id="ps-prefixo" type="text" placeholder="Ex.: (" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<label for="ps-sufixo" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Sufixo</label>
<input id="ps-sufixo" type="text" placeholder="Ex.: )," autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:20px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="ps-adicionar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Adicionar Prefixo/Sufixo</button>
<button type="button" id="ps-enumerar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Enumerar lista</button>
<button type="button" id="ps-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="ps-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resultado:</strong> <span id="ps-status">preencha o texto e clique em um dos botões.</span>
<textarea id="ps-resultado" rows="6" readonly style="width:100%;margin-top:12px;padding:12px 14px;font-size:1rem;font-family:inherit;border:2px solid #c7d2fe;border-radius:10px;background:#f8fafc;color:#1e293b;box-sizing:border-box;outline:none;resize:vertical;"></textarea>
<button type="button" id="ps-copiar" style="margin-top:12px;padding:10px 16px;font-size:0.95rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Copiar resultado</button>
</div>
</div>
<script>
(function () {
  var texto = document.getElementById('ps-texto');
  var prefixo = document.getElementById('ps-prefixo');
  var sufixo = document.getElementById('ps-sufixo');
  var resultado = document.getElementById('ps-resultado');
  var status = document.getElementById('ps-status');
  var caixa = document.getElementById('ps-resposta');
  var quebra = String.fromCharCode(10);
  function pegarLinhas() {
    return texto.value.split(/\r?\n/);
  }
  function vazia(linha) {
    return linha.trim() === '';
  }
  function erro(msg) {
    caixa.style.borderColor = '#fca5a5';
    caixa.style.background = '#fef2f2';
    status.style.color = '#b91c1c';
    status.textContent = msg;
    resultado.value = '';
  }
  function sucesso(linhas) {
    var total = linhas.filter(function (l) { return !vazia(l); }).length;
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    status.style.color = '#166534';
    status.textContent = total + (total === 1 ? ' linha processada.' : ' linhas processadas.');
    resultado.value = linhas.join(quebra);
  }
  function adicionar() {
    if (vazia(texto.value)) { erro('digite ou cole o seu texto primeiro.'); return; }
    if (prefixo.value === '' && sufixo.value === '') { erro('informe um prefixo, um sufixo ou os dois.'); return; }
    var saida = pegarLinhas().map(function (linha) {
      return vazia(linha) ? linha : prefixo.value + linha + sufixo.value;
    });
    sucesso(saida);
  }
  function enumerar() {
    if (vazia(texto.value)) { erro('digite ou cole o seu texto primeiro.'); return; }
    var n = 0;
    var saida = pegarLinhas().map(function (linha) {
      if (vazia(linha)) { return linha; }
      n = n + 1;
      return n + '. ' + linha;
    });
    sucesso(saida);
  }
  function limpar() {
    texto.value = '';
    prefixo.value = '';
    sufixo.value = '';
    resultado.value = '';
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    status.style.color = '#64748b';
    status.textContent = 'preencha o texto e clique em um dos botões.';
    texto.focus();
  }
  function copiar() {
    if (resultado.value === '') { return; }
    if (navigator.clipboard && navigator.clipboard.writeText) {
      navigator.clipboard.writeText(resultado.value);
    } else {
      resultado.select();
      document.execCommand('copy');
    }
    status.textContent = 'resultado copiado.';
  }
  document.getElementById('ps-adicionar').addEventListener('click', adicionar);
  document.getElementById('ps-enumerar').addEventListener('click', enumerar);
  document.getElementById('ps-limpar').addEventListener('click', limpar);
  document.getElementById('ps-copiar').addEventListener('click', copiar);
  [texto, prefixo, sufixo].forEach(function (el) {
    el.addEventListener('focus', function () { el.style.borderColor = '#6366f1'; });
    el.addEventListener('blur', function () { el.style.borderColor = '#c7d2fe'; });
  });
})();
</script>

## Como usar a ferramenta

1. Digite ou cole a sua lista no campo **Seu texto**, com um item por linha.
2. Informe o **Prefixo** (texto que vai antes de cada linha), o **Sufixo** (texto que vai depois) ou os dois.
3. Clique em **Adicionar Prefixo/Sufixo** para ver o resultado na caixa **Resultado**.
4. Se preferir numerar a lista (1., 2., 3. ...), clique em **Enumerar lista**. Nesse caso, o prefixo e o sufixo não são usados.
5. Use **Copiar resultado** para copiar o texto pronto e **Limpar** para apagar tudo e começar de novo.

As linhas em branco são mantidas como estão, sem prefixo, sufixo ou número. Espaços digitados no prefixo e no sufixo são mantidos, então você pode usar, por exemplo, um espaço depois de um hífen.

## Entendendo os termos

- **Prefixo:** texto adicionado no início de cada linha, antes do conteúdo original. Exemplo: aspas, parêntese, hífen ou o começo de um comando.
- **Sufixo:** texto adicionado no final de cada linha, depois do conteúdo original. Exemplo: vírgula, ponto e vírgula, aspas ou parêntese de fechamento.
- **Lista:** conjunto de itens escritos um por linha, como nomes, e-mails, números ou palavras.
- **Linha:** cada trecho de texto separado por uma quebra de linha (tecla Enter).
- **Enumerar lista:** numerar os itens em sequência (1, 2, 3...), um número para cada linha preenchida.
- **Resultado:** texto final, com o prefixo e o sufixo (ou a numeração) já aplicados em cada linha.