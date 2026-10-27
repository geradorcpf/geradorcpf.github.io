---
title: "Emoticons para Copiar"
seoTitle: "Emoticons para Copiar"
description: "Emoticons para Copiar: copie emoticons de texto com um clique. Grátis e online, sem cadastro."
summary: "Copie emoticons de texto com um clique."
date: 2026-10-27
draft: false
category: "texto"
tags: ["emoticons", "símbolos", "copiar e colar", "redes sociais"]
keywords: ["emoticons para copiar", "emoticons para copiar online", "emoticons", "símbolos", "copiar e colar"]
---
<!--sudah dikerjakan-->

Basta clicar no emoticon desejado abaixo para copiá-lo e depois colar onde quiser.

<div id="calc-emoticons" style="max-width:720px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">😊 Emoticons para Copiar</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Clique em um emoticon para copiá-lo na hora.</p>
<div id="emo-grade" style="display:grid;grid-template-columns:repeat(auto-fill,minmax(140px,1fr));gap:10px;margin-bottom:20px;"></div>
<div id="emo-resposta" aria-live="polite" style="padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;word-break:break-word;"><strong style="color:#3730a3;">Resposta:</strong> <span id="emo-resultado">clique em um emoticon para copiar.</span></div>
</div>
<script>
(function () {
  var dados = [
    "( ͡° ͜ʖ ͡°)", "( ͡ᵔ ͜ʖ ͡ᵔ )", "( ͡ಠ ʖ̯ ͡ಠ)", "( ͠° ͟ʖ ͡°)", "(ง ͠° ͜ʖ ͡°)ง",
    "( ͡~ ͜ʖ ͡~)", "( ͡° _ʖ ͡°)", "( ͡ᵔ ͜ʖ ͡°)", "( ͡~ ͜ʖ ͡°)", "( ͡° ʖ̯ ͡°)",
    "( ͡ಠ ͜ʖ ͡ಠ)", "( ͡°ε ͡°)", "(͡° ͜ʖ ͡°)", "( ͡° ᴥ ͡°)", "(ㆆ_ㆆ)",
    "( ˘︹˘ )", "(´✪‿✪`)", "( ⚆ _ ⚆ )", "(●__●)", "(●'◡'●)",
    "('⌒')", "(⌒_⌒;)", "(*^‿^*)", "٩(⁎❛ᴗ❛⁎)۶", "ʘل͟ʘ",
    "ʘ‿ʘ", "ಠ_ಠ", "ó_ò", "♥‿♥", "(¬‿¬)",
    "(｡◕‿◕｡)", "(°◡°♡)", "(◡‿◡✿)", "(♡´౪`♡)", "ʕ•ᴥ•ʔ",
    "ฅʕ•ᴥ•ʔฅ", "(ᵔᴥᵔ)", "o(*°▽°*)o", "(っ◔◡◔)っ", "ԅ(¯﹃¯ԅ)",
    "(ง︡'-'︠)ง", "ᕙ(⇀‸↼‶)ᕗ", "ᕙ(`▿´)ᕗ", "¯\\_(ツ)_/¯", "¯\\(°_o)/¯",
    "ᕦ( ͡° ͜ʖ ͡°)ᕤ", "ᕦ(ò_óˇ)ᕤ", "╰(*°▽°*)╯", "╭∩╮( ͡⚆ ͜ʖ ͡⚆)╭∩╮", "┌∩┐(◣_◢)┌∩┐",
    "[̲̅$̲̅(̲̅ ͡° ͜ʖ ͡°̲̅)̲̅$̲̅]", "ヽ༼ຈل͜ຈ༽ﾉ", "ᕙ༼ຈل͜ຈ༽ᕗ", "ヽ༼ʘ̚ل͜ʘ̚༽ﾉ", "ヽ༼◉ل͜◉༽ﾉ",
    "ヽ༼◔ل͜◔༽ﾉ", "ヽ༼☉ل͜☉༽ﾉ", "ヽ༼ಠل͜ಠ༽ﾉ", "༼ ಥل͟ಥ ༽", "༼ つ ◕‿◕ ༽つ",
    "[\u003C()\u003E]", "[̲̅$̲̅(̲̅ιοο̲̅)̲̅$̲̅]", "■■□□□40%", "❚█══█❚"
  ];
  var grade = document.getElementById('emo-grade');
  var resultado = document.getElementById('emo-resultado');
  var caixa = document.getElementById('emo-resposta');
  var estiloBotao = "padding:12px 10px;font-size:1rem;line-height:1.5;color:#1e293b;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;box-sizing:border-box;min-height:48px;overflow-wrap:anywhere;";
  function sucesso(texto) {
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    resultado.textContent = '';
    resultado.appendChild(document.createTextNode('copiado! '));
    var forte = document.createElement('strong');
    forte.style.fontSize = '1.2rem';
    forte.textContent = texto;
    resultado.appendChild(forte);
  }
  function erro() {
    caixa.style.borderColor = '#fca5a5';
    caixa.style.background = '#fef2f2';
    resultado.style.color = '#b91c1c';
    resultado.textContent = 'não foi possível copiar. Selecione o emoticon e copie manualmente.';
  }
  function alternativa(texto) {
    var area = document.createElement('textarea');
    area.value = texto;
    area.setAttribute('readonly', '');
    area.style.position = 'fixed';
    area.style.top = '0';
    area.style.left = '0';
    area.style.opacity = '0';
    document.body.appendChild(area);
    area.select();
    var ok = false;
    try { ok = document.execCommand('copy'); } catch (e) { ok = false; }
    document.body.removeChild(area);
    if (ok) { sucesso(texto); } else { erro(); }
  }
  function copiar(texto) {
    if (navigator.clipboard && navigator.clipboard.writeText) {
      navigator.clipboard.writeText(texto).then(function () { sucesso(texto); }, function () { alternativa(texto); });
    } else {
      alternativa(texto);
    }
  }
  dados.forEach(function (texto) {
    var botao = document.createElement('button');
    botao.type = 'button';
    botao.style.cssText = estiloBotao;
    botao.textContent = texto;
    botao.setAttribute('title', 'Copiar ' + texto);
    botao.addEventListener('click', function () { copiar(texto); });
    botao.addEventListener('mouseenter', function () { botao.style.borderColor = '#6366f1'; botao.style.background = '#eef2ff'; });
    botao.addEventListener('mouseleave', function () { botao.style.borderColor = '#c7d2fe'; botao.style.background = '#ffffff'; });
    botao.addEventListener('focus', function () { botao.style.borderColor = '#6366f1'; });
    botao.addEventListener('blur', function () { botao.style.borderColor = '#c7d2fe'; });
    grade.appendChild(botao);
  });
})();
</script>

