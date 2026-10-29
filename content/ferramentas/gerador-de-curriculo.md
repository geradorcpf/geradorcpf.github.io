---
title: "Gerador de Currículo"
seoTitle: "Gerador de Currículo"
description: "Gerador de Currículo: monte um currículo profissional e baixe em PDF. Grátis e online, sem cadastro."
summary: "Monte um currículo profissional e baixe em PDF."
date: 2026-10-29
draft: false
category: "financas"
tags: ["currículo", "trabalho", "carreira"]
keywords: ["gerador de currículo", "gerador de currículo online", "currículo", "trabalho", "carreira"]
---

Basta preencher as 4 etapas abaixo e depois clicar em **Baixar PDF**.

<div id="cv-gerador" style="max-width:560px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">📄 Gerador de Currículo</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Preencha as 4 etapas e baixe o seu currículo em PDF.</p>
<div id="cv-passos" style="display:flex;gap:6px;margin-bottom:18px;"></div>
<h3 id="cv-titulo" style="margin:0 0 14px;font-size:1.05rem;color:#3730a3;"></h3>
<div id="cv-conteudo"></div>
<div id="cv-nav" style="display:flex;gap:10px;flex-wrap:wrap;margin-top:6px;"></div>
<div id="cv-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="cv-resultado">preencha os dados e avance pelas etapas.</span></div>
</div>
<script>
(function () {
  var C = {
    input: 'width:100%;padding:12px 14px;margin-bottom:14px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;font-family:inherit;',
    label: 'display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;',
    btn: 'flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);',
    btn2: 'padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;',
    rem: 'padding:6px 12px;font-size:0.85rem;font-weight:600;color:#b91c1c;background:#ffffff;border:2px solid #fca5a5;border-radius:8px;cursor:pointer;',
    card: 'padding:14px;margin-bottom:14px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;',
    row: 'display:flex;gap:10px;flex-wrap:wrap;',
    pill: 'flex:1;padding:8px 4px;font-size:0.75rem;font-weight:600;text-align:center;border-radius:10px;box-sizing:border-box;'
  };
  var STEPS = ['Dados Pessoais', 'Experiência', 'Formação', 'Informações'];
  var TITLES = ['1. Dados pessoais', '2. Experiência profissional', '3. Formação acadêmica', '4. Informações adicionais'];
  var NIVEIS = ['Ensino Fundamental', 'Ensino Médio', 'Curso Técnico', 'Graduação', 'Pós-graduação', 'Mestrado', 'Doutorado'];
  var passos = document.getElementById('cv-passos');
  var titulo = document.getElementById('cv-titulo');
  var conteudo = document.getElementById('cv-conteudo');
  var nav = document.getElementById('cv-nav');
  var caixa = document.getElementById('cv-resposta');
  var resultado = document.getElementById('cv-resultado');
  var step = 0;
  var uid = 0;
  var data = novo();
  function vazioExp() { return { cargo: '', empresa: '', inicio: '', fim: '', descricao: '' }; }
  function vazioEdu() { return { curso: '', instituicao: '', nivel: 'Graduação', inicio: '', fim: '' }; }
  function novo() {
    return {
      nome: '', email: '', celular: '', endereco: '', cidade: '', estado: '', cep: '',
      resumo: '', habilidades: '', idiomas: '', cursos: '', extras: '',
      exp: [vazioExp()], edu: [vazioEdu()]
    };
  }
  function mk(tag, css, txt) {
    var e = document.createElement(tag);
    if (css) { e.style.cssText = css; }
    if (txt) { e.textContent = txt; }
    return e;
  }
  function btn(txt, css, fn) {
    var b = mk('button', css, txt);
    b.type = 'button';
    b.addEventListener('click', fn);
    return b;
  }
  function soDigitos(v) { return String(v).replace(/\D/g, ''); }
  function maskCep(v) {
    var d = soDigitos(v).slice(0, 8);
    if (d.length > 5) { d = d.slice(0, 5) + '-' + d.slice(5); }
    return d;
  }
  function maskTel(v) {
    var d = soDigitos(v).slice(0, 11);
    if (d.length > 10) { return '(' + d.slice(0, 2) + ') ' + d.slice(2, 7) + '-' + d.slice(7); }
    if (d.length > 6) { return '(' + d.slice(0, 2) + ') ' + d.slice(2, 6) + '-' + d.slice(6); }
    if (d.length > 2) { return '(' + d.slice(0, 2) + ') ' + d.slice(2); }
    if (d.length > 0) { return '(' + d; }
    return '';
  }
  function maskUf(v) { return String(v).replace(/[^a-zA-Z]/g, '').toUpperCase().slice(0, 2); }
  function campo(rotulo, obj, chave, op) {
    op = op || {};
    uid += 1;
    var w = mk('div', 'flex:1;min-width:140px;');
    var l = mk('label', C.label, rotulo + (op.req ? ' *' : ''));
    var tag = 'input';
    if (op.area) { tag = 'textarea'; }
    if (op.opcoes) { tag = 'select'; }
    var i = mk(tag, C.input);
    i.id = 'cv-campo-' + uid;
    l.htmlFor = i.id;
    if (op.opcoes) {
      op.opcoes.forEach(function (o) {
        var opt = document.createElement('option');
        opt.value = o;
        opt.textContent = o;
        i.appendChild(opt);
      });
    } else {
      if (op.area) { i.rows = op.rows || 3; i.style.resize = 'vertical'; } else { i.type = 'text'; }
      if (op.ph) { i.placeholder = op.ph; }
      if (op.mode) { i.setAttribute('inputmode', op.mode); }
      i.setAttribute('autocomplete', 'off');
    }
    i.value = obj[chave];
    var atualiza = function () {
      if (op.mask) { i.value = op.mask(i.value); }
      obj[chave] = i.value;
    };
    i.addEventListener('input', atualiza);
    i.addEventListener('change', atualiza);
    i.addEventListener('focus', function () { i.style.borderColor = '#6366f1'; });
    i.addEventListener('blur', function () { i.style.borderColor = '#c7d2fe'; });
    w.appendChild(l);
    w.appendChild(i);
    return w;
  }
  function linha() { return mk('div', C.row); }
  function bloco(arr, rotulo, fabrica, montar, textoAdd) {
    arr.forEach(function (item, idx) {
      var card = mk('div', C.card);
      var topo = mk('div', 'display:flex;justify-content:space-between;align-items:center;margin-bottom:10px;');
      topo.appendChild(mk('strong', 'color:#3730a3;font-size:0.95rem;', rotulo + ' ' + (idx + 1)));
      if (arr.length > 1) {
        topo.appendChild(btn('Remover', C.rem, function () { arr.splice(idx, 1); renderConteudo(); }));
      }
      card.appendChild(topo);
      montar(card, item);
      conteudo.appendChild(card);
    });
    conteudo.appendChild(btn(textoAdd, C.btn2 + 'width:100%;margin-bottom:14px;', function () { arr.push(fabrica()); renderConteudo(); }));
  }
  function renderPassos() {
    passos.textContent = '';
    STEPS.forEach(function (nome, idx) {
      var css = C.pill + 'background:#ffffff;border:2px solid #c7d2fe;color:#64748b;';
      if (idx === step) { css = C.pill + 'background:#4f46e5;border:2px solid #4f46e5;color:#ffffff;'; }
      if (idx > step) { css = C.pill + 'background:#ffffff;border:2px solid #c7d2fe;color:#64748b;'; }
      if (idx !== step) { if (!(idx > step)) { css = C.pill + 'background:#e0e7ff;border:2px solid #c7d2fe;color:#3730a3;cursor:pointer;'; } }
      var p = mk('div', css, (idx + 1) + '. ' + nome);
      if (idx !== step) { if (!(idx > step)) { p.addEventListener('click', function () { irPara(idx); }); } }
      passos.appendChild(p);
    });
  }
  function renderConteudo() {
    conteudo.textContent = '';
    var r;
    if (step === 0) {
      conteudo.appendChild(campo('Nome Completo', data, 'nome', { req: true, ph: 'Ex.: Maria da Silva' }));
      conteudo.appendChild(campo('Email', data, 'email', { req: true, ph: 'Ex.: maria@email.com', mode: 'email' }));
      conteudo.appendChild(campo('Celular', data, 'celular', { ph: 'Ex.: (11) 91234-5678', mode: 'tel', mask: maskTel }));
      conteudo.appendChild(campo('Endereço', data, 'endereco', { ph: 'Ex.: Rua das Flores, 123' }));
      r = linha();
      r.appendChild(campo('Cidade', data, 'cidade', { ph: 'Ex.: São Paulo' }));
      r.appendChild(campo('Estado', data, 'estado', { ph: 'Ex.: SP', mask: maskUf }));
      r.appendChild(campo('CEP', data, 'cep', { ph: 'Ex.: 01234-567', mode: 'numeric', mask: maskCep }));
      conteudo.appendChild(r);
    }
    if (step === 1) {
      bloco(data.exp, 'Experiência', vazioExp, function (card, it) {
        card.appendChild(campo('Cargo', it, 'cargo', { ph: 'Ex.: Assistente Administrativo' }));
        card.appendChild(campo('Empresa', it, 'empresa', { ph: 'Ex.: Empresa Exemplo Ltda.' }));
        var rr = linha();
        rr.appendChild(campo('Início', it, 'inicio', { ph: 'Ex.: 03/2020' }));
        rr.appendChild(campo('Término', it, 'fim', { ph: 'Ex.: 08/2023 ou Atual' }));
        card.appendChild(rr);
        card.appendChild(campo('Atividades realizadas', it, 'descricao', { area: true, rows: 3, ph: 'Descreva suas principais atividades e resultados.' }));
      }, '+ Adicionar experiência');
    }
    if (step === 2) {
      bloco(data.edu, 'Formação', vazioEdu, function (card, it) {
        card.appendChild(campo('Curso', it, 'curso', { ph: 'Ex.: Administração' }));
        card.appendChild(campo('Instituição', it, 'instituicao', { ph: 'Ex.: Universidade Exemplo' }));
        card.appendChild(campo('Nível', it, 'nivel', { opcoes: NIVEIS }));
        var rr = linha();
        rr.appendChild(campo('Início', it, 'inicio', { ph: 'Ex.: 2016' }));
        rr.appendChild(campo('Conclusão', it, 'fim', { ph: 'Ex.: 2020 ou Cursando' }));
        card.appendChild(rr);
      }, '+ Adicionar formação');
    }
    if (step === 3) {
      conteudo.appendChild(campo('Resumo profissional', data, 'resumo', { area: true, rows: 4, ph: 'Ex.: Profissional dedicada, com experiência em atendimento e rotinas administrativas.' }));
      conteudo.appendChild(campo('Habilidades', data, 'habilidades', { area: true, rows: 2, ph: 'Ex.: Pacote Office, comunicação, trabalho em equipe' }));
      conteudo.appendChild(campo('Idiomas', data, 'idiomas', { ph: 'Ex.: Inglês (intermediário), Espanhol (básico)' }));
      conteudo.appendChild(campo('Cursos e certificações', data, 'cursos', { area: true, rows: 2, ph: 'Ex.: Excel Avançado (40h) - Curso Exemplo, 2022' }));
      conteudo.appendChild(campo('Informações adicionais', data, 'extras', { area: true, rows: 2, ph: 'Ex.: CNH categoria B, disponibilidade para viagens' }));
    }
  }
  function renderNav() {
    nav.textContent = '';
    if (step > 0) { nav.appendChild(btn('Voltar', C.btn2, function () { irPara(step - 1); })); }
    if (step !== 3) {
      nav.appendChild(btn('Próximo', C.btn, proximo));
    } else {
      nav.appendChild(btn('Baixar PDF', C.btn, baixar));
    }
    nav.appendChild(btn('Limpar', C.btn2, limpar));
  }
  function renderTudo() {
    renderPassos();
    titulo.textContent = TITLES[step];
    renderConteudo();
    renderNav();
  }
  function mostrar(tipo, msg) {
    if (tipo === 'erro') {
      caixa.style.borderColor = '#fca5a5';
      caixa.style.background = '#fef2f2';
      resultado.style.color = '#b91c1c';
    } else if (tipo === 'ok') {
      caixa.style.borderColor = '#86efac';
      caixa.style.background = '#f0fdf4';
      resultado.style.color = '#166534';
    } else {
      caixa.style.borderColor = '#c7d2fe';
      caixa.style.background = '#ffffff';
      resultado.style.color = '#64748b';
    }
    resultado.textContent = msg;
  }
  function validar() {
    if (data.nome.trim() === '') { return 'informe o nome completo.'; }
    if (!/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(data.email.trim())) { return 'informe um email válido.'; }
    return '';
  }
  function irPara(n) {
    step = n;
    renderTudo();
    mostrar('info', 'etapa ' + (n + 1) + ' de 4: ' + TITLES[n].slice(3).toLowerCase() + '.');
  }
  function proximo() {
    if (step === 0) {
      var m = validar();
      if (m) { mostrar('erro', m); return; }
    }
    irPara(step + 1);
  }
  function limpar() {
    data = novo();
    step = 0;
    renderTudo();
    mostrar('info', 'preencha os dados e avance pelas etapas.');
  }
  /* ---------- Geração do PDF (sem bibliotecas externas) ---------- */
  function enc(s) {
    var out = '';
    s = String(s);
    for (var i = 0; i !== s.length; i++) {
      var c = s.charCodeAt(i);
      if (c === 8211 || c === 8212) { c = 45; }
      else if (c === 8216 || c === 8217) { c = 39; }
      else if (c === 8220 || c === 8221) { c = 34; }
      else if (c === 8226) { c = 149; }
      else if (c === 9) { c = 32; }
      else if (c > 255) { c = 63; }
      else if (!(c > 31)) { c = 32; }
      if (c === 40 || c === 41 || c === 92) { out += '\\'; }
      out += String.fromCharCode(c);
    }
    return out;
  }
  function quebra(str, size, bold, maxW) {
    var f = size * (bold ? 0.58 : 0.53);
    var max = Math.max(10, Math.floor(maxW / f));
    var out = [];
    String(str).split('\n').forEach(function (par) {
      var line = '';
      par.split(' ').forEach(function (w) {
        while (w.length > max) {
          if (line) { out.push(line); line = ''; }
          out.push(w.slice(0, max));
          w = w.slice(max);
        }
        if (!w) { return; }
        var t = line ? line + ' ' + w : w;
        if (t.length > max) { out.push(line); line = w; } else { line = t; }
      });
      out.push(line);
    });
    return out;
  }
  function pad10(n) { return ('0000000000' + n).slice(-10); }
  function gerarPdf() {
    var IND = [0.22, 0.19, 0.64];
    var GRAY = [0.4, 0.45, 0.52];
    var DARK = [0.12, 0.16, 0.23];
    var pg = [];
    var cur = '';
    var y = 0;
    function nova() { if (cur) { pg.push(cur); } cur = ''; y = 792; }
    function esp(h) { if (y - h > 49) { return; } nova(); }
    function lin(str, size, bold, x, rgb) {
      esp(size * 1.4);
      y -= size;
      cur += rgb[0] + ' ' + rgb[1] + ' ' + rgb[2] + ' rg BT /F' + (bold ? 2 : 1) + ' ' + size + ' Tf ' + x + ' ' + y.toFixed(2) + ' Td (' + enc(str) + ') Tj ET\n';
      y -= size * 0.35;
    }
    function par(str, size, bold, rgb) {
      quebra(str, size, bold, 495).forEach(function (l) { lin(l, size, bold, 50, rgb); });
    }
    function sec(t) {
      y -= 10;
      esp(44);
      lin(t.toUpperCase(), 12, true, 50, IND);
      cur += '0.78 0.82 0.99 RG 1 w 50 ' + y.toFixed(2) + ' m 545 ' + y.toFixed(2) + ' l S\n';
      y -= 8;
    }
    function junta(arr, sep) { return arr.filter(function (v) { return v; }).join(sep); }
    nova();
    lin(data.nome.trim(), 22, true, 50, IND);
    y -= 2;
    var contato = junta([data.email.trim(), data.celular.trim()], '  |  ');
    if (contato) { par(contato, 10, false, GRAY); }
    var cidUf = data.cidade.trim();
    if (data.estado.trim()) { cidUf = cidUf ? cidUf + ' - ' + data.estado.trim() : data.estado.trim(); }
    var ender = junta([data.endereco.trim(), cidUf, data.cep.trim() ? 'CEP ' + data.cep.trim() : ''], ', ');
    if (ender) { par(ender, 10, false, GRAY); }
    if (data.resumo.trim()) { sec('Resumo profissional'); par(data.resumo.trim(), 10.5, false, DARK); }
    var exps = data.exp.filter(function (e) { return e.cargo.trim() || e.empresa.trim() || e.descricao.trim(); });
    if (exps.length > 0) {
      sec('Experiência profissional');
      exps.forEach(function (e) {
        par(junta([e.cargo.trim(), e.empresa.trim()], ' - '), 11, true, DARK);
        var per = e.inicio.trim() ? e.inicio.trim() + ' - ' + (e.fim.trim() || 'Atual') : e.fim.trim();
        if (per) { par(per, 9.5, false, GRAY); }
        if (e.descricao.trim()) { par(e.descricao.trim(), 10, false, DARK); }
        y -= 6;
      });
    }
    var edus = data.edu.filter(function (e) { return e.curso.trim() || e.instituicao.trim(); });
    if (edus.length > 0) {
      sec('Formação acadêmica');
      edus.forEach(function (e) {
        par(e.curso.trim() || e.instituicao.trim(), 11, true, DARK);
        var sub = junta([e.curso.trim() ? e.instituicao.trim() : '', e.nivel], ' - ');
        if (sub) { par(sub, 10, false, DARK); }
        var per = e.inicio.trim() ? e.inicio.trim() + ' - ' + (e.fim.trim() || 'Atual') : e.fim.trim();
        if (per) { par(per, 9.5, false, GRAY); }
        y -= 6;
      });
    }
    if (data.habilidades.trim()) { sec('Habilidades'); par(data.habilidades.trim(), 10, false, DARK); }
    if (data.idiomas.trim()) { sec('Idiomas'); par(data.idiomas.trim(), 10, false, DARK); }
    if (data.cursos.trim()) { sec('Cursos e certificações'); par(data.cursos.trim(), 10, false, DARK); }
    if (data.extras.trim()) { sec('Informações adicionais'); par(data.extras.trim(), 10, false, DARK); }
    pg.push(cur);
    var n = pg.length;
    var objs = [];
    var kids = [];
    for (var i = 0; i !== n; i++) { kids.push((5 + 2 * i) + ' 0 R'); }
    objs[1] = '<< /Type /Catalog /Pages 2 0 R >>';
    objs[2] = '<< /Type /Pages /Kids [' + kids.join(' ') + '] /Count ' + n + ' >>';
    objs[3] = '<< /Type /Font /Subtype /Type1 /BaseFont /Helvetica /Encoding /WinAnsiEncoding >>';
    objs[4] = '<< /Type /Font /Subtype /Type1 /BaseFont /Helvetica-Bold /Encoding /WinAnsiEncoding >>';
    pg.forEach(function (conteudoPg, k) {
      objs[5 + 2 * k] = '<< /Type /Page /Parent 2 0 R /MediaBox [0 0 595 842] /Resources << /Font << /F1 3 0 R /F2 4 0 R >> >> /Contents ' + (6 + 2 * k) + ' 0 R >>';
      objs[6 + 2 * k] = '<< /Length ' + conteudoPg.length + ' >>\nstream\n' + conteudoPg + 'endstream';
    });
    var total = objs.length - 1;
    var out = '%PDF-1.4\n';
    var offs = [];
    for (var j = 1; j !== total + 1; j++) {
      offs[j] = out.length;
      out += j + ' 0 obj\n' + objs[j] + '\nendobj\n';
    }
    var xref = out.length;
    out += 'xref\n0 ' + (total + 1) + '\n0000000000 65535 f \n';
    for (var m = 1; m !== total + 1; m++) { out += pad10(offs[m]) + ' 00000 n \n'; }
    out += 'trailer\n<< /Size ' + (total + 1) + ' /Root 1 0 R >>\nstartxref\n' + xref + '\n%%EOF';
    var bytes = new Uint8Array(out.length);
    for (var b = 0; b !== out.length; b++) { bytes[b] = out.charCodeAt(b) & 255; }
    return bytes;
  }
  function nomeArquivo() {
    var s = data.nome.toLowerCase();
    if (s.normalize) { s = s.normalize('NFD').replace(/[\u0300-\u036f]/g, ''); }
    s = s.replace(/[^a-z0-9]+/g, '-').replace(/^-+|-+$/g, '');
    return 'curriculo-' + (s || 'novo') + '.pdf';
  }
  function baixar() {
    var m = validar();
    if (m) { irPara(0); mostrar('erro', m); return; }
    try {
      var blob = new Blob([gerarPdf()], { type: 'application/pdf' });
      var url = URL.createObjectURL(blob);
      var a = document.createElement('a');
      a.href = url;
      a.download = nomeArquivo();
      document.body.appendChild(a);
      a.click();
      document.body.removeChild(a);
      setTimeout(function () { URL.revokeObjectURL(url); }, 4000);
      mostrar('ok', 'currículo gerado! O download do PDF foi iniciado.');
    } catch (e) {
      mostrar('erro', 'não foi possível gerar o PDF. Tente novamente.');
    }
  }
  renderTudo();
})();
</script>

