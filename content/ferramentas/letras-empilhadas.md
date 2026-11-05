---
title: "Letras Empilhadas"
seoTitle: "Letras Empilhadas"
description: "Letras Empilhadas: empilhe as letras do seu texto em formatos criativos. Grátis e online, sem cadastro."
summary: "Empilhe as letras do seu texto em formatos criativos."
date: 2026-11-05
draft: false
category: "texto"
tags: ["letras personalizadas", "fontes", "texto"]
keywords: ["letras empilhadas", "letras empilhadas online", "letras personalizadas", "fontes", "texto"]
---

Digite seu texto abaixo, coloque o cursor onde deseja empilhar e clique nas letras. A letra escolhida aparece pequena, em cima do caractere anterior.

<div id="calc-empilhadas" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🔠 Gerador de Letras Empilhadas</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Digite o texto, posicione o cursor e clique nas letras.</p>
<label for="emp-texto" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Seu texto</label>
<textarea id="emp-texto" rows="3" placeholder="Ex.: você" autocomplete="off" style="width:100%;min-height:84px;padding:12px 14px;margin-bottom:16px;font-family:inherit;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;resize:vertical;"></textarea>
<label style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Letras para empilhar</label>
<div id="emp-letras" style="display:flex;gap:8px;flex-wrap:wrap;margin-bottom:20px;"></div>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="emp-copiar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Copiar Texto</button>
<button type="button" id="emp-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="emp-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="emp-resultado" style="white-space:pre-wrap;word-break:break-word;">digite um texto e clique nas letras para empilhar.</span><br><small id="emp-status" style="color:#475569;"></small></div>
</div>
<script>
(function () {
  var ta = document.getElementById('emp-texto');
  var grade = document.getElementById('emp-letras');
  var resultado = document.getElementById('emp-resultado');
  var status = document.getElementById('emp-status');
  var caixa = document.getElementById('emp-resposta');
  var padrao = 'digite um texto e clique nas letras para empilhar.';
  var tocado = false;
  var mapa = [
    ['a', 'ͣ'], ['e', 'ͤ'], ['i', 'ͥ'], ['o', 'ͦ'], ['u', 'ͧ'],
    ['b', 'ᷨ'], ['c', 'ͨ'], ['ç', 'ᷗ'], ['d', 'ͩ'], ['f', 'ᷫ'],
    ['g', 'ᷚ'], ['G', 'ᷛ'], ['h', 'ͪ'], ['k', 'ᷜ'], ['l', 'ᷝ'],
    ['L', 'ᷞ'], ['m', 'ͫ'], ['M', 'ᷟ'], ['n', 'ᷠ'], ['N', 'ᷡ'],
    ['p', 'ᷮ'], ['r', 'ͬ'], ['R', 'ᷢ'], ['s', 'ᷤ'], ['t', 'ͭ'],
    ['v', 'ͮ'], ['w', 'ᷱ'], ['x', 'ͯ'], ['z', 'ᷦ'], ['.', '̇']
  ];
  function neutro() {
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    resultado.style.color = '#64748b';
    status.style.color = '#475569';
  }
  function atualizar() {
    neutro();
    status.textContent = '';
    if (ta.value === '') {
      resultado.textContent = padrao;
    } else {
      resultado.textContent = ta.value;
      resultado.style.color = '#1e293b';
      resultado.style.fontSize = '1.2rem';
    }
    if (ta.value === '') { resultado.style.fontSize = '1rem'; }
  }
  function aviso(msg, ok) {
    status.textContent = msg;
    if (ok) {
      caixa.style.borderColor = '#86efac';
      caixa.style.background = '#f0fdf4';
      status.style.color = '#166534';
    } else {
      caixa.style.borderColor = '#fca5a5';
      caixa.style.background = '#fef2f2';
      status.style.color = '#b91c1c';
    }
  }
  function inserir(c) {
    var v = ta.value;
    var pos = tocado ? ta.selectionEnd : v.length;
    if (pos === 0) {
      aviso('digite uma letra antes e coloque o cursor depois dela.', false);
      ta.focus();
      return;
    }
    ta.value = v.slice(0, pos) + c + v.slice(pos);
    var novo = pos + c.length;
    ta.focus();
    try { ta.setSelectionRange(novo, novo); } catch (e) {}
    tocado = true;
    atualizar();
  }
  function copiadoOk() { aviso('texto copiado!', true); }
  function copiadoErro() { aviso('não foi possível copiar. Selecione o texto e copie manualmente.', false); }
  function copiarAntigo() {
    ta.focus();
    ta.select();
    try {
      if (document.execCommand('copy')) { copiadoOk(); } else { copiadoErro(); }
    } catch (e) { copiadoErro(); }
  }
  function copiar() {
    if (ta.value === '') { aviso('digite um texto antes de copiar.', false); return; }
    if (navigator.clipboard && navigator.clipboard.writeText) {
      navigator.clipboard.writeText(ta.value).then(copiadoOk, copiarAntigo);
    } else {
      copiarAntigo();
    }
  }
  function limpar() {
    ta.value = '';
    tocado = false;
    atualizar();
    ta.focus();
  }
  mapa.forEach(function (par) {
    var b = document.createElement('button');
    b.type = 'button';
    b.textContent = par[0];
    b.setAttribute('aria-label', 'Empilhar a letra ' + par[0]);
    b.style.cssText = 'min-width:42px;padding:10px 12px;font-size:1.05rem;font-weight:700;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;';
    b.addEventListener('mousedown', function (e) { e.preventDefault(); });
    b.addEventListener('mouseenter', function () { b.style.background = '#eef2ff'; });
    b.addEventListener('mouseleave', function () { b.style.background = '#ffffff'; });
    b.addEventListener('click', function () { inserir(par[1]); });
    grade.appendChild(b);
  });
  document.getElementById('emp-copiar').addEventListener('click', copiar);
  document.getElementById('emp-limpar').addEventListener('click', limpar);
  ta.addEventListener('input', function () { tocado = true; atualizar(); });
  ta.addEventListener('click', function () { tocado = true; });
  ta.addEventListener('keyup', function () { tocado = true; });
  ta.addEventListener('focus', function () { ta.style.borderColor = '#6366f1'; });
  ta.addEventListener('blur', function () { ta.style.borderColor = '#c7d2fe'; });
})();
</script>

