---
title: "Quem Deixou de me Seguir?"
seoTitle: "Quem Deixou de me Seguir?"
description: "Quem Deixou de me Seguir?: descubra quem deixou de seguir você no Instagram. Grátis e online, sem cadastro."
summary: "Descubra quem deixou de seguir você no Instagram."
date: 2026-11-07
draft: false
category: "social"
tags: ["instagram", "seguidores", "redes sociais"]
keywords: ["quem deixou de me seguir?", "quem deixou de me seguir? online", "instagram", "seguidores", "redes sociais"]
---

Cole abaixo a lista de seguidores de duas datas diferentes e depois clique em **Comparar Listas**.

<div id="calc-quem-deixou" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">👥 Quem Deixou de me Seguir?</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Compare duas listas de seguidores e veja as diferenças na hora.</p>
<label for="qdms-anterior" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Lista Anterior (data mais antiga)</label>
<textarea id="qdms-anterior" placeholder="Ex.: ana_silva, joao.souza, @maria_oliveira" autocomplete="off" spellcheck="false" style="width:100%;min-height:120px;padding:12px 14px;margin-bottom:16px;font-size:1rem;font-family:inherit;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;resize:vertical;"></textarea>
<label for="qdms-atual" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Lista Atual (data mais recente)</label>
<textarea id="qdms-atual" placeholder="Ex.: ana_silva, @maria_oliveira, carlos.lima" autocomplete="off" spellcheck="false" style="width:100%;min-height:120px;padding:12px 14px;margin-bottom:20px;font-size:1rem;font-family:inherit;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;resize:vertical;"></textarea>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="qdms-comparar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Comparar Listas</button>
<button type="button" id="qdms-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="qdms-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="qdms-resultado">cole as duas listas e clique em "Comparar Listas".</span></div>
</div>
<script>
(function () {
  var anterior = document.getElementById('qdms-anterior');
  var atual = document.getElementById('qdms-atual');
  var resultado = document.getElementById('qdms-resultado');
  var caixa = document.getElementById('qdms-resposta');
  var LIMITE = 10000;
  var MSG_INICIAL = 'cole as duas listas e clique em "Comparar Listas".';
  function extrair(texto) {
    var partes = String(texto).split(/[\s,;]+/);
    var vistos = {};
    var lista = [];
    partes.forEach(function (p) {
      var u = p.trim();
      if (u === '') { return; }
      u = u.replace(/^https?:\/\/(www\.)?instagram\.com\//i, '');
      u = u.split(/[\/?#]/)[0];
      u = u.replace(/^@/, '').toLowerCase();
      if (!/^[a-z0-9._]{1,30}$/.test(u)) { return; }
      if (vistos['u_' + u] !== true) {
        vistos['u_' + u] = true;
        lista.push(u);
      }
    });
    return lista;
  }
  function fmt(n) { return n.toLocaleString('pt-BR'); }
  function estilo(borda, fundo, cor) {
    caixa.style.borderColor = borda;
    caixa.style.background = fundo;
    resultado.style.color = cor;
  }
  function esvaziar() {
    while (resultado.firstChild) { resultado.removeChild(resultado.firstChild); }
  }
  function erro(msg) {
    estilo('#fca5a5', '#fef2f2', '#b91c1c');
    esvaziar();
    resultado.textContent = msg;
  }
  function diferenca(a, b) {
    var mapa = {};
    b.forEach(function (u) { mapa['u_' + u] = true; });
    return a.filter(function (u) { return mapa['u_' + u] !== true; });
  }
  function bloco(titulo, itens, corTitulo) {
    var secao = document.createElement('div');
    secao.style.marginTop = '14px';
    var h = document.createElement('div');
    h.style.fontWeight = '700';
    h.style.color = corTitulo;
    h.style.marginBottom = '8px';
    h.textContent = titulo + ' (' + fmt(itens.length) + ')';
    secao.appendChild(h);
    if (itens.length === 0) {
      var vazio = document.createElement('div');
      vazio.style.fontSize = '0.9rem';
      vazio.style.color = '#475569';
      vazio.textContent = 'Nenhum usuário.';
      secao.appendChild(vazio);
      return secao;
    }
    var grade = document.createElement('div');
    grade.style.cssText = 'display:flex;flex-wrap:wrap;gap:6px;max-height:240px;overflow:auto;';
    itens.forEach(function (u) {
      var a = document.createElement('a');
      a.href = 'https://www.instagram.com/' + u + '/';
      a.target = '_blank';
      a.rel = 'noopener noreferrer';
      a.textContent = '@' + u;
      a.style.cssText = 'padding:4px 10px;font-size:0.9rem;color:#3730a3;background:#eef2ff;border:1px solid #c7d2fe;border-radius:999px;text-decoration:none;';
      grade.appendChild(a);
    });
    secao.appendChild(grade);
    return secao;
  }
  function comparar() {
    var antes = extrair(anterior.value);
    var depois = extrair(atual.value);
    if (antes.length === 0 || depois.length === 0) {
      erro('cole usuários válidos nas duas listas.');
      return;
    }
    if (antes.length > LIMITE || depois.length > LIMITE) {
      erro('cada lista pode ter no máximo ' + fmt(LIMITE) + ' usuários.');
      return;
    }
    var saiu = diferenca(antes, depois);
    var novos = diferenca(depois, antes);
    estilo('#86efac', '#f0fdf4', '#166534');
    esvaziar();
    var resumo = document.createElement('div');
    var forte = document.createElement('strong');
    forte.style.fontSize = '1.2rem';
    forte.textContent = fmt(saiu.length);
    resumo.appendChild(forte);
    resumo.appendChild(document.createTextNode(saiu.length === 1 ? ' pessoa deixou de seguir você' : ' pessoas deixaram de seguir você'));
    resultado.appendChild(resumo);
    var info = document.createElement('div');
    info.style.fontSize = '0.85rem';
    info.style.color = '#475569';
    info.textContent = 'Lista anterior: ' + fmt(antes.length) + ' | Lista atual: ' + fmt(depois.length);
    resultado.appendChild(info);
    resultado.appendChild(bloco('Deixaram de seguir', saiu, '#b91c1c'));
    resultado.appendChild(bloco('Novos seguidores', novos, '#166534'));
  }
  function limpar() {
    anterior.value = '';
    atual.value = '';
    estilo('#c7d2fe', '#ffffff', '#64748b');
    esvaziar();
    resultado.textContent = MSG_INICIAL;
    anterior.focus();
  }
  document.getElementById('qdms-comparar').addEventListener('click', comparar);
  document.getElementById('qdms-limpar').addEventListener('click', limpar);
  [anterior, atual].forEach(function (el) {
    el.addEventListener('focus', function () { el.style.borderColor = '#6366f1'; });
    el.addEventListener('blur', function () { el.style.borderColor = '#c7d2fe'; });
  });
})();
</script>

## Como usar a ferramenta

1. Reúna a lista de seguidores do seu perfil do Instagram em uma data anterior e cole os nomes de usuário no campo **Lista Anterior**.
2. Reúna a lista de seguidores atual, de uma data mais recente, e cole no campo **Lista Atual**.
3. Clique em **Comparar Listas** para ver quem estava na lista anterior e não está mais na atual.
4. Clique no nome de um usuário no resultado para abrir o perfil dele no Instagram.
5. Use o botão **Limpar** para apagar as duas listas e fazer uma nova comparação.

Os nomes podem ser separados por espaço, vírgula, ponto e vírgula ou quebra de linha. Você pode colar com ou sem o símbolo @, e links de perfil como `instagram.com/usuario` também são aceitos. Letras maiúsculas e minúsculas são tratadas como iguais, e nomes repetidos são contados uma única vez. Cada lista pode ter até 10.000 usuários.

Para comparar de forma correta, as duas listas devem ser do mesmo perfil e de dias diferentes. Quanto maior o intervalo entre elas, mais mudanças tendem a aparecer. Todo o processamento acontece no seu navegador, e nenhuma lista é enviada ou salva em servidores.

## Entendendo os termos

- **Seguidor:** conta que acompanha as publicações do seu perfil no Instagram.
- **Deixar de seguir:** ação de parar de seguir um perfil. Nesta ferramenta, é quem aparece na lista anterior, mas não na atual.
- **Novo seguidor:** conta que aparece na lista atual, mas não estava na lista anterior.
- **Nome de usuário:** identificador único de uma conta no Instagram, o texto que vem depois do @. Pode ter letras, números, pontos e sublinhados, com até 30 caracteres.
- **Lista Anterior:** lista de seguidores de uma data mais antiga, usada como ponto de partida da comparação.
- **Lista Atual:** lista de seguidores de uma data mais recente, usada para identificar as mudanças.
- **Comparação:** verificação das diferenças entre as duas listas, mostrando quem saiu e quem entrou.