## Como usar a ferramenta

1. Role a lista e escolha o emoticon que combina com a sua mensagem.
2. Clique no emoticon para copiá-lo automaticamente.
3. Confira a confirmação **copiado!** na caixa de resposta abaixo da lista.
4. Cole o emoticon (Ctrl + V no computador ou toque e segure no celular) no WhatsApp, Instagram, Facebook ou em qualquer campo de texto.

Os emoticons são texto comum, então funcionam em qualquer rede social, bate-papo, comentário ou bio. Em alguns aplicativos, o desenho pode variar um pouco conforme a fonte usada.

## Entendendo os termos

- **Emoticon:** sequência de letras, números e símbolos que forma um rosto ou uma expressão, como `ಠ_ಠ`, usada para transmitir emoção em textos.
- **Emoji:** pequena imagem colorida padronizada, diferente do emoticon, que é montado apenas com caracteres de texto.
- **Lenny face:** emoticon `( ͡° ͜ʖ ͡°)`, de rosto malicioso ou brincalhão, muito popular na internet.
- **Donger:** emoticon de braços levantados, como `ヽ༼ຈل͜ຈ༽ﾉ`, usado para expressar empolgação ou celebração.
- **Kaomoji:** estilo japonês de emoticon que se lê de frente, como `(｡◕‿◕｡)`, geralmente com carinhas fofas e expressivas.
- **Caractere Unicode:** símbolo padronizado que pode ser exibido em diferentes dispositivos e sistemas, base de quase todos os emoticons.
- **Copiar e colar:** ação de duplicar o emoticon para a área de transferência e inseri-lo em outro lugar.
- **Área de transferência:** espaço temporário do aparelho onde o item copiado fica guardado até ser colado.