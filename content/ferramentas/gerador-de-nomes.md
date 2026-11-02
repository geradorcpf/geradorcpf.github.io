---
title: "Gerador de Nomes"
seoTitle: "Gerador de Nomes"
description: "Gerador de Nomes: gere nomes e sobrenomes brasileiros aleatórios. Grátis e online, sem cadastro."
summary: "Gere nomes e sobrenomes brasileiros aleatórios."
date: 2026-11-02
draft: false
category: "aleatorio"
tags: ["nomes", "pessoas", "gerador", "dados de teste"]
keywords: ["gerador de nomes", "gerador de nomes online", "nomes", "pessoas", "gerador"]
---

Basta escolher a raça, o gênero e a quantidade abaixo e depois clicar em **Gerar Nomes**.

<div id="calc-gerador-nomes" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🎲 Gerador de Nomes</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Escolha as opções e gere nomes na hora.</p>
<label for="ger-raca" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Raça</label>
<select id="ger-raca" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<option value="aleatorio">Aleatório</option>
<option value="humano">Humano</option>
<option value="elfo">Elfo</option>
<option value="anao">Anão</option>
<option value="orc">Orc</option>
<option value="dragao">Dragão</option>
</select>
<label for="ger-genero" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Gênero</label>
<select id="ger-genero" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<option value="m">Masculino</option>
<option value="f">Feminino</option>
</select>
<label for="ger-quantidade" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Quantidade (1 a 50)</label>
<input id="ger-quantidade" type="text" inputmode="numeric" placeholder="Ex.: 10" value="10" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:20px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="ger-gerar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Gerar Nomes</button>
<button type="button" id="ger-copiar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Copiar Todos</button>
<button type="button" id="ger-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="ger-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="ger-resultado">escolha as opções e clique em "Gerar Nomes".</span></div>
</div>
<script>
(function () {
  var selRaca = document.getElementById('ger-raca');
  var selGenero = document.getElementById('ger-genero');
  var inpQtd = document.getElementById('ger-quantidade');
  var resultado = document.getElementById('ger-resultado');
  var caixa = document.getElementById('ger-resposta');
  var atual = [];
  var MSG_INICIAL = 'escolha as opções e clique em "Gerar Nomes".';
  var RACAS = ['humano', 'elfo', 'anao', 'orc', 'dragao'];
  var HUM_M = ['João', 'Pedro', 'Lucas', 'Gabriel', 'Mateus', 'Rafael', 'Carlos', 'Rodrigo', 'Felipe', 'Bruno', 'Thiago', 'Gustavo', 'Eduardo', 'Henrique', 'Fernando', 'André', 'Marcelo', 'Daniel', 'Leonardo', 'Ricardo'];
  var HUM_F = ['Maria', 'Ana', 'Juliana', 'Camila', 'Fernanda', 'Beatriz', 'Larissa', 'Patrícia', 'Aline', 'Mariana', 'Letícia', 'Carolina', 'Amanda', 'Renata', 'Bianca', 'Gabriela', 'Luana', 'Vanessa', 'Isabela', 'Priscila'];
  var HUM_S = ['Silva', 'Santos', 'Oliveira', 'Souza', 'Pereira', 'Costa', 'Rodrigues', 'Almeida', 'Nascimento', 'Lima', 'Araújo', 'Fernandes', 'Carvalho', 'Gomes', 'Martins', 'Rocha', 'Ribeiro', 'Alves', 'Monteiro', 'Barbosa'];
  var ELF_PM = ['aeg', 'bara', 'beleg', 'celeb', 'el', 'fela', 'gal'];
  var ELF_SM = ['bor', 'las', 'randir', 'rod', 'thalion', 'thir', 'uil'];
  var ELF_PF = ['fan', 'galadh', 'gil', 'mel', 'mor', 'sael'];
  var ELF_SF = ['anor', 'dis', 'el', 'uilos'];
  var ANA_P = ['g', 'k', 'l', 't', 'dw', 'thr'];
  var ANA_S = ['ori', 'óin', 'íli', 'alin', 'orin', 'osi', 'imli', 'ormur'];
  var ANA_C = ['Martelo de Ferro', 'Barba de Pedra', 'Punho de Aço', 'Forjador', 'Mineiro', 'Escudo de Carvalho', 'Machado de Prata', 'Filho da Montanha', 'Ferreiro', 'Cavador de Ouro'];
  var ORC_S = ['Gor', 'Mog', 'Thrak', 'Urz', 'Krag', 'Dur', 'Bol', 'Zug', 'Rak', 'Naz', 'Gul', 'Varg'];
  var ORC_T = ['bolg', 'mush', 'thak', 'nash', 'zul', 'krim', 'dagh', 'rukh'];
  var DRA_P = ['Vyr', 'Thar', 'Zy', 'Ignar', 'Kael', 'Draz', 'Sar', 'Mor', 'Aur', 'Ny'];
  var DRA_SM = ['ax', 'ion', 'rath', 'ynth', 'oth', 'akar', 'us'];
  var DRA_SF = ['ia', 'yra', 'ithra', 'ael', 'essa', 'una', 'ira'];
  var DRA_E = ['Sopro de Fogo', 'Asa de Sombra', 'Escama Rubra', 'Garra de Gelo', 'Coração de Brasa', 'Olhar de Tempestade', 'Guardião do Tesouro', 'Senhor das Cinzas'];
  function pick(lista) { return lista[Math.floor(Math.random() * lista.length)]; }
  function cap(t) { return t.charAt(0).toUpperCase() + t.slice(1); }
  function humano(f) {
    var s1 = pick(HUM_S);
    var s2 = pick(HUM_S);
    while (s2 === s1) { s2 = pick(HUM_S); }
    return pick(f ? HUM_F : HUM_M) + ' ' + s1 + ' ' + s2;
  }
  function elfoNome(f) {
    return f ? cap(pick(ELF_PF) + pick(ELF_SF)) : cap(pick(ELF_PM) + pick(ELF_SM));
  }
  function elfo(f) { return elfoNome(f) + ' ' + elfoNome(f); }
  function anao() { return cap(pick(ANA_P) + pick(ANA_S)) + ' ' + pick(ANA_C); }
  function orc(f) {
    var nome = pick(ORC_S) + pick(['osh', 'om']) + (f ? 'a' : '');
    return nome + ' ' + cap((f ? 'gra' : 'gro') + pick(ORC_T));
  }
  function dragao(f) { return cap(pick(DRA_P) + pick(f ? DRA_SF : DRA_SM)) + ' ' + pick(DRA_E); }
  function gerarUm(raca, f) {
    if (raca === 'aleatorio') { raca = pick(RACAS); }
    if (raca === 'humano') { return humano(f); }
    if (raca === 'elfo') { return elfo(f); }
    if (raca === 'anao') { return anao(); }
    if (raca === 'orc') { return orc(f); }
    return dragao(f);
  }
  function fallback(texto) {
    var ta = document.createElement('textarea');
    ta.value = texto;
    ta.style.position = 'fixed';
    ta.style.opacity = '0';
    document.body.appendChild(ta);
    ta.select();
    try { document.execCommand('copy'); } catch (e) {}
    document.body.removeChild(ta);
  }
  function aviso(msg) {
    var el = document.getElementById('ger-aviso');
    if (el) { el.textContent = msg; }
  }
  function copiar(texto, msg) {
    if (navigator.clipboard && navigator.clipboard.writeText) {
      navigator.clipboard.writeText(texto).then(function () { aviso(msg); }, function () { fallback(texto); aviso(msg); });
    } else {
      fallback(texto);
      aviso(msg);
    }
  }
  function erro(msg) {
    atual = [];
    caixa.style.borderColor = '#fca5a5';
    caixa.style.background = '#fef2f2';
    resultado.style.display = 'inline';
    resultado.style.color = '#b91c1c';
    resultado.textContent = msg;
  }
  function mostrar(lista) {
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.display = 'block';
    resultado.style.color = '#166534';
    resultado.textContent = '';
    var dica = document.createElement('div');
    dica.style.cssText = 'margin:4px 0 10px;font-size:0.9rem;color:#475569;';
    dica.textContent = lista.length + ' nome(s) gerado(s). Clique em um nome para copiar.';
    resultado.appendChild(dica);
    var grade = document.createElement('div');
    grade.style.cssText = 'display:flex;flex-wrap:wrap;gap:8px;';
    lista.forEach(function (nome) {
      var b = document.createElement('button');
      b.type = 'button';
      b.textContent = nome;
      b.title = 'Clique para copiar';
      b.style.cssText = 'padding:8px 12px;font-size:0.95rem;font-weight:600;color:#166534;background:#ffffff;border:2px solid #86efac;border-radius:10px;cursor:pointer;';
      b.addEventListener('click', function () { copiar(nome, 'Copiado: ' + nome); });
      grade.appendChild(b);
    });
    resultado.appendChild(grade);
    var av = document.createElement('div');
    av.id = 'ger-aviso';
    av.style.cssText = 'margin-top:10px;font-size:0.9rem;font-weight:600;color:#166534;';
    resultado.appendChild(av);
  }
  function gerar() {
    var t = String(inpQtd.value).trim();
    var q = Number(t);
    if (t === '' || isNaN(q) || q % 1 !== 0) { erro('informe uma quantidade válida (número inteiro).'); return; }
    if (q === 0 || q > 50 || q !== Math.abs(q)) { erro('a quantidade deve ficar entre 1 e 50.'); return; }
    var f = selGenero.value === 'f';
    var lista = [];
    var tentativas = 0;
    while (lista.length !== q && tentativas !== 2000) {
      var n = gerarUm(selRaca.value, f);
      if (lista.indexOf(n) === -1) { lista.push(n); }
      tentativas++;
    }
    atual = lista;
    mostrar(lista);
  }
  function copiarTodos() {
    if (atual.length === 0) { erro('gere os nomes primeiro para poder copiá-los.'); return; }
    copiar(atual.join('\n'), 'Todos os nomes foram copiados.');
  }
  function limpar() {
    atual = [];
    selRaca.value = 'aleatorio';
    selGenero.value = 'm';
    inpQtd.value = '10';
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    resultado.style.display = 'inline';
    resultado.style.color = '#64748b';
    resultado.textContent = MSG_INICIAL;
    selRaca.focus();
  }
  document.getElementById('ger-gerar').addEventListener('click', gerar);
  document.getElementById('ger-copiar').addEventListener('click', copiarTodos);
  document.getElementById('ger-limpar').addEventListener('click', limpar);
  inpQtd.addEventListener('keydown', function (e) { if (e.key === 'Enter') { gerar(); } });
  [selRaca, selGenero, inpQtd].forEach(function (el) {
    el.addEventListener('focus', function () { el.style.borderColor = '#6366f1'; });
    el.addEventListener('blur', function () { el.style.borderColor = '#c7d2fe'; });
  });
})();
</script>

