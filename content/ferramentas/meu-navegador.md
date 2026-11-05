---
title: "Meu Navegador"
seoTitle: "Meu Navegador"
description: "Meu Navegador: descubra qual navegador e versão você está usando. Grátis e online, sem cadastro."
summary: "Descubra qual navegador e versão você está usando."
date: 2026-11-05
draft: false
category: "rede"
tags: ["navegador", "diagnóstico", "rede"]
keywords: ["meu navegador", "meu navegador online", "navegador", "diagnóstico", "rede"]
---

Abra esta página e o resultado aparece automaticamente logo abaixo. Se quiser, use o botão **Copiar Resultado** para compartilhar as informações.

<div id="nav-ferramenta" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🌐 Meu Navegador</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Veja qual navegador e versão você está usando agora.</p>
<div style="margin-bottom:12px;padding:14px 16px;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;box-sizing:border-box;">
<div style="font-weight:600;font-size:0.95rem;color:#64748b;margin-bottom:4px;">Navegador</div>
<div id="nav-nome" style="font-size:1.15rem;font-weight:700;color:#3730a3;">Detectando...</div>
</div>
<div style="margin-bottom:12px;padding:14px 16px;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;box-sizing:border-box;">
<div style="font-weight:600;font-size:0.95rem;color:#64748b;margin-bottom:4px;">Versão</div>
<div id="nav-versao" style="font-size:1.15rem;font-weight:700;color:#3730a3;">Detectando...</div>
</div>
<div style="margin-bottom:20px;padding:14px 16px;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;box-sizing:border-box;">
<div style="font-weight:600;font-size:0.95rem;color:#64748b;margin-bottom:4px;">User Agent</div>
<div id="nav-ua" style="font-size:0.85rem;color:#475569;word-break:break-all;line-height:1.5;">Detectando...</div>
</div>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="nav-copiar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Copiar Resultado</button>
<button type="button" id="nav-atualizar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Atualizar</button>
</div>
<div id="nav-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="nav-resultado">detectando o seu navegador...</span></div>
</div>
<script>
(function () {
  var ua = navigator.userAgent || '';
  var elNome = document.getElementById('nav-nome');
  var elVersao = document.getElementById('nav-versao');
  var elUa = document.getElementById('nav-ua');
  var caixa = document.getElementById('nav-resposta');
  var resultado = document.getElementById('nav-resultado');
  var atual = { nome: 'Desconhecido', versao: 'Não identificada' };
  function pegar(re) {
    var m = ua.match(re);
    return m ? m[1] : '';
  }
  function mostrar() {
    elNome.textContent = atual.nome;
    elVersao.textContent = atual.versao;
    elUa.textContent = ua;
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    resultado.innerHTML = 'Você está usando o <strong style="font-size:1.2rem;">' + atual.nome + '</strong> na versão <strong style="font-size:1.2rem;">' + atual.versao + '</strong>.';
  }
  function detectar() {
    var nome = 'Desconhecido';
    var versao = '';
    if (/Edg(?:e|A|iOS)?\//.test(ua)) {
      nome = 'Microsoft Edge';
      versao = pegar(/Edg(?:e|A|iOS)?\/([\d.]+)/);
    } else if (/OPR\/|OPiOS\/|Opera/.test(ua)) {
      nome = 'Opera';
      versao = pegar(/(?:OPR|OPiOS)\/([\d.]+)/) || pegar(/Version\/([\d.]+)/);
    } else if (/SamsungBrowser\//.test(ua)) {
      nome = 'Samsung Internet';
      versao = pegar(/SamsungBrowser\/([\d.]+)/);
    } else if (/Vivaldi\//.test(ua)) {
      nome = 'Vivaldi';
      versao = pegar(/Vivaldi\/([\d.]+)/);
    } else if (/Firefox\/|FxiOS\//.test(ua)) {
      nome = 'Mozilla Firefox';
      versao = pegar(/(?:Firefox|FxiOS)\/([\d.]+)/);
    } else if (/Chrome\/|CriOS\//.test(ua)) {
      nome = 'Google Chrome';
      versao = pegar(/(?:Chrome|CriOS)\/([\d.]+)/);
    } else if (/Safari\//.test(ua)) {
      nome = 'Safari';
      versao = pegar(/Version\/([\d.]+)/);
    } else if (/MSIE |Trident\//.test(ua)) {
      nome = 'Internet Explorer';
      versao = pegar(/MSIE ([\d.]+)/) || pegar(/rv:([\d.]+)/);
    }
    atual = { nome: nome, versao: versao || 'Não identificada' };
    mostrar();
    try {
      if (nome === 'Google Chrome') {
        if (navigator.brave) {
          if (typeof navigator.brave.isBrave === 'function') {
            navigator.brave.isBrave().then(function (ehBrave) {
              if (ehBrave) {
                atual.nome = 'Brave';
                mostrar();
              }
            }).catch(function () {});
          }
        }
      }
    } catch (e) {}
  }
  function copiar() {
    var texto = 'Navegador: ' + atual.nome + '\nVersão: ' + atual.versao + '\nUser Agent: ' + ua;
    var btn = document.getElementById('nav-copiar');
    function aviso(msg) {
      btn.textContent = msg;
      setTimeout(function () { btn.textContent = 'Copiar Resultado'; }, 1800);
    }
    try {
      if (navigator.clipboard) {
        navigator.clipboard.writeText(texto).then(function () { aviso('Copiado!'); }).catch(function () { aviso('Não foi possível copiar'); });
      } else {
        aviso('Não foi possível copiar');
      }
    } catch (e) {
      aviso('Não foi possível copiar');
    }
  }
  document.getElementById('nav-copiar').addEventListener('click', copiar);
  document.getElementById('nav-atualizar').addEventListener('click', detectar);
  detectar();
})();
</script>

## Como usar a ferramenta

1. Acesse esta página no navegador que você quer identificar.
2. Veja nos campos **Navegador** e **Versão** o resultado, que aparece sozinho assim que a página carrega.
3. Confira o **User Agent** completo, se precisar de mais detalhes técnicos.
4. Clique em **Copiar Resultado** para levar as informações para um e-mail, chamado de suporte ou conversa com um desenvolvedor.
5. Use o botão **Atualizar** para repetir a detecção.

Para saber a informação de outro navegador, abra esta mesma página nele. A ferramenta sempre mostra os dados do navegador que está aberto no momento.

## Entendendo os termos

- **Navegador (browser):** programa usado para acessar sites na internet, como Chrome, Firefox, Edge, Safari e Opera.
- **Versão:** número que identifica a edição do navegador instalada, por exemplo 130.0.6723. Versões mais novas trazem recursos e correções de segurança.
- **User Agent:** texto que o navegador envia aos sites para se identificar, com nome, versão e sistema operacional. É a base da detecção feita por esta ferramenta.
- **Sistema operacional:** programa que controla o dispositivo, como Windows, macOS, Linux, Android e iOS.
- **Motor de renderização:** parte do navegador que desenha as páginas na tela, como Blink (Chrome, Edge), Gecko (Firefox) e WebKit (Safari).
- **Navegador desatualizado:** versão antiga que pode ter falhas de segurança e não exibir sites modernos corretamente.

## Por que saber o navegador e a versão?

Essas informações ajudam a diagnosticar problemas de um site que não carrega direito, a abrir chamados de suporte com mais precisão e a conferir se o navegador está atualizado. Desenvolvedores também usam esses dados para testar a compatibilidade de páginas e sistemas.