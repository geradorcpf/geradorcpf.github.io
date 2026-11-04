---
title: "Instagram Anônimo"
seoTitle: "Instagram Anônimo"
description: "Instagram Anônimo: visualize perfis públicos do Instagram sem entrar na conta. Grátis e online, sem cadastro."
summary: "Visualize perfis públicos do Instagram sem entrar na conta."
date: 2026-11-04
draft: false
category: "social"
tags: ["instagram", "privacidade", "redes sociais"]
keywords: ["instagram anônimo", "instagram anônimo online", "instagram", "privacidade", "redes sociais"]
---

Veja stories no Instagram sem aparecer na lista de visualizações. Verifique se o seu navegador é compatível e instale a extensão pelo botão abaixo.

<div id="ig-anonimo" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🕶️ Instagram Anônimo</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Extensão para o navegador Chrome (ou Kiwi Browser no Android).</p>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<a id="ig-instalar" href="https://chromewebstore.google.com/detail/anonymous-stories/djagffgjghpihfffmiomblhinennkkig" target="_blank" rel="noopener noreferrer" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);text-align:center;text-decoration:none;box-sizing:border-box;">Instalar extensão</a>
<button type="button" id="ig-verificar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Verificar navegador</button>
</div>
<div id="ig-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="ig-resultado">clique em "Verificar navegador" para saber se a extensão funciona no seu aparelho.</span></div>
</div>
<script>
(function () {
  var botao = document.getElementById('ig-verificar');
  var resultado = document.getElementById('ig-resultado');
  var caixa = document.getElementById('ig-resposta');
  function mostrar(ok, msg) {
    caixa.style.borderColor = ok ? '#86efac' : '#fca5a5';
    caixa.style.background = ok ? '#f0fdf4' : '#fef2f2';
    resultado.style.color = ok ? '#166534' : '#b91c1c';
    resultado.textContent = msg;
  }
  function verificar() {
    var ua = navigator.userAgent || '';
    var chromium = ua.indexOf('Chrome') > -1 || ua.indexOf('Chromium') > -1;
    var android = ua.indexOf('Android') > -1;
    if (!chromium) {
      mostrar(false, 'este navegador não é compatível. Use o Chrome no computador ou o Kiwi Browser no Android.');
      return;
    }
    if (android) {
      mostrar(true, 'no Android, a extensão exige o Kiwi Browser. Se você já está nele, é só clicar em "Instalar extensão".');
      return;
    }
    mostrar(true, 'seu navegador parece compatível. Clique em "Instalar extensão".');
  }
  botao.addEventListener('click', verificar);
})();
</script>

## Como usar a ferramenta

1. Abra o site no **Chrome** (computador) ou no **Kiwi Browser** (Android).
2. Clique em **Instalar extensão** e adicione a extensão **Anonymous Stories** pela Chrome Web Store.
3. Acesse o seu Instagram normalmente e assista aos stories que quiser. Com a extensão ligada, eles não são marcados como visualizados.
4. Para voltar ao normal, clique no ícone da extensão na barra do navegador e deixe-a **desligada**.

Use o botão **Verificar navegador** se tiver dúvida sobre a compatibilidade. A extensão funciona no seu próprio Instagram, inclusive com stories de contas privadas que você já segue.

## Entendendo os termos

- **Instagram Anônimo:** nome dado a ferramentas que permitem ver conteúdo do Instagram sem deixar rastro da sua visita.
- **Story:** foto ou vídeo que fica disponível por 24 horas no perfil de alguém.
- **Visualização de story:** registro que o Instagram mostra ao autor com os nomes de quem assistiu ao story.
- **Extensão:** pequeno programa instalado no navegador que adiciona recursos a ele.
- **Chrome Web Store:** loja oficial de extensões do Google Chrome.
- **Kiwi Browser:** navegador para Android que aceita extensões do Chrome.
- **Conta privada:** perfil em que só os seguidores aprovados podem ver as publicações e os stories.
- **Ligar e desligar a extensão:** ao clicar no ícone dela, você escolhe se os stories assistidos ficam ocultos ou voltam a ser marcados como vistos.