## Como usar a calculadora

1. Escolha a **Raça** do nome no primeiro campo (ou deixe em **Aleatório** para misturar todas).
2. Escolha o **Gênero**: Masculino ou Feminino.
3. Digite a **Quantidade** de nomes que deseja gerar (de 1 a 50).
4. Clique em **Gerar Nomes** (ou pressione Enter no campo de quantidade) para ver o resultado.
5. Clique sobre um nome para copiá-lo, ou use **Copiar Todos** para copiar a lista inteira.
6. Use o botão **Limpar** para voltar às opções iniciais e fazer uma nova geração.

Cada clique em **Gerar Nomes** cria uma nova lista, e os nomes de uma mesma lista não se repetem.

## Entendendo os termos

- **Nome:** palavra que identifica a pessoa ou o personagem, também chamada de primeiro nome ou nome próprio.
- **Sobrenome:** parte do nome que indica a família, o clã, a tribo ou uma característica. Nos humanos são dois sobrenomes brasileiros; nas outras raças funciona como apelido ou título.
- **Raça:** tipo de pessoa ou criatura para o qual o nome é gerado, o que muda o estilo e a sonoridade do resultado.
- **Aleatório:** sorteia uma raça diferente para cada nome gerado.
- **Humano:** nomes e sobrenomes brasileiros comuns, úteis também como dados de teste.
- **Elfo:** nomes elegantes formados pela união de um prefixo e um sufixo, como em histórias de fantasia.
- **Anão:** nomes curtos de sonoridade nórdica, seguidos de um clã ou profissão como sobrenome.
- **Orc:** nomes fortes e curtos, com terminações como -osh e -om, e sobrenome que indica a tribo.
- **Dragão:** nomes imponentes de sonoridade rústica, acompanhados de um título como Asa de Sombra.
- **Gênero:** define se o nome terá forma masculina ou feminina. Nos anões, o nome é o mesmo para os dois gêneros.
- **Quantidade:** número de nomes que serão gerados de uma só vez.
- **Prefixo e sufixo:** pedaços de palavra colocados no início e no fim para formar um nome novo.
- **Nome de fantasia:** nome inventado para personagens de jogos, histórias e RPG, ou para usar como apelido.
- **Copiar:** envia o nome clicado, ou a lista inteira, para a área de transferência, pronto para colar em outro lugar.