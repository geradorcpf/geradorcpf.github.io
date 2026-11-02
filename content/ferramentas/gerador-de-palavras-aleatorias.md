---
title: "Gerador de Palavras Aleatórias"
seoTitle: "Gerador de Palavras Aleatórias"
description: "Gerador de Palavras Aleatórias: gere palavras aleatórias para jogos e criação de texto. Grátis e online, sem cadastro."
summary: "Gere palavras aleatórias para jogos e criação de texto."
date: 2026-11-02
draft: false
category: "aleatorio"
tags: ["palavras", "escrita", "gerador"]
keywords: ["gerador de palavras aleatórias", "gerador de palavras aleatórias online", "palavras", "escrita", "gerador"]
---

Escolha o tipo de palavra, defina os filtros que quiser e clique em **Gerar Palavras**.

<div id="gerador-palavras" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🎲 Gerador de Palavras Aleatórias</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Escolha as opções e veja as palavras na hora.</p>
<label for="pal-tipo" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Tipo</label>
<select id="pal-tipo" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<option value="todas">Todas as Palavras</option>
<option value="animais">Animais</option>
<option value="corpo">Corpo Humano</option>
<option value="profissoes">Profissões</option>
<option value="frutas">Frutas</option>
</select>
<label for="pal-quantidade" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Palavras</label>
<input id="pal-quantidade" type="text" inputmode="numeric" placeholder="Ex.: 10" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<label for="pal-letras" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Quantidade de letras</label>
<input id="pal-letras" type="text" inputmode="numeric" placeholder="Ex.: 5 (opcional)" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<label for="pal-inicio" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Começa com</label>
<input id="pal-inicio" type="text" placeholder="Ex.: ca (opcional)" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<label for="pal-fim" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Termina com</label>
<input id="pal-fim" type="text" placeholder="Ex.: o (opcional)" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:20px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="pal-gerar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Gerar Palavras</button>
<button type="button" id="pal-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="pal-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resultado:</strong> <div id="pal-resultado" style="margin-top:6px;">escolha as opções e clique em "Gerar Palavras".</div></div>
</div>
<script>
(function () {
  var BANCO = {
    animais: ['cachorro', 'gato', 'cavalo', 'elefante', 'girafa', 'leão', 'tigre', 'macaco', 'coelho', 'tartaruga', 'golfinho', 'baleia', 'tubarão', 'águia', 'coruja', 'pinguim', 'jacaré', 'cobra', 'borboleta', 'formiga', 'abelha', 'aranha', 'camelo', 'zebra', 'urso', 'lobo', 'raposa', 'onça', 'jabuti', 'papagaio', 'tucano', 'sapo', 'rato', 'vaca', 'porco', 'ovelha', 'cabra', 'galinha', 'pato', 'peixe', 'polvo', 'lagosta', 'caranguejo', 'canguru', 'hipopótamo', 'rinoceronte', 'crocodilo', 'camaleão', 'besouro', 'gavião'],
    corpo: ['cabeça', 'cabelo', 'testa', 'olho', 'nariz', 'boca', 'língua', 'dente', 'orelha', 'pescoço', 'ombro', 'braço', 'cotovelo', 'mão', 'dedo', 'unha', 'peito', 'costela', 'barriga', 'umbigo', 'cintura', 'quadril', 'perna', 'joelho', 'coxa', 'tornozelo', 'pé', 'calcanhar', 'coração', 'pulmão', 'fígado', 'estômago', 'rim', 'cérebro', 'osso', 'músculo', 'pele', 'sangue', 'garganta', 'bochecha', 'sobrancelha', 'cílio', 'queixo', 'punho', 'panturrilha', 'tendão', 'veia', 'nuca'],
    profissoes: ['médico', 'professor', 'engenheiro', 'advogado', 'arquiteto', 'dentista', 'enfermeiro', 'motorista', 'padeiro', 'pedreiro', 'carpinteiro', 'eletricista', 'encanador', 'cozinheiro', 'garçom', 'bombeiro', 'policial', 'piloto', 'jornalista', 'pintor', 'músico', 'cantor', 'ator', 'fotógrafo', 'programador', 'farmacêutico', 'veterinário', 'jardineiro', 'mecânico', 'vendedor', 'cientista', 'bibliotecário', 'costureiro', 'açougueiro', 'barbeiro', 'cabeleireiro', 'juiz', 'soldado', 'escritor', 'tradutor', 'contador', 'psicólogo', 'nutricionista', 'fisioterapeuta', 'agricultor', 'pescador', 'marceneiro', 'secretário', 'atleta', 'designer'],
    frutas: ['maçã', 'banana', 'laranja', 'uva', 'manga', 'abacaxi', 'melancia', 'morango', 'pera', 'pêssego', 'limão', 'mamão', 'goiaba', 'caju', 'acerola', 'abacate', 'kiwi', 'cereja', 'ameixa', 'framboesa', 'amora', 'coco', 'figo', 'melão', 'tangerina', 'maracujá', 'jabuticaba', 'pitanga', 'graviola', 'lichia', 'romã', 'caqui', 'carambola', 'cupuaçu', 'açaí', 'jaca', 'mexerica', 'nectarina', 'tâmara', 'pitaya'],
    geral: ['casa', 'livro', 'mesa', 'cadeira', 'janela', 'porta', 'carro', 'bicicleta', 'estrada', 'cidade', 'montanha', 'rio', 'mar', 'praia', 'floresta', 'jardim', 'flor', 'árvore', 'sol', 'lua', 'estrela', 'nuvem', 'chuva', 'vento', 'fogo', 'terra', 'água', 'amigo', 'família', 'escola', 'trabalho', 'música', 'dança', 'festa', 'viagem', 'aventura', 'segredo', 'sonho', 'tempo', 'caminho', 'ponte', 'castelo', 'tesouro', 'espelho', 'relógio', 'telefone', 'computador', 'caneta', 'papel', 'caderno', 'mochila', 'chave', 'lâmpada', 'cozinha', 'quarto', 'sala', 'banheiro', 'pão', 'queijo', 'café', 'chocolate', 'sorvete', 'bolo', 'feijão', 'arroz', 'mundo', 'ideia', 'palavra', 'história', 'silêncio', 'coragem', 'alegria', 'saudade', 'liberdade', 'verdade', 'esperança', 'amizade', 'lembrança', 'mistério', 'horizonte', 'oceano', 'deserto', 'vulcão', 'cachoeira', 'trovão', 'relâmpago', 'neblina', 'caverna', 'planeta', 'foguete', 'robô', 'dragão', 'fada', 'pirata', 'bruxa', 'cavaleiro', 'tambor', 'violão', 'guitarra', 'piano']
  };
  var tipo = document.getElementById('pal-tipo');
  var quantidade = document.getElementById('pal-quantidade');
  var letras = document.getElementById('pal-letras');
  var inicio = document.getElementById('pal-inicio');
  var fim = document.getElementById('pal-fim');
  var resultado = document.getElementById('pal-resultado');
  var caixa = document.getElementById('pal-resposta');
  var TEXTO_INICIAL = 'escolha as opções e clique em "Gerar Palavras".';
  function semAcento(s) {
    return String(s).toLowerCase().normalize('NFD').replace(/[\u0300-\u036f]/g, '');
  }
  function inteiro(v) {
    var t = String(v).trim();
    if (t === '') { return null; }
    if (!/^\d+$/.test(t)) { return NaN; }
    return Number(t);
  }
  function listaDoTipo(t) {
    if (t !== 'todas') { return BANCO[t].slice(); }
    var vistos = {};
    var todas = [];
    ['geral', 'animais', 'corpo', 'profissoes', 'frutas'].forEach(function (k) {
      BANCO[k].forEach(function (p) {
        if (!vistos[p]) { vistos[p] = true; todas.push(p); }
      });
    });
    return todas;
  }
  function embaralhar(arr) {
    var a = arr.slice();
    var i = a.length;
    while (i) {
      var j = Math.floor(Math.random() * i);
      i = i - 1;
      var tmp = a[i];
      a[i] = a[j];
      a[j] = tmp;
    }
    return a;
  }
  function erro(msg) {
    caixa.style.borderColor = '#fca5a5';
    caixa.style.background = '#fef2f2';
    resultado.style.color = '#b91c1c';
    resultado.textContent = msg;
  }
  function gerar() {
    var n = inteiro(quantidade.value);
    var l = inteiro(letras.value);
    if (n !== null) {
      if (isNaN(n)) { erro('informe um número inteiro válido em "Palavras".'); return; }
      if (n === 0) { erro('a quantidade de palavras deve ser de pelo menos 1.'); return; }
    }
    if (l !== null) {
      if (isNaN(l)) { erro('informe um número inteiro válido em "Quantidade de letras".'); return; }
      if (l === 0) { erro('a quantidade de letras deve ser de pelo menos 1.'); return; }
    }
    if (n === null) { n = 10; }
    n = Math.min(n, 100);
    var ci = semAcento(inicio.value).replace(/\s/g, '');
    var cf = semAcento(fim.value).replace(/\s/g, '');
    var achadas = listaDoTipo(tipo.value).filter(function (p) {
      var s = semAcento(p);
      if (l !== null) { if (s.length !== l) { return false; } }
      if (ci !== '') { if (s.indexOf(ci) !== 0) { return false; } }
      if (cf !== '') { if (s.slice(s.length - cf.length) !== cf) { return false; } }
      return true;
    });
    if (achadas.length === 0) { erro('nenhuma palavra encontrada com esses filtros. Tente mudar as opções.'); return; }
    var sorteadas = embaralhar(achadas).slice(0, n);
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    resultado.textContent = '';
    sorteadas.forEach(function (p) {
      var chip = document.createElement('span');
      chip.textContent = p;
      chip.style.cssText = 'display:inline-block;margin:4px 6px 4px 0;padding:6px 12px;background:#eef2ff;border:1px solid #c7d2fe;border-radius:999px;color:#3730a3;font-weight:600;';
      resultado.appendChild(chip);
    });
    if (sorteadas.length !== n) {
      var aviso = document.createElement('div');
      aviso.style.cssText = 'margin-top:8px;font-size:0.85rem;color:#475569;';
      aviso.textContent = 'Só existem ' + sorteadas.length + ' palavra(s) com esses filtros.';
      resultado.appendChild(aviso);
    }
  }
  function limpar() {
    tipo.value = 'todas';
    quantidade.value = '';
    letras.value = '';
    inicio.value = '';
    fim.value = '';
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    resultado.style.color = '#64748b';
    resultado.textContent = TEXTO_INICIAL;
    quantidade.focus();
  }
  document.getElementById('pal-gerar').addEventListener('click', gerar);
  document.getElementById('pal-limpar').addEventListener('click', limpar);
  [tipo, quantidade, letras, inicio, fim].forEach(function (el) {
    el.addEventListener('focus', function () { el.style.borderColor = '#6366f1'; });
    el.addEventListener('blur', function () { el.style.borderColor = '#c7d2fe'; });
  });
  [quantidade, letras, inicio, fim].forEach(function (el) {
    el.addEventListener('keydown', function (e) { if (e.key === 'Enter') { gerar(); } });
  });
})();
</script>

