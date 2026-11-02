---
title: "Gerador de Nicks"
seoTitle: "Gerador de Nicks"
description: "Gerador de Nicks: gere nicks e apelidos criativos para jogos e redes. Grátis e online, sem cadastro."
summary: "Gere nicks e apelidos criativos para jogos e redes."
date: 2026-11-02
draft: false
category: "aleatorio"
tags: ["nicks", "nomes", "jogos", "gerador"]
keywords: ["gerador de nicks", "gerador de nicks online", "nicks", "nomes", "jogos"]
---

Escolha o método, defina quantos nicks quer e clique em **Gerar Nicks**. Para copiar um nick, basta clicar nele.

<div id="calc-nicks" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🎮 Gerador de Nicks</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Escolha o método e gere nicks criativos na hora.</p>
<label for="nick-metodo" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Método</label>
<select id="nick-metodo" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<option value="nome">A partir do seu nome</option>
<option value="aleatorio">Aleatório</option>
<option value="adjetivo">Nome + Adjetivo</option>
</select>
<label for="nick-quantidade" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Nº de nicks a gerar</label>
<input id="nick-quantidade" type="text" inputmode="numeric" value="10" placeholder="Ex.: 10" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<div id="nick-bloco-letras" style="display:none;">
<label for="nick-letras" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Número de letras</label>
<select id="nick-letras" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<option value="4">4</option>
<option value="5">5</option>
<option value="6" selected>6</option>
<option value="7">7</option>
<option value="8">8</option>
</select>
</div>
<div id="nick-bloco-nome">
<label for="nick-nome" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Nome</label>
<input id="nick-nome" type="text" placeholder="Ex.: Carlos" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<label for="nick-sobrenome" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Sobrenome</label>
<input id="nick-sobrenome" type="text" placeholder="Ex.: Silva" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
</div>
<div style="display:flex;gap:10px;flex-wrap:wrap;margin-top:4px;">
<button type="button" id="nick-gerar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Gerar Nicks</button>
<button type="button" id="nick-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="nick-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="nick-resultado">escolha o método e clique em "Gerar Nicks".</span></div>
</div>
<script>
(function () {
  var metodo = document.getElementById('nick-metodo');
  var quantidade = document.getElementById('nick-quantidade');
  var letras = document.getElementById('nick-letras');
  var nome = document.getElementById('nick-nome');
  var sobrenome = document.getElementById('nick-sobrenome');
  var blocoLetras = document.getElementById('nick-bloco-letras');
  var blocoNome = document.getElementById('nick-bloco-nome');
  var resultado = document.getElementById('nick-resultado');
  var caixa = document.getElementById('nick-resposta');
  var adjetivos = ['Veloz', 'Sombrio', 'Mortal', 'Furioso', 'Lendario', 'Astuto', 'Bravo', 'Feroz', 'Gelado', 'Ardente', 'Noturno', 'Mistico', 'Sagaz', 'Implacavel', 'Selvagem', 'Supremo', 'Silencioso', 'Invicto', 'Fatal', 'Magico', 'Valente', 'Eterno', 'Rebelde', 'Esperto', 'Titan', 'Fantasma', 'Dourado', 'Atomico', 'Cosmico', 'Epico'];
  var palavras = ['Dragao', 'Lobo', 'Falcao', 'Ninja', 'Samurai', 'Tigre', 'Trovao', 'Raio', 'Fenix', 'Guerreiro', 'Cacador', 'Mago', 'Sombra', 'Aguia', 'Fogo', 'Gelo', 'Tempestade', 'Lamina', 'Escudo', 'Pantera', 'Viking', 'Lenda', 'Cometa', 'Furia', 'Rei'];
  var nomes = ['Pedro', 'Lucas', 'Rafael', 'Bruno', 'Thiago', 'Gabriel', 'Diego', 'Mateus', 'Felipe', 'Caio', 'Davi', 'Enzo', 'Leo', 'Artur', 'Nico', 'Igor', 'Hugo', 'Vitor', 'Joao', 'Andre'];
  var consoantes = 'bcdfgjklmnprstvz';
  var vogais = 'aeiou';
  function sorteio(lista) { return lista[Math.floor(Math.random() * lista.length)]; }
  function limparTexto(v) {
    var t = String(v).trim().normalize('NFD').replace(/[\u0300-\u036f]/g, '');
    return t.replace(/[^A-Za-z0-9]/g, '');
  }
  function capitalizar(t) {
    if (t === '') { return ''; }
    return t.charAt(0).toUpperCase() + t.slice(1).toLowerCase();
  }
  function palavraAleatoria(tamanho) {
    var saida = '';
    var usarConsoante = Math.random() > 0.3;
    while (saida.length !== tamanho) {
      saida += usarConsoante ? sorteio(consoantes) : sorteio(vogais);
      usarConsoante = !usarConsoante;
    }
    return capitalizar(saida);
  }
  function nickDoNome(n, s) {
    var w = sorteio(adjetivos);
    var p = sorteio(palavras);
    var opcoes = [
      function () { return n + w; },
      function () { return w + n; },
      function () { return n + '_' + p; },
      function () { return p + n; },
      function () { return s === '' ? n + p : s + w; },
      function () { return s === '' ? w + n : n + s.charAt(0).toUpperCase(); },
      function () { return s === '' ? n + '_' + w : n + s; },
      function () { return n.slice(0, 3) + p; },
      function () { return n + Math.floor(Math.random() * 90 + 10); }
    ];
    return sorteio(opcoes)();
  }
  function nickComAdjetivo() {
    var n = sorteio(nomes);
    var w = sorteio(adjetivos);
    var opcoes = [
      function () { return n + w; },
      function () { return w + n; },
      function () { return n + '_' + w; },
      function () { return w + '_' + n; }
    ];
    return sorteio(opcoes)();
  }
  function atualizarCampos() {
    blocoLetras.style.display = metodo.value === 'aleatorio' ? 'block' : 'none';
    blocoNome.style.display = metodo.value === 'nome' ? 'block' : 'none';
  }
  function erro(msg) {
    caixa.style.borderColor = '#fca5a5';
    caixa.style.background = '#fef2f2';
    resultado.style.color = '#b91c1c';
    resultado.textContent = msg;
  }
  function copiar(texto, botao) {
    var original = botao.textContent;
    function aviso() {
      botao.textContent = 'Copiado!';
      setTimeout(function () { botao.textContent = original; }, 1200);
    }
    if (navigator.clipboard) {
      navigator.clipboard.writeText(texto).then(aviso, function () {});
    } else {
      var area = document.createElement('textarea');
      area.value = texto;
      document.body.appendChild(area);
      area.select();
      try { document.execCommand('copy'); aviso(); } catch (e) {}
      document.body.removeChild(area);
    }
  }
  function gerar() {
    var qtd = parseInt(String(quantidade.value).trim(), 10);
    if (isNaN(qtd) || qtd > 50 || qtd === 0 || qtd !== Math.abs(qtd)) { erro('informe um número de nicks entre 1 e 50.'); return; }
    var n = limparTexto(nome.value);
    var s = limparTexto(sobrenome.value);
    if (metodo.value === 'nome' && n === '') { erro('digite o seu nome para gerar nicks a partir dele.'); return; }
    n = capitalizar(n);
    s = capitalizar(s);
    var lista = [];
    var vistos = {};
    var tentativas = 0;
    while (lista.length !== qtd && tentativas !== 3000) {
      tentativas += 1;
      var nick;
      if (metodo.value === 'aleatorio') { nick = palavraAleatoria(parseInt(letras.value, 10)); }
      else if (metodo.value === 'adjetivo') { nick = nickComAdjetivo(); }
      else { nick = nickDoNome(n, s); }
      if (!vistos[nick]) {
        vistos[nick] = true;
        lista.push(nick);
      }
    }
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    resultado.textContent = '';
    var titulo = document.createElement('div');
    titulo.style.marginBottom = '10px';
    titulo.textContent = lista.length + ' nick(s) gerado(s). Clique para copiar:';
    resultado.appendChild(titulo);
    var grade = document.createElement('div');
    grade.style.cssText = 'display:flex;flex-wrap:wrap;gap:8px;';
    lista.forEach(function (item) {
      var b = document.createElement('button');
      b.type = 'button';
      b.textContent = item;
      b.style.cssText = 'padding:8px 14px;font-size:1rem;font-weight:600;color:#3730a3;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;';
      b.addEventListener('click', function () { copiar(item, b); });
      grade.appendChild(b);
    });
    resultado.appendChild(grade);
  }
  function limpar() {
    nome.value = '';
    sobrenome.value = '';
    quantidade.value = '10';
    letras.value = '6';
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    resultado.style.color = '#64748b';
    resultado.textContent = 'escolha o método e clique em "Gerar Nicks".';
  }
  document.getElementById('nick-gerar').addEventListener('click', gerar);
  document.getElementById('nick-limpar').addEventListener('click', limpar);
  metodo.addEventListener('change', atualizarCampos);
  [quantidade, nome, sobrenome, metodo, letras].forEach(function (el) {
    el.addEventListener('focus', function () { el.style.borderColor = '#6366f1'; });
    el.addEventListener('blur', function () { el.style.borderColor = '#c7d2fe'; });
  });
  [quantidade, nome, sobrenome].forEach(function (el) {
    el.addEventListener('keydown', function (e) { if (e.key === 'Enter') { gerar(); } });
  });
  atualizarCampos();
})();
</script>

