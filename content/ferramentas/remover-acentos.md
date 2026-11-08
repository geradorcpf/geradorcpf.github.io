---
title: "Remover Acentos de um Texto"
seoTitle: "Remover Acentos de um Texto"
description: "Remover Acentos de um Texto: tire acentos e cedilhas de qualquer texto. Grátis e online, sem cadastro."
summary: "Tire acentos e cedilhas de qualquer texto."
date: 2026-11-08
draft: false
category: "texto"
tags: ["acentos", "formatação", "texto"]
keywords: ["remover acentos de um texto", "remover acentos de um texto online", "acentos", "formatação", "texto"]
---

Basta digitar ou colar o texto abaixo e depois clicar em **Remover Acentos**.

<div id="calc-acentos" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🔤 Remover Acentos de um Texto</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Cole o texto e veja o resultado sem acentos na hora.</p>
<label for="acc-texto" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Texto</label>
<textarea id="acc-texto" rows="5" placeholder="Ex.: Atenção, João e José foram à escola." autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:20px;font-size:1rem;font-family:inherit;line-height:1.5;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;resize:vertical;"></textarea>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="acc-remover" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Remover Acentos</button>
<button type="button" id="acc-copiar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Copiar</button>
<button type="button" id="acc-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="acc-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="acc-resultado" style="white-space:pre-wrap;word-break:break-word;">digite o texto e clique em "Remover Acentos".</span></div>
</div>
<script>
(function () {
  var entrada = document.getElementById('acc-texto');
  var resultado = document.getElementById('acc-resultado');
  var caixa = document.getElementById('acc-resposta');
  var padrao = 'digite o texto e clique em "Remover Acentos".';
  var ultimo = '';
  function remover(t) {
    return t.normalize('NFD').replace(/[\u0300-\u036f]/g, '');
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
  function converter() {
    var texto = entrada.value;
    if (texto.trim() === '') {
      ultimo = '';
      erro('digite ou cole um texto para remover os acentos.');
      return;
    }
    ultimo = remover(texto);
    sucesso(ultimo);
  }
  function copiarAlternativo() {
    var area = document.createElement('textarea');
    area.value = ultimo;
    area.style.position = 'fixed';
    area.style.opacity = '0';
    document.body.appendChild(area);
    area.select();
    var ok = false;
    try { ok = document.execCommand('copy'); } catch (e) { ok = false; }
    document.body.removeChild(area);
    if (ok) { sucesso(ultimo); } else { erro('não foi possível copiar. Selecione o texto e copie manualmente.'); }
  }
  function copiar() {
    if (ultimo === '') {
      erro('clique primeiro em "Remover Acentos" para gerar o resultado.');
      return;
    }
    if (navigator.clipboard) {
      navigator.clipboard.writeText(ultimo).then(function () { sucesso(ultimo); }, copiarAlternativo);
    } else {
      copiarAlternativo();
    }
  }
  function limpar() {
    entrada.value = '';
    ultimo = '';
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    resultado.style.color = '#64748b';
    resultado.textContent = padrao;
    entrada.focus();
  }
  document.getElementById('acc-remover').addEventListener('click', converter);
  document.getElementById('acc-copiar').addEventListener('click', copiar);
  document.getElementById('acc-limpar').addEventListener('click', limpar);
  entrada.addEventListener('focus', function () { entrada.style.borderColor = '#6366f1'; });
  entrada.addEventListener('blur', function () { entrada.style.borderColor = '#c7d2fe'; });
})();
</script>

## Como usar a ferramenta

1. Digite ou cole o seu texto no campo **Texto**.
2. Clique em **Remover Acentos** para ver o texto sem acentos na caixa **Resposta**.
3. Clique em **Copiar** para levar o resultado para a área de transferência.
4. Use o botão **Limpar** para apagar o texto e começar de novo.

A ferramenta funciona com palavras, frases e textos longos, em maiúsculas ou minúsculas. Apenas os acentos e a cedilha são trocados pelas letras simples correspondentes. O restante do texto, como números, pontuação e espaços, permanece igual.

## Entendendo os termos

- **Acento:** sinal gráfico colocado sobre ou sob uma letra para indicar pronúncia, como em "é", "ê" e "ç".
- **Acento agudo (´):** marca a vogal tônica aberta ou a sílaba mais forte, como em "café" e "avó".
- **Acento grave (`):** indica a crase, como em "à" e "às".
- **Acento circunflexo (^):** marca a vogal tônica fechada, como em "você" e "avô".
- **Til (~):** indica som nasal, como em "mão" e "coração".
- **Cedilha (¸):** sinal sob o "c" que dá a ele som de "s", como em "criança". Ao remover, "ç" vira "c".
- **Trema (¨):** sinal sobre o "u" usado em palavras de origem estrangeira, como em "müller".
- **Caractere especial:** qualquer símbolo que não seja letra simples ou número, como acentos, "@" e "#".
- **Normalização Unicode:** processo que separa a letra do seu acento, permitindo remover só o sinal e manter a letra base.

## Exemplo resolvido

Um desenvolvedor precisa gerar um endereço (URL) a partir do título "Atenção: João e José foram à escola". Como acentos podem causar problemas em endereços e arquivos, ele quer o texto sem eles.

1. Cole o texto no campo: `Atenção: João e José foram à escola`.
2. Clique em **Remover Acentos**.
3. A ferramenta troca "ç" por "c", "ã" por "a", "é" por "e" e "à" por "a".

**Resposta:** `Atencao: Joao e Jose foram a escola`.