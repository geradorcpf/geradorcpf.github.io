---
title: "Contador de Caracteres, Palavras e Linhas"
seoTitle: "Contador de Caracteres, Palavras e Linhas"
description: "Contador de Caracteres, Palavras e Linhas: conte caracteres, palavras, linhas e parágrafos de qualquer texto. Grátis e online, sem cadastro."
summary: "Conte caracteres, palavras, linhas e parágrafos de qualquer texto."
date: 2026-10-25
draft: false
category: "texto"
tags: ["contador", "caracteres", "palavras", "texto"]
keywords: ["contador de caracteres, palavras e linhas", "contador de caracteres, palavras e linhas online", "contador", "caracteres", "palavras"]
---

<!--INI SUDAH DIKERJAKAN-->

Basta digitar ou colar o seu texto abaixo e o resultado aparece na hora, enquanto você escreve.

<div id="calc-contador" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">📝 Contador de Caracteres, Palavras e Linhas</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Digite ou cole o texto e veja a contagem na hora.</p>
<label for="cnt-texto" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Digite o texto</label>
<textarea id="cnt-texto" rows="8" placeholder="Escreva ou cole o seu texto aqui..." autocomplete="off" spellcheck="false" style="width:100%;padding:12px 14px;margin-bottom:20px;font-size:1rem;font-family:inherit;line-height:1.5;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;resize:vertical;"></textarea>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="cnt-limpar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Limpar Texto</button>
</div>
<div id="cnt-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #86efac;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;">
<strong style="color:#3730a3;">Resposta:</strong>
<div style="display:grid;grid-template-columns:repeat(auto-fit,minmax(130px,1fr));gap:10px;margin-top:12px;">
<div style="padding:12px;background:#f0fdf4;border:1px solid #86efac;border-radius:10px;text-align:center;"><div style="font-size:0.8rem;color:#475569;">Caracteres</div><div id="cnt-caracteres" style="font-size:1.3rem;font-weight:700;color:#166534;">0</div></div>
<div style="padding:12px;background:#f0fdf4;border:1px solid #86efac;border-radius:10px;text-align:center;"><div style="font-size:0.8rem;color:#475569;">Sem espaços</div><div id="cnt-semespacos" style="font-size:1.3rem;font-weight:700;color:#166534;">0</div></div>
<div style="padding:12px;background:#f0fdf4;border:1px solid #86efac;border-radius:10px;text-align:center;"><div style="font-size:0.8rem;color:#475569;">Palavras</div><div id="cnt-palavras" style="font-size:1.3rem;font-weight:700;color:#166534;">0</div></div>
<div style="padding:12px;background:#f0fdf4;border:1px solid #86efac;border-radius:10px;text-align:center;"><div style="font-size:0.8rem;color:#475569;">Espaços</div><div id="cnt-espacos" style="font-size:1.3rem;font-weight:700;color:#166534;">0</div></div>
<div style="padding:12px;background:#f0fdf4;border:1px solid #86efac;border-radius:10px;text-align:center;"><div style="font-size:0.8rem;color:#475569;">Linhas</div><div id="cnt-linhas" style="font-size:1.3rem;font-weight:700;color:#166534;">0</div></div>
<div style="padding:12px;background:#f0fdf4;border:1px solid #86efac;border-radius:10px;text-align:center;"><div style="font-size:0.8rem;color:#475569;">Parágrafos</div><div id="cnt-paragrafos" style="font-size:1.3rem;font-weight:700;color:#166534;">0</div></div>
<div style="padding:12px;background:#f0fdf4;border:1px solid #86efac;border-radius:10px;text-align:center;"><div style="font-size:0.8rem;color:#475569;">Vogais</div><div id="cnt-vogais" style="font-size:1.3rem;font-weight:700;color:#166534;">0</div></div>
<div style="padding:12px;background:#f0fdf4;border:1px solid #86efac;border-radius:10px;text-align:center;"><div style="font-size:0.8rem;color:#475569;">Números</div><div id="cnt-numeros" style="font-size:1.3rem;font-weight:700;color:#166534;">0</div></div>
</div>
</div>
</div>
<script>
(function () {
  var campo = document.getElementById('cnt-texto');
  function mostrar(id, valor) {
    document.getElementById('cnt-' + id).textContent = valor.toLocaleString('pt-BR');
  }
  function contar() {
    var t = campo.value;
    var limpo = t.trim();
    var caracteres = Array.from(t).length;
    var semEspacos = Array.from(t.replace(/\s/g, '')).length;
    var palavras = limpo === '' ? 0 : limpo.split(/\s+/).length;
    var espacos = (t.match(/ /g) || []).length;
    var linhas = t === '' ? 0 : t.split(/\r\n|\r|\n/).length;
    var paragrafos = limpo === '' ? 0 : limpo.split(/\n\s*\n/).length;
    var vogais = (t.normalize('NFD').replace(/[\u0300-\u036f]/g, '').match(/[aeiou]/gi) || []).length;
    var numeros = (t.match(/[0-9]/g) || []).length;
    mostrar('caracteres', caracteres);
    mostrar('semespacos', semEspacos);
    mostrar('palavras', palavras);
    mostrar('espacos', espacos);
    mostrar('linhas', linhas);
    mostrar('paragrafos', paragrafos);
    mostrar('vogais', vogais);
    mostrar('numeros', numeros);
  }
  function limpar() {
    campo.value = '';
    contar();
    campo.focus();
  }
  campo.addEventListener('input', contar);
  campo.addEventListener('focus', function () { campo.style.borderColor = '#6366f1'; });
  campo.addEventListener('blur', function () { campo.style.borderColor = '#c7d2fe'; });
  document.getElementById('cnt-limpar').addEventListener('click', limpar);
  contar();
})();
</script>