## Como usar o gerador

1. Escolha o **Método** de geração: a partir do seu nome, aleatório ou nome + adjetivo.
2. Informe o **Nº de nicks a gerar** (de 1 a 50).
3. Se escolheu o método **Aleatório**, selecione o **Número de letras** do nick (de 4 a 8).
4. Se escolheu o método **A partir do seu nome**, digite seu **Nome** e, se quiser, o **Sobrenome**.
5. Clique em **Gerar Nicks** (ou pressione Enter) para ver a lista de nicks.
6. Clique em qualquer nick da lista para copiá-lo e use o botão **Limpar** para recomeçar.

Você pode clicar em **Gerar Nicks** quantas vezes quiser: a cada clique saem novas combinações. Acentos e espaços são removidos automaticamente, pois a maioria dos jogos e redes não aceita esses caracteres.

## Entendendo os termos

- **Nick:** apelido usado no lugar do nome real em jogos, redes sociais e fóruns. Também é chamado de nickname.
- **Gamertag:** nome de usuário de um jogador, usado para identificá-lo nos jogos online e nas plataformas de games.
- **Método:** forma como os nicks são criados: a partir do seu nome, de letras aleatórias ou de um nome combinado com um adjetivo.
- **A partir do seu nome:** método que mistura o seu nome e o seu sobrenome com palavras, adjetivos e números.
- **Aleatório:** método que cria palavras pronunciáveis, sem significado, com o número de letras escolhido.
- **Nome + Adjetivo:** método que une um nome a um adjetivo, como em "PedroVeloz" ou "Sombrio_Lucas".
- **Nº de nicks a gerar:** quantidade de sugestões exibidas de uma só vez.
- **Número de letras:** tamanho do nick no método aleatório. Nicks curtos são mais fáceis de lembrar e de digitar.
- **Nome e Sobrenome:** dados usados como base no método "A partir do seu nome". O sobrenome é opcional.
- **Adjetivo:** palavra que dá uma característica ao nome, como veloz, sombrio ou lendário.