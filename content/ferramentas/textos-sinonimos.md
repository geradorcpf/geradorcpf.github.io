---
title: "Textos Sinônimos"
seoTitle: "Textos Sinônimos"
description: "Textos Sinônimos: encontre sinônimos para variar as palavras do texto. Grátis e online, sem cadastro."
summary: "Encontre sinônimos para variar as palavras do texto."
date: 2026-11-12
draft: false
category: "texto"
tags: ["sinônimos", "escrita", "texto"]
keywords: ["textos sinônimos", "textos sinônimos online", "sinônimos", "escrita", "texto"]
---
<!--INI SUDAH DIKERJAKAN-->

Cole o seu texto abaixo, clique em **Gerar Sinônimos** e depois clique nas palavras sublinhadas para trocá-las.

<div id="calc-sinonimos" style="max-width:640px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">✍️ Textos Sinônimos</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Troque palavras do texto por sinônimos e varie o vocabulário.</p>
<label for="sin-entrada" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Texto original</label>
<textarea id="sin-entrada" rows="4" placeholder="Digite ou cole o seu texto aqui" autocomplete="off" spellcheck="false" style="width:100%;min-height:110px;padding:12px 14px;margin-bottom:16px;font-size:1rem;font-family:inherit;line-height:1.5;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;resize:vertical;"></textarea>
<div style="display:flex;gap:10px;flex-wrap:wrap;margin-bottom:20px;">
<button type="button" id="sin-gerar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Gerar Sinônimos</button>
<button type="button" id="sin-copiar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Copiar texto</button>
<button type="button" id="sin-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<label for="sin-saida" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Texto com sinônimos</label>
<div id="sin-area-saida" style="position:relative;">
<div id="sin-saida" contenteditable="true" spellcheck="false" role="textbox" aria-multiline="true" aria-live="polite" style="min-height:72px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#1e293b;font-size:1rem;line-height:1.8;box-sizing:border-box;outline:none;white-space:pre-wrap;word-wrap:break-word;"></div>
<div id="sin-menu" role="listbox" style="display:none;position:absolute;z-index:10;min-width:170px;max-width:260px;max-height:240px;overflow:auto;padding:6px;background:#ffffff;border:2px solid #c7d2fe;border-radius:12px;box-shadow:0 8px 24px rgba(79,70,229,0.18);box-sizing:border-box;"></div>
</div>
<p id="sin-status" aria-live="polite" style="margin:12px 0 0;font-size:0.9rem;line-height:1.5;color:#64748b;">Cole um texto e clique em "Gerar Sinônimos".</p>
</div>
<script>
(function () {
  var D = {
    'simplicidade': ['singeleza', 'naturalidade', 'modéstia', 'sobriedade'],
    'sofisticação': ['refinamento', 'requinte', 'elegância', 'apuro'],
    'máximo': ['supremo', 'extremo', 'superior', 'culminante'],
    'mínimo': ['reduzido', 'ínfimo', 'diminuto', 'irrisório'],
    'bonito': ['belo', 'lindo', 'formoso', 'atraente'],
    'belo': ['bonito', 'lindo', 'formoso', 'elegante'],
    'lindo': ['belo', 'encantador', 'deslumbrante', 'maravilhoso'],
    'grande': ['enorme', 'amplo', 'imenso', 'vasto'],
    'pequeno': ['reduzido', 'diminuto', 'compacto', 'miúdo'],
    'importante': ['relevante', 'essencial', 'fundamental', 'significativo'],
    'bom': ['ótimo', 'excelente', 'agradável', 'positivo'],
    'ruim': ['mau', 'péssimo', 'desfavorável', 'inadequado'],
    'rápido': ['veloz', 'ligeiro', 'célere', 'acelerado'],
    'lento': ['vagaroso', 'demorado', 'pausado', 'moroso'],
    'fácil': ['simples', 'descomplicado', 'acessível', 'tranquilo'],
    'difícil': ['complicado', 'árduo', 'complexo', 'penoso'],
    'feliz': ['contente', 'alegre', 'satisfeito', 'radiante'],
    'triste': ['abatido', 'melancólico', 'desanimado', 'infeliz'],
    'forte': ['robusto', 'resistente', 'poderoso', 'firme'],
    'fraco': ['débil', 'delicado', 'enfraquecido', 'vulnerável'],
    'inteligente': ['esperto', 'perspicaz', 'sagaz', 'astuto'],
    'claro': ['nítido', 'evidente', 'límpido', 'transparente'],
    'escuro': ['sombrio', 'obscuro', 'tenebroso', 'negro'],
    'caro': ['custoso', 'dispendioso', 'valioso'],
    'barato': ['econômico', 'acessível', 'em conta', 'módico'],
    'simples': ['singelo', 'descomplicado', 'modesto', 'sóbrio'],
    'complexo': ['complicado', 'intrincado', 'elaborado', 'sofisticado'],
    'útil': ['proveitoso', 'vantajoso', 'prático', 'valioso'],
    'necessário': ['essencial', 'indispensável', 'imprescindível', 'preciso'],
    'possível': ['viável', 'plausível', 'factível', 'provável'],
    'impossível': ['inviável', 'irrealizável', 'inconcebível'],
    'seguro': ['protegido', 'confiável', 'firme', 'estável'],
    'perigoso': ['arriscado', 'nocivo', 'temível', 'ameaçador'],
    'tranquilo': ['calmo', 'sereno', 'sossegado', 'pacífico'],
    'novo': ['recente', 'moderno', 'inédito', 'atual'],
    'moderno': ['atual', 'contemporâneo', 'recente', 'inovador'],
    'antigo': ['velho', 'remoto', 'arcaico', 'vetusto'],
    'velho': ['antigo', 'idoso', 'ancião', 'ultrapassado'],
    'jovem': ['moço', 'novo', 'juvenil', 'adolescente'],
    'diferente': ['distinto', 'diverso', 'desigual', 'variado'],
    'igual': ['idêntico', 'semelhante', 'equivalente', 'parecido'],
    'certo': ['correto', 'exato', 'adequado', 'preciso'],
    'errado': ['incorreto', 'equivocado', 'falso', 'impreciso'],
    'todo': ['inteiro', 'completo', 'total', 'integral'],
    'pessoa': ['indivíduo', 'sujeito', 'cidadão', 'ser'],
    'criança': ['infante', 'pequeno', 'menor'],
    'amigo': ['companheiro', 'camarada', 'colega', 'parceiro'],
    'família': ['parentela', 'clã', 'parentes', 'lar'],
    'cliente': ['consumidor', 'comprador', 'freguês', 'usuário'],
    'grupo': ['conjunto', 'equipe', 'turma', 'coletivo'],
    'casa': ['lar', 'moradia', 'residência', 'habitação'],
    'cidade': ['urbe', 'município', 'metrópole', 'localidade'],
    'país': ['nação', 'pátria', 'estado', 'território'],
    'mundo': ['planeta', 'globo', 'universo', 'terra'],
    'lugar': ['local', 'espaço', 'sítio', 'ponto'],
    'espaço': ['área', 'lugar', 'extensão', 'local'],
    'caminho': ['trajeto', 'rota', 'percurso', 'trilha'],
    'coisa': ['objeto', 'item', 'elemento', 'algo'],
    'objeto': ['item', 'coisa', 'artigo', 'peça'],
    'parte': ['pedaço', 'fração', 'porção', 'trecho'],
    'trabalho': ['serviço', 'labor', 'tarefa', 'ocupação'],
    'empresa': ['companhia', 'firma', 'organização', 'negócio'],
    'produto': ['mercadoria', 'artigo', 'item', 'bem'],
    'serviço': ['trabalho', 'atividade', 'prestação', 'função'],
    'qualidade': ['excelência', 'virtude', 'padrão', 'atributo'],
    'valor': ['importância', 'mérito', 'preço', 'custo'],
    'problema': ['dificuldade', 'obstáculo', 'empecilho', 'impasse'],
    'solução': ['resposta', 'saída', 'resolução', 'remédio'],
    'ideia': ['conceito', 'noção', 'plano', 'sugestão'],
    'projeto': ['plano', 'proposta', 'empreendimento', 'iniciativa'],
    'objetivo': ['meta', 'finalidade', 'propósito', 'alvo'],
    'resultado': ['efeito', 'desfecho', 'consequência', 'produto'],
    'mudança': ['alteração', 'transformação', 'modificação', 'variação'],
    'começo': ['início', 'princípio', 'origem', 'abertura'],
    'fim': ['término', 'final', 'conclusão', 'desfecho'],
    'vida': ['existência', 'vivência', 'trajetória'],
    'tempo': ['período', 'época', 'prazo', 'duração'],
    'momento': ['instante', 'ocasião', 'hora', 'ponto'],
    'forma': ['maneira', 'modo', 'jeito', 'método'],
    'maneira': ['modo', 'forma', 'jeito', 'estilo'],
    'texto': ['escrito', 'redação', 'conteúdo', 'trecho'],
    'palavra': ['termo', 'vocábulo', 'expressão', 'verbete'],
    'frase': ['sentença', 'oração', 'expressão', 'enunciado'],
    'informação': ['dado', 'notícia', 'conhecimento', 'esclarecimento'],
    'conhecimento': ['saber', 'informação', 'instrução', 'sabedoria'],
    'história': ['narrativa', 'relato', 'conto', 'trajetória'],
    'exemplo': ['modelo', 'amostra', 'caso', 'ilustração'],
    'verdade': ['realidade', 'fato', 'veracidade', 'certeza'],
    'erro': ['equívoco', 'engano', 'falha', 'deslize'],
    'falha': ['erro', 'defeito', 'lacuna', 'imperfeição'],
    'sucesso': ['êxito', 'triunfo', 'vitória', 'realização'],
    'medo': ['temor', 'receio', 'pavor', 'apreensão'],
    'alegria': ['contentamento', 'felicidade', 'júbilo', 'satisfação'],
    'tristeza': ['pesar', 'mágoa', 'melancolia', 'desânimo'],
    'amor': ['afeto', 'carinho', 'paixão', 'ternura'],
    'desejo': ['vontade', 'anseio', 'aspiração', 'ambição'],
    'vontade': ['desejo', 'intenção', 'anseio', 'disposição'],
    'força': ['vigor', 'energia', 'potência', 'poder'],
    'cuidado': ['atenção', 'zelo', 'cautela', 'prudência'],
    'atenção': ['cuidado', 'concentração', 'foco', 'zelo'],
    'interesse': ['curiosidade', 'atenção', 'proveito', 'empenho'],
    'ajuda': ['auxílio', 'apoio', 'socorro', 'colaboração'],
    'apoio': ['suporte', 'auxílio', 'amparo', 'sustentação'],
    'opção': ['alternativa', 'escolha', 'possibilidade', 'saída'],
    'escolha': ['opção', 'seleção', 'preferência', 'decisão'],
    'decisão': ['resolução', 'deliberação', 'determinação', 'escolha'],
    'processo': ['procedimento', 'método', 'andamento', 'sistema'],
    'sistema': ['método', 'estrutura', 'mecanismo', 'esquema'],
    'método': ['técnica', 'processo', 'sistema', 'procedimento'],
    'ferramenta': ['instrumento', 'utensílio', 'recurso', 'aparelho'],
    'recurso': ['meio', 'ferramenta', 'instrumento', 'apoio'],
    'muito': ['bastante', 'extremamente', 'imensamente'],
    'sempre': ['constantemente', 'continuamente', 'invariavelmente'],
    'também': ['igualmente', 'ainda', 'além disso', 'do mesmo modo'],
    'porém': ['contudo', 'todavia', 'entretanto', 'no entanto'],
    'mas': ['porém', 'contudo', 'todavia', 'entretanto'],
    'então': ['assim', 'portanto', 'logo', 'nesse caso'],
    'ajudar': ['auxiliar', 'apoiar', 'socorrer', 'colaborar'],
    'fazer': ['realizar', 'executar', 'produzir', 'efetuar'],
    'usar': ['utilizar', 'empregar', 'aplicar', 'manusear'],
    'mostrar': ['exibir', 'apresentar', 'revelar', 'demonstrar'],
    'dizer': ['afirmar', 'declarar', 'falar', 'comentar'],
    'ver': ['enxergar', 'observar', 'notar', 'avistar'],
    'pensar': ['refletir', 'raciocinar', 'considerar', 'cogitar'],
    'querer': ['desejar', 'almejar', 'pretender', 'ambicionar'],
    'precisar': ['necessitar', 'carecer', 'requerer'],
    'conseguir': ['obter', 'alcançar', 'atingir', 'lograr'],
    'criar': ['gerar', 'produzir', 'desenvolver', 'elaborar'],
    'melhorar': ['aprimorar', 'aperfeiçoar', 'progredir', 'evoluir'],
    'aumentar': ['ampliar', 'elevar', 'expandir', 'acrescentar'],
    'diminuir': ['reduzir', 'abaixar', 'encolher', 'atenuar'],
    'escolher': ['selecionar', 'optar', 'eleger', 'preferir'],
    'começar': ['iniciar', 'principiar', 'dar início', 'estrear'],
    'terminar': ['concluir', 'finalizar', 'encerrar', 'acabar']
  };
  var entrada = document.getElementById('sin-entrada');
  var saida = document.getElementById('sin-saida');
  var status = document.getElementById('sin-status');
  var menu = document.getElementById('sin-menu');
  var envoltorio = document.getElementById('sin-area-saida');
  var btnGerar = document.getElementById('sin-gerar');
  var btnCopiar = document.getElementById('sin-copiar');
  var btnLimpar = document.getElementById('sin-limpar');
  var spanAberto = null;
  var indice = 0;
  function tem(k) { return Object.prototype.hasOwnProperty.call(D, k); }
  function termina(w, s) { return w.length >= s.length && w.slice(w.length - s.length) === s; }
  function achar(w) {
    var passos = [{ p: false, t: w }];
    var regras = [['ões', 'ão'], ['ais', 'al'], ['eis', 'el'], ['eis', 'il'], ['ns', 'm'], ['res', 'r'], ['zes', 'z'], ['s', '']];
    regras.forEach(function (r) {
      if (termina(w, r[0]) && w.length > r[0].length + 1) {
        passos.push({ p: true, t: w.slice(0, w.length - r[0].length) + r[1] });
      }
    });
    for (var i = 0; i !== passos.length; i++) {
      var t = passos[i].t;
      if (tem(t)) { return { k: t, p: passos[i].p, f: false }; }
      if (termina(t, 'a')) {
        var m = t.slice(0, t.length - 1) + 'o';
        if (tem(m)) { return { k: m, p: passos[i].p, f: true }; }
      }
    }
    return null;
  }
  function plural(s) {
    if (s === 'cidadão' || s === 'irmão' || s === 'órgão' || s === 'cristão') { return s + 's'; }
    if (termina(s, 'ão')) { return s.slice(0, s.length - 2) + 'ões'; }
    if (termina(s, 'al')) { return s.slice(0, s.length - 2) + 'ais'; }
    if (termina(s, 'el')) { return s.slice(0, s.length - 2) + 'eis'; }
    if (termina(s, 'il')) { return s.slice(0, s.length - 2) + 'eis'; }
    if (termina(s, 'm')) { return s.slice(0, s.length - 1) + 'ns'; }
    if (termina(s, 'r') || termina(s, 'z')) { return s + 'es'; }
    if (termina(s, 's')) { return s; }
    return s + 's';
  }
  function flexionar(s, p, f) {
    if (s.indexOf(' ') !== -1) { return s; }
    if (f && termina(s, 'o')) { s = s.slice(0, s.length - 1) + 'a'; }
    if (p) { s = plural(s); }
    return s;
  }
  function ajustarCaixa(orig, s) {
    if (orig.length > 1 && orig === orig.toUpperCase()) { return s.toUpperCase(); }
    if (orig.charAt(0) !== orig.charAt(0).toLowerCase()) { return s.charAt(0).toUpperCase() + s.slice(1); }
    return s;
  }
  function opcoes(palavra) {
    var base = palavra.toLowerCase();
    if (base.length > 2) {
      var r = achar(base);
      if (r) {
        return D[r.k].map(function (s) { return ajustarCaixa(palavra, flexionar(s, r.p, r.f)); });
      }
    }
    return null;
  }
  function msg(texto, ok) {
    status.style.color = ok ? '#166534' : '#b91c1c';
    status.textContent = texto;
  }
  function msgNeutra(texto) {
    status.style.color = '#64748b';
    status.textContent = texto;
  }
  function estiloPalavra(s) {
    s.style.cursor = 'pointer';
    s.style.borderBottom = '2px dotted #6366f1';
    s.style.outline = 'none';
    s.style.borderRadius = '4px';
    if (s._atual > 0) {
      s.style.background = '#c7d2fe';
      s.style.color = '#3730a3';
      s.style.fontWeight = '600';
    } else {
      s.style.background = 'transparent';
      s.style.color = '#1e293b';
      s.style.fontWeight = 'inherit';
    }
  }
  function criarPalavra(palavra, lista) {
    var s = document.createElement('span');
    s.textContent = palavra;
    s.setAttribute('data-sin', '1');
    s.setAttribute('role', 'button');
    s.setAttribute('aria-haspopup', 'listbox');
    s.tabIndex = 0;
    s._opcoes = [palavra].concat(lista);
    s._atual = 0;
    estiloPalavra(s);
    s.addEventListener('focus', function () { s.style.background = '#e0e7ff'; });
    s.addEventListener('blur', function () { estiloPalavra(s); });
    return s;
  }
  function pintar() {
    Array.prototype.forEach.call(menu.children, function (it, i) {
      it.style.background = i === indice ? '#eef2ff' : 'transparent';
    });
    if (menu.children[indice]) { menu.children[indice].focus(); }
  }
  function fecharMenu(voltar) {
    menu.style.display = 'none';
    var s = spanAberto;
    spanAberto = null;
    if (voltar && s) { s.focus(); }
  }
  function escolher(i) {
    var s = spanAberto;
    if (!s) { return; }
    s.textContent = s._opcoes[i];
    s._atual = i;
    estiloPalavra(s);
    fecharMenu(true);
  }
  function abrirMenu(s) {
    spanAberto = s;
    menu.textContent = '';
    s._opcoes.forEach(function (t, i) {
      var it = document.createElement('div');
      it.setAttribute('role', 'option');
      it.setAttribute('aria-selected', i === s._atual ? 'true' : 'false');
      it.tabIndex = -1;
      it.style.display = 'flex';
      it.style.justifyContent = 'space-between';
      it.style.gap = '12px';
      it.style.padding = '8px 12px';
      it.style.cursor = 'pointer';
      it.style.fontSize = '0.95rem';
      it.style.borderRadius = '8px';
      it.style.outline = 'none';
      it.style.color = i === s._atual ? '#3730a3' : '#1e293b';
      it.style.fontWeight = i === s._atual ? '700' : '400';
      var rotulo = document.createElement('span');
      rotulo.textContent = t;
      it.appendChild(rotulo);
      if (i === 0) {
        var peq = document.createElement('span');
        peq.textContent = 'original';
        peq.style.fontSize = '0.75rem';
        peq.style.color = '#64748b';
        it.appendChild(peq);
      }
      it.addEventListener('mouseenter', function () { indice = i; pintar(); });
      it.addEventListener('click', function () { escolher(i); });
      menu.appendChild(it);
    });
    var r = s.getBoundingClientRect();
    var w = envoltorio.getBoundingClientRect();
    var esq = Math.max(0, Math.min(r.left - w.left, w.width - 190));
    menu.style.left = esq + 'px';
    menu.style.top = (r.bottom - w.top + 4) + 'px';
    menu.style.display = 'block';
    indice = s._atual;
    pintar();
  }
  function gerar() {
    fecharMenu(false);
    saida.textContent = '';
    var txt = entrada.value;
    if (txt.trim() === '') {
      msg('digite ou cole um texto no campo "Texto original".', false);
      entrada.focus();
      return;
    }
    var re = /[A-Za-zÀ-ÖØ-öø-ÿ]+/g;
    var ultimo = 0;
    var total = 0;
    var m;
    while ((m = re.exec(txt)) !== null) {
      if (m.index > ultimo) { saida.appendChild(document.createTextNode(txt.slice(ultimo, m.index))); }
      ultimo = m.index + m[0].length;
      var lista = opcoes(m[0]);
      if (lista) {
        saida.appendChild(criarPalavra(m[0], lista));
        total += 1;
      } else {
        saida.appendChild(document.createTextNode(m[0]));
      }
    }
    if (txt.length > ultimo) { saida.appendChild(document.createTextNode(txt.slice(ultimo))); }
    saida.style.borderColor = '#86efac';
    saida.style.background = '#f0fdf4';
    if (total === 0) {
      msg('nenhuma palavra deste texto tem sinônimos no dicionário da ferramenta. Tente outro texto.', false);
    } else {
      msg(total + (total === 1 ? ' palavra tem' : ' palavras têm') + ' sinônimos. Clique nas palavras sublinhadas para trocar.', true);
    }
  }
  function limpar() {
    fecharMenu(false);
    entrada.value = '';
    saida.textContent = '';
    saida.style.borderColor = '#c7d2fe';
    saida.style.background = '#ffffff';
    msgNeutra('Cole um texto e clique em "Gerar Sinônimos".');
    entrada.focus();
  }
  function copiarFallback(texto) {
    var ta = document.createElement('textarea');
    ta.value = texto;
    ta.style.position = 'fixed';
    ta.style.opacity = '0';
    document.body.appendChild(ta);
    ta.select();
    var ok = false;
    try { ok = document.execCommand('copy'); } catch (e) { ok = false; }
    document.body.removeChild(ta);
    return ok;
  }
  function copiado() {
    var antes = 'Copiar texto';
    btnCopiar.textContent = 'Copiado!';
    setTimeout(function () { btnCopiar.textContent = antes; }, 1500);
  }
  function copiar() {
    var texto = saida.textContent;
    if (texto.trim() === '') { msg('não há texto para copiar. Clique em "Gerar Sinônimos" primeiro.', false); return; }
    if (navigator.clipboard && navigator.clipboard.writeText) {
      navigator.clipboard.writeText(texto).then(copiado, function () {
        if (copiarFallback(texto)) { copiado(); } else { msg('não foi possível copiar. Selecione o texto e copie manualmente.', false); }
      });
    } else if (copiarFallback(texto)) {
      copiado();
    } else {
      msg('não foi possível copiar. Selecione o texto e copie manualmente.', false);
    }
  }
  btnGerar.addEventListener('click', gerar);
  btnCopiar.addEventListener('click', copiar);
  btnLimpar.addEventListener('click', limpar);
  entrada.addEventListener('keydown', function (e) {
    if (e.key === 'Enter' && (e.ctrlKey || e.metaKey)) { e.preventDefault(); gerar(); }
  });
  saida.addEventListener('click', function (e) {
    var s = e.target && e.target.closest ? e.target.closest('[data-sin]') : null;
    if (s && saida.contains(s)) {
      if (spanAberto === s) { fecharMenu(false); } else { abrirMenu(s); }
    }
  });
  saida.addEventListener('keydown', function (e) {
    var s = e.target;
    if (s && s.getAttribute && s.getAttribute('data-sin') && (e.key === 'Enter' || e.key === 'ArrowDown')) {
      e.preventDefault();
      abrirMenu(s);
    }
  });
  menu.addEventListener('keydown', function (e) {
    var n = menu.children.length;
    if (e.key === 'ArrowDown') { e.preventDefault(); indice = (indice + 1) % n; pintar(); }
    else if (e.key === 'ArrowUp') { e.preventDefault(); indice = (indice + n - 1) % n; pintar(); }
    else if (e.key === 'Enter') { e.preventDefault(); escolher(indice); }
    else if (e.key === 'Escape' || e.key === 'Tab') { e.preventDefault(); fecharMenu(true); }
  });
  document.addEventListener('click', function (e) {
    if (!spanAberto) { return; }
    var t = e.target;
    var dentroMenu = menu.contains(t);
    var emPalavra = t && t.closest ? t.closest('[data-sin]') : null;
    if (!dentroMenu && !emPalavra) { fecharMenu(false); }
  });
  [entrada, saida].forEach(function (el) {
    el.addEventListener('focus', function () { el.style.borderColor = '#6366f1'; });
    el.addEventListener('blur', function () {
      el.style.borderColor = (el === saida && saida.textContent.trim() !== '') ? '#86efac' : '#c7d2fe';
    });
  });
  entrada.value = 'A simplicidade é a máxima sofisticação.';
  gerar();
})();
</script>