## Como usar o contador

1. Digite ou cole o seu texto no campo **Digite o texto**.
2. Veja os números na caixa **Resposta**: eles se atualizam sozinhos a cada letra digitada ou apagada.
3. Edite o texto quantas vezes quiser e acompanhe a contagem mudar na hora.
4. Clique em **Limpar Texto** para apagar tudo e começar uma nova contagem.

Você pode colar textos longos, com acentos, números, símbolos e quebras de linha. O texto é processado apenas no seu navegador e não é enviado para nenhum servidor.

## Entendendo os termos

- **Caracteres:** total de símbolos do texto, contando letras, números, pontuação, espaços e quebras de linha.
- **Caracteres sem espaços:** total de símbolos sem contar espaços, tabulações e quebras de linha.
- **Palavras:** sequências de caracteres separadas por espaço ou quebra de linha.
- **Espaços:** quantidade de espaços em branco entre palavras e símbolos do texto.
- **Linhas:** quantidade de linhas, contadas a cada vez que você pressiona Enter para quebrar a linha.
- **Parágrafos:** blocos de texto separados por uma ou mais linhas em branco.
- **Vogais:** quantidade das letras a, e, i, o, u, com ou sem acento (á, ã, é, ô etc.).
- **Números:** quantidade de dígitos de 0 a 9 presentes no texto. Por exemplo, "2026" tem 4 dígitos.

## Exemplo resolvido

Considere o texto abaixo, escrito em uma única linha:

`Ola mundo 2026`

1. **Caracteres:** O-l-a (3) + espaço (1) + m-u-n-d-o (5) + espaço (1) + 2-0-2-6 (4) = 14.
2. **Caracteres sem espaços:** 14 − 2 espaços = 12.
3. **Palavras:** "Ola", "mundo" e "2026" = 3.
4. **Espaços:** 2.
5. **Linhas:** 1.
6. **Vogais:** O, a, u, o = 4.
7. **Números:** 2, 0, 2, 6 = 4.

**Resposta:** o texto tem 14 caracteres (12 sem espaços), 3 palavras, 2 espaços, 1 linha, 4 vogais e 4 números.