## Como usar o gerador

1. Escolha o **Tipo** de palavra: todas as palavras, animais, corpo humano, profissões ou frutas.
2. Em **Palavras**, digite quantas palavras você quer gerar (até 100). Se deixar em branco, o gerador mostra 10.
3. Se quiser, informe a **Quantidade de letras** para gerar só palavras com esse tamanho.
4. Se quiser, preencha **Começa com** e/ou **Termina com** para filtrar pelo início e pelo final da palavra.
5. Clique em **Gerar Palavras** (ou pressione Enter) para ver o resultado.
6. Use o botão **Limpar** para voltar às opções iniciais e fazer uma nova geração.

Os filtros podem ser combinados. Por exemplo, tipo **Animais**, 5 letras e começando com **c** mostra apenas animais de cinco letras que começam com essa letra. A busca ignora acentos e letras maiúsculas, então `a` encontra tanto "abelha" quanto "águia". Se existirem menos palavras do que o pedido, o gerador mostra todas as que encontrou e avisa quantas são.

## Entendendo os termos

- **Palavra aleatória:** palavra sorteada ao acaso de uma lista, sem ordem ou padrão definido. Cada clique em Gerar Palavras pode trazer um resultado diferente.
- **Tipo:** categoria da lista usada no sorteio. Pode ser Todas as Palavras, Animais, Corpo Humano, Profissões ou Frutas.
- **Palavras:** campo que define a quantidade de palavras que serão geradas de uma vez.
- **Quantidade de letras:** filtro que limita o resultado a palavras com exatamente esse número de letras. É útil para jogos como Wordle e palavras cruzadas.
- **Começa com:** filtro que mantém apenas as palavras que iniciam com a letra ou o trecho informado.
- **Termina com:** filtro que mantém apenas as palavras que terminam com a letra ou o trecho informado.
- **Resultado:** área onde aparecem as palavras sorteadas, uma ao lado da outra.