## Como usar o gerador de textos sinônimos

1. Digite ou cole o seu texto no campo **Texto original**.
2. Clique em **Gerar Sinônimos** (ou pressione Ctrl + Enter dentro do campo).
3. No **Texto com sinônimos**, as palavras sublinhadas têm sinônimos. Clique em uma delas para abrir a lista e escolha a que preferir.
4. A palavra trocada fica destacada, e a palavra original continua no topo da lista, para você voltar a ela quando quiser.
5. Use o botão **Copiar texto** para copiar o resultado e **Limpar** para começar de novo.

O resultado pode ser editado diretamente, como em um editor de texto. Também dá para usar o teclado: Tab vai de uma palavra sublinhada à outra, Enter ou seta para baixo abre a lista, as setas para cima e para baixo percorrem os sinônimos, Enter escolhe e Esc fecha a lista.

Plural e feminino são ajustados automaticamente (por exemplo, pessoas → indivíduos e modernas → atuais). Verbos conjugados ainda não têm sinônimos, apenas os verbos no infinitivo. Como a troca é feita por você, palavra por palavra, leia o texto final antes de usar.

## Entendendo os termos

- **Sinônimo:** palavra com sentido igual ou muito parecido com o de outra, usada para dizer a mesma coisa de outro jeito.
- **Texto original:** o texto que você digita ou cola, antes de qualquer troca de palavras.
- **Texto com sinônimos:** o resultado gerado, em que as palavras com sinônimos aparecem sublinhadas e podem ser trocadas com um clique.
- **Palavra sublinhada:** palavra do texto que tem sinônimos disponíveis. Ao clicar nela, a lista de opções é aberta.
- **Palavra destacada:** palavra que você já trocou por um sinônimo. Ela aparece com fundo colorido para você identificar o que foi alterado.
- **Parafrasear:** reescrever uma ideia com outras palavras, mantendo o mesmo significado.
- **Repetição de palavras:** uso da mesma palavra várias vezes em um texto, o que deixa a leitura cansativa. Os sinônimos ajudam a evitar isso.
- **Vocabulário:** conjunto de palavras que uma pessoa conhece e usa. Variar o vocabulário deixa o texto mais rico.
- **Plural e feminino:** flexões da palavra. A ferramenta ajusta o sinônimo à forma usada no texto (singular ou plural, masculino ou feminino).
- **Verbo conjugado:** verbo flexionado em tempo e pessoa, como "fiz" ou "faremos". Esses verbos ainda não têm sinônimos.
- **Contexto:** o sentido que a palavra tem dentro da frase. Uma palavra pode ter vários sentidos, e nem todo sinônimo combina com o seu texto, por isso vale conferir o resultado.