## Como usar o gerador

1. Digite o seu texto no campo **Seu texto**.
2. Coloque o cursor logo depois da letra que receberá a letra pequena em cima.
3. Clique na letra desejada em **Letras para empilhar**. Ela é inserida na posição do cursor e aparece pequena, acima do caractere anterior.
4. Repita os passos 2 e 3 quantas vezes quiser, em qualquer parte do texto.
5. Clique em **Copiar Texto** para copiar o resultado e colar em redes sociais, apelidos (nicks), bios e mensagens.
6. Use o botão **Limpar** para apagar tudo e começar de novo.

Só é possível empilhar as letras que aparecem nos botões: a e i o u b c ç d f g G h k l L m M n N p r R s t v w x z e o ponto. Se o cursor estiver no início do campo, não há letra anterior para receber a letra pequena, então digite algo antes. Para desfazer uma letra empilhada, apague-a com a tecla Backspace, como qualquer outro caractere.

## Exemplos

- vͣoͫcͦê
- eͪnͣgͪrͣaͪçͣado
- mͫaͧsͥsͭaͦ

## Entendendo os termos

- **Letras empilhadas:** texto em que pequenas letras aparecem em cima de outras letras, como se fossem um expoente.
- **Letra empilhada (sobrescrita):** a letra pequena colocada acima do caractere anterior. Cada botão da ferramenta adiciona uma delas.
- **Cursor:** a barra que pisca no campo de texto e mostra onde o próximo caractere será inserido.
- **Caractere combinante:** caractere especial que não ocupa espaço próprio e se junta ao caractere que vem antes dele, subindo para cima da letra.
- **Unicode:** padrão que define os caracteres usados em computadores e celulares, incluindo as letrinhas combinantes usadas aqui.
- **Versalete:** letra com forma de maiúscula, mas em tamanho pequeno. É o caso das letras G, L, M, N e R da lista.
- **Nick:** apelido usado em jogos, perfis e redes sociais, onde as letras empilhadas costumam ser aplicadas.
- **Copiar Texto:** ação que copia o resultado para a área de transferência, pronto para colar em outro lugar.
- **Limpar:** ação que apaga todo o texto do campo para você começar um novo.

## Observações

O resultado é texto comum (Unicode), então pode ser colado onde você quiser. Em alguns aplicativos e fontes, as letras pequenas podem aparecer um pouco deslocadas ou não aparecer. Se isso acontecer, teste em outro aplicativo ou mude a fonte.