---
title: "Gerador de Senhas"
seoTitle: "Gerador de Senhas"
description: "Gerador de Senhas: crie senhas fortes e aleatórias com o tamanho que quiser. Grátis e online, sem cadastro."
summary: "Crie senhas fortes e aleatórias com o tamanho que quiser."
date: 2026-11-03
draft: false
category: "dev"
tags: ["senhas", "segurança", "gerador"]
keywords: ["gerador de senhas", "gerador de senhas online", "senhas", "segurança", "gerador"]
---
<!--INI SUDAH DIKERJAKAN-->

Basta escolher o tamanho e os tipos de caracteres abaixo e depois clicar em **Gerar Senha**.

<div id="calc-senha" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🔐 Gerador de Senhas</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Escolha as opções e gere senhas fortes na hora.</p>
<label for="sen-tamanho" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Tamanho da Senha (máximo 32)</label>
<input id="sen-tamanho" type="text" inputmode="numeric" value="12" placeholder="Ex.: 12" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<label style="display:flex;align-items:center;gap:10px;margin-bottom:10px;font-size:0.95rem;cursor:pointer;"><input id="sen-maiusculas" type="checkbox" checked style="width:18px;height:18px;accent-color:#4f46e5;cursor:pointer;">Incluir Letras Maiúsculas</label>
<label style="display:flex;align-items:center;gap:10px;margin-bottom:10px;font-size:0.95rem;cursor:pointer;"><input id="sen-minusculas" type="checkbox" checked style="width:18px;height:18px;accent-color:#4f46e5;cursor:pointer;">Incluir Letras Minúsculas</label>
<label style="display:flex;align-items:center;gap:10px;margin-bottom:10px;font-size:0.95rem;cursor:pointer;"><input id="sen-numeros" type="checkbox" checked style="width:18px;height:18px;accent-color:#4f46e5;cursor:pointer;">Incluir Números</label>
<label style="display:flex;align-items:center;gap:10px;margin-bottom:16px;font-size:0.95rem;cursor:pointer;"><input id="sen-especiais" type="checkbox" checked style="width:18px;height:18px;accent-color:#4f46e5;cursor:pointer;">Incluir Caracteres Especiais (!@#$%&amp;*()-+.,;?{[}]^&gt;&lt;:)</label>
<label for="sen-quantidade" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Número de Senhas Geradas (máximo 50)</label>
<input id="sen-quantidade" type="text" inputmode="numeric" value="1" placeholder="Ex.: 1" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:20px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="sen-gerar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Gerar Senha</button>
<button type="button" id="sen-copiar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Copiar</button>
<button type="button" id="sen-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="sen-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="sen-mensagem">escolha as opções e clique em "Gerar Senha".</span><div id="sen-lista"></div></div>
</div>
<script>
(function () {
  var tamanho = document.getElementById('sen-tamanho');
  var quantidade = document.getElementById('sen-quantidade');
  var chMai = document.getElementById('sen-maiusculas');
  var chMin = document.getElementById('sen-minusculas');
  var chNum = document.getElementById('sen-numeros');
  var chEsp = document.getElementById('sen-especiais');
  var caixa = document.getElementById('sen-resposta');
  var mensagem = document.getElementById('sen-mensagem');
  var lista = document.getElementById('sen-lista');
  var btnCopiar = document.getElementById('sen-copiar');
  var MAI = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ';
  var MIN = 'abcdefghijklmnopqrstuvwxyz';
  var NUM = '0123456789';
  var ESP = '!@#$%&*()-+.,;?{[}]^\x3E\x3C:';
  var atuais = [];
  function inteiro(v) {
    var t = String(v).trim();
    if (!/^\d+$/.test(t)) { return NaN; }
    return Number(t);
  }
  function sorteio(n) {
    var a = new Uint32Array(1);
    var limite = Math.floor(4294967296 / n) * n;
    do { crypto.getRandomValues(a); } while (a[0] >= limite);
    return a[0] % n;
  }
  function esvaziar() {
    while (lista.firstChild) { lista.removeChild(lista.firstChild); }
  }
  function erro(msg) {
    atuais = [];
    esvaziar();
    caixa.style.borderColor = '#fca5a5';
    caixa.style.background = '#fef2f2';
    mensagem.style.color = '#b91c1c';
    mensagem.textContent = msg;
  }
  function criarSenha(len, grupos, todos) {
    var chars = [];
    var i;
    for (i = 0; i !== grupos.length && chars.length !== len; i++) {
      chars.push(grupos[i].charAt(sorteio(grupos[i].length)));
    }
    while (chars.length !== len) {
      chars.push(todos.charAt(sorteio(todos.length)));
    }
    for (var j = chars.length - 1; j > 0; j--) {
      var k = sorteio(j + 1);
      var tmp = chars[j];
      chars[j] = chars[k];
      chars[k] = tmp;
    }
    return chars.join('');
  }
  function gerar() {
    var len = inteiro(tamanho.value);
    var qtd = inteiro(quantidade.value);
    if (isNaN(len) || len === 0 || len > 32) { erro('informe um tamanho entre 1 e 32.'); return; }
    if (isNaN(qtd) || qtd === 0 || qtd > 50) { erro('informe uma quantidade entre 1 e 50.'); return; }
    var grupos = [];
    if (chMai.checked) { grupos.push(MAI); }
    if (chMin.checked) { grupos.push(MIN); }
    if (chNum.checked) { grupos.push(NUM); }
    if (chEsp.checked) { grupos.push(ESP); }
    if (grupos.length === 0) { erro('selecione pelo menos um tipo de caractere.'); return; }
    var todos = grupos.join('');
    atuais = [];
    esvaziar();
    for (var n = 0; n !== qtd; n++) {
      var senha = criarSenha(len, grupos, todos);
      atuais.push(senha);
      var linha = document.createElement('div');
      linha.textContent = senha;
      linha.style.cssText = 'margin-top:8px;padding:10px 12px;background:#f0fdf4;border:1px solid #86efac;border-radius:8px;font-family:ui-monospace,SFMono-Regular,Menlo,Consolas,monospace;font-size:1.05rem;font-weight:700;color:#166534;word-break:break-all;';
      lista.appendChild(linha);
    }
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    mensagem.style.color = '#166534';
    mensagem.textContent = qtd === 1 ? 'senha gerada com sucesso.' : 'senhas geradas com sucesso.';
  }
  function copiar() {
    if (atuais.length === 0) { return; }
    var texto = atuais.join('\n');
    function feito() {
      btnCopiar.textContent = 'Copiado!';
      setTimeout(function () { btnCopiar.textContent = 'Copiar'; }, 1500);
    }
    function alternativa() {
      var area = document.createElement('textarea');
      area.value = texto;
      area.style.position = 'fixed';
      area.style.opacity = '0';
      document.body.appendChild(area);
      area.select();
      try { document.execCommand('copy'); feito(); } catch (e) {}
      document.body.removeChild(area);
    }
    if (navigator.clipboard && navigator.clipboard.writeText) {
      navigator.clipboard.writeText(texto).then(feito, alternativa);
    } else {
      alternativa();
    }
  }
  function limpar() {
    tamanho.value = '12';
    quantidade.value = '1';
    chMai.checked = true;
    chMin.checked = true;
    chNum.checked = true;
    chEsp.checked = true;
    atuais = [];
    esvaziar();
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    mensagem.style.color = '#64748b';
    mensagem.textContent = 'escolha as opções e clique em "Gerar Senha".';
    tamanho.focus();
  }
  document.getElementById('sen-gerar').addEventListener('click', gerar);
  btnCopiar.addEventListener('click', copiar);
  document.getElementById('sen-limpar').addEventListener('click', limpar);
  [tamanho, quantidade].forEach(function (el) {
    el.addEventListener('keydown', function (e) { if (e.key === 'Enter') { gerar(); } });
    el.addEventListener('focus', function () { el.style.borderColor = '#6366f1'; });
    el.addEventListener('blur', function () { el.style.borderColor = '#c7d2fe'; });
  });
})();
</script>

## Como usar o gerador

1. Digite o **Tamanho da Senha** no primeiro campo (de 1 a 32 caracteres).
2. Marque os tipos de caracteres que deseja usar: **letras maiúsculas**, **letras minúsculas**, **números** e **caracteres especiais**.
3. Informe o **Número de Senhas Geradas** (de 1 a 50) se quiser várias senhas de uma vez.
4. Clique em **Gerar Senha** (ou pressione Enter) para ver o resultado.
5. Use o botão **Copiar** para levar as senhas para a área de transferência e o botão **Limpar** para voltar às opções iniciais.

Pelo menos um tipo de caractere precisa estar marcado. Quanto maior a senha e mais tipos de caracteres você usar, mais forte ela fica. Cada senha gerada contém ao menos um caractere de cada tipo selecionado, desde que o tamanho permita.

## Entendendo os termos

- **Senha:** sequência de caracteres usada para provar sua identidade e proteger o acesso a contas, aplicativos e arquivos.
- **Senha forte:** senha longa, imprevisível e que mistura diferentes tipos de caracteres, o que a torna difícil de adivinhar ou descobrir.
- **Senha aleatória:** senha formada por caracteres sorteados, sem seguir nomes, datas ou padrões que alguém possa deduzir.
- **Tamanho da senha:** quantidade de caracteres da senha. Neste gerador, o máximo é de 32.
- **Letras maiúsculas:** letras de A a Z escritas em caixa alta, como `A`, `B` e `C`.
- **Letras minúsculas:** letras de a a z escritas em caixa baixa, como `a`, `b` e `c`.
- **Números:** dígitos de 0 a 9.
- **Caracteres especiais:** símbolos como `!@#$%&*()-+.,;?{[}]^><:`, que aumentam a variedade da senha.
- **Número de senhas geradas:** quantidade de senhas diferentes criadas de uma só vez a cada clique em **Gerar Senha**.
- **Ataque de força bruta:** técnica em que o invasor testa todas as combinações possíveis até acertar a senha. Senhas longas e variadas tornam esse ataque muito mais demorado.