## Como usar o gerador de currículo

1. Na etapa **Dados Pessoais**, informe o nome completo e o email (campos obrigatórios) e, se quiser, celular, endereço, cidade, estado e CEP.
2. Clique em **Próximo** e, na etapa **Experiência**, preencha cargo, empresa, período e atividades. Use **+ Adicionar experiência** para incluir mais de um emprego.
3. Na etapa **Formação**, informe curso, instituição, nível e período. Use **+ Adicionar formação** para cadastrar mais de uma formação.
4. Na etapa **Informações**, escreva o resumo profissional, as habilidades, os idiomas, os cursos e qualquer informação extra.
5. Clique em **Baixar PDF** para salvar o currículo no seu dispositivo.
6. Use **Voltar** para corrigir etapas anteriores ou **Limpar** para apagar tudo e começar um novo currículo.

Os campos que ficarem vazios não aparecem no PDF. Tudo é feito no seu navegador: os dados não são enviados nem armazenados em nenhum servidor.

## Entendendo os termos

- **Currículo:** documento que resume a sua trajetória profissional e acadêmica para apresentar a empresas e recrutadores. Também é chamado de *curriculum vitae* (CV).
- **Dados pessoais:** informações de identificação e contato, como nome, email, celular e endereço.
- **CEP:** código de endereçamento postal, formado por 8 dígitos (por exemplo, 01234-567).
- **Experiência profissional:** empregos, estágios e trabalhos anteriores, com cargo, empresa, período e principais atividades.
- **Cargo:** função que você exercia na empresa, como assistente, analista ou vendedor.
- **Formação acadêmica:** cursos de ensino formal que você concluiu ou está cursando, como ensino médio, curso técnico e graduação.
- **Nível:** grau do curso, como Ensino Médio, Graduação, Pós-graduação, Mestrado ou Doutorado.
- **Resumo profissional:** pequeno texto de apresentação, com poucas linhas, sobre quem você é e o que busca.
- **Habilidades:** competências que você domina, como pacote Office, atendimento ao cliente ou comunicação.
- **Idiomas:** línguas que você fala, com o nível de domínio (básico, intermediário, avançado ou fluente).
- **Cursos e certificações:** cursos livres, treinamentos e certificados complementares, geralmente com carga horária.
- **Informações adicionais:** dados extras úteis para a vaga, como CNH, disponibilidade de horário ou para viagens.
- **PDF:** formato de arquivo que mantém o layout do documento igual em qualquer dispositivo, ideal para enviar currículos.