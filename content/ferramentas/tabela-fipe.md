---
title: "Tabela Fipe Veículos"
seoTitle: "Tabela Fipe Veículos"
description: "Tabela Fipe Veículos: consulte o preço de veículos na tabela Fipe. Grátis e online, sem cadastro."
summary: "Consulte o preço de veículos na tabela Fipe."
date: 2026-11-11
draft: false
category: "financas"
tags: ["fipe", "veículos", "preços", "finanças"]
keywords: ["tabela fipe veículos", "tabela fipe veículos online", "fipe", "veículos", "preços"]
---

Escolha o tipo de veículo, a marca, o modelo e o ano abaixo e depois clique em **Consultar Preço**.

<div id="calc-fipe" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🚗 Tabela Fipe Veículos</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Consulte o preço médio de carros, motos e caminhões.</p>
<div style="display:flex;gap:8px;flex-wrap:wrap;margin-bottom:18px;">
<button type="button" id="fipe-tipo-cars" style="flex:1;min-width:100px;padding:10px 12px;font-size:0.95rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:2px solid #4f46e5;border-radius:10px;cursor:pointer;">Carros</button>
<button type="button" id="fipe-tipo-motorcycles" style="flex:1;min-width:100px;padding:10px 12px;font-size:0.95rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Motos</button>
<button type="button" id="fipe-tipo-trucks" style="flex:1;min-width:100px;padding:10px 12px;font-size:0.95rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Caminhões</button>
</div>
<label for="fipe-marca" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Marca</label>
<select id="fipe-marca" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;"></select>
<label for="fipe-modelo" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Modelo</label>
<select id="fipe-modelo" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;"></select>
<label for="fipe-ano" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Ano Modelo</label>
<select id="fipe-ano" style="width:100%;padding:12px 14px;margin-bottom:20px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;"></select>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="fipe-consultar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Consultar Preço</button>
<button type="button" id="fipe-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="fipe-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="fipe-resultado">escolha o veículo e clique em "Consultar Preço".</span></div>
<div id="fipe-historico" style="margin-top:16px;"></div>
</div>
<script>
(function () {
  var BASE = 'https://fipe.parallelum.com.br/api/v2';
  var tipo = 'cars';
  var selMarca = document.getElementById('fipe-marca');
  var selModelo = document.getElementById('fipe-modelo');
  var selAno = document.getElementById('fipe-ano');
  var caixa = document.getElementById('fipe-resposta');
  var resultado = document.getElementById('fipe-resultado');
  var areaHist = document.getElementById('fipe-historico');
  var ultimo = null;
  var TEXTO_INICIAL = 'escolha o veículo e clique em "Consultar Preço".';
  var abas = {
    cars: document.getElementById('fipe-tipo-cars'),
    motorcycles: document.getElementById('fipe-tipo-motorcycles'),
    trucks: document.getElementById('fipe-tipo-trucks')
  };
  function get(url) {
    return fetch(url).then(function (r) {
      if (!r.ok) { throw new Error('HTTP ' + r.status); }
      return r.json();
    });
  }
  function limparNo(n) {
    while (n.firstChild) { n.removeChild(n.firstChild); }
  }
  function estado(cor, fundo, texto) {
    caixa.style.borderColor = cor;
    caixa.style.background = fundo;
    resultado.style.color = texto;
  }
  function mensagem(tipoMsg, msg) {
    limparNo(resultado);
    limparNo(areaHist);
    if (tipoMsg === 'erro') { estado('#fca5a5', '#fef2f2', '#b91c1c'); }
    else if (tipoMsg === 'ok') { estado('#86efac', '#f0fdf4', '#166534'); }
    else { estado('#c7d2fe', '#ffffff', '#64748b'); }
    resultado.textContent = msg;
  }
  function preencher(sel, itens, rotulo) {
    limparNo(sel);
    var o = document.createElement('option');
    o.value = '';
    o.textContent = rotulo;
    sel.appendChild(o);
    itens.forEach(function (it) {
      var op = document.createElement('option');
      op.value = String(it.code);
      op.textContent = it.name;
      sel.appendChild(op);
    });
    sel.disabled = itens.length === 0;
  }
  function resetar(sel, rotulo) {
    preencher(sel, [], rotulo);
  }
  function lista(dados) {
    if (Array.isArray(dados)) { return dados; }
    if (dados && Array.isArray(dados.models)) { return dados.models; }
    return [];
  }
  function marcarAba(t) {
    Object.keys(abas).forEach(function (k) {
      var b = abas[k];
      if (k === t) {
        b.style.color = '#ffffff';
        b.style.background = 'linear-gradient(135deg,#4f46e5,#6366f1)';
        b.style.borderColor = '#4f46e5';
        b.style.fontWeight = '700';
      } else {
        b.style.color = '#4f46e5';
        b.style.background = '#ffffff';
        b.style.borderColor = '#c7d2fe';
        b.style.fontWeight = '600';
      }
    });
  }
  function carregarMarcas() {
    resetar(selMarca, 'Carregando marcas...');
    resetar(selModelo, 'Selecione a marca primeiro');
    resetar(selAno, 'Selecione o modelo primeiro');
    get(BASE + '/' + tipo + '/brands').then(function (d) {
      preencher(selMarca, lista(d), 'Selecione a marca');
    }).catch(function () {
      resetar(selMarca, 'Erro ao carregar');
      mensagem('erro', 'não foi possível carregar as marcas. Tente novamente em instantes.');
    });
  }
  function carregarModelos() {
    resetar(selAno, 'Selecione o modelo primeiro');
    if (!selMarca.value) { resetar(selModelo, 'Selecione a marca primeiro'); return; }
    resetar(selModelo, 'Carregando modelos...');
    get(BASE + '/' + tipo + '/brands/' + selMarca.value + '/models').then(function (d) {
      preencher(selModelo, lista(d), 'Selecione o modelo');
    }).catch(function () {
      resetar(selModelo, 'Erro ao carregar');
      mensagem('erro', 'não foi possível carregar os modelos.');
    });
  }
  function carregarAnos() {
    if (!selModelo.value) { resetar(selAno, 'Selecione o modelo primeiro'); return; }
    resetar(selAno, 'Carregando anos...');
    get(BASE + '/' + tipo + '/brands/' + selMarca.value + '/models/' + selModelo.value + '/years').then(function (d) {
      preencher(selAno, lista(d), 'Selecione o ano');
    }).catch(function () {
      resetar(selAno, 'Erro ao carregar');
      mensagem('erro', 'não foi possível carregar os anos.');
    });
  }
  function urlVeiculo(q) {
    return BASE + '/' + ultimo.tipo + '/brands/' + ultimo.marca + '/models/' + ultimo.modelo + '/years/' + ultimo.ano + q;
  }
  function linha(rotulo, valor, destaque) {
    var d = document.createElement('div');
    d.style.margin = '4px 0';
    var s = document.createElement('strong');
    s.textContent = rotulo + ': ';
    var v = document.createElement('span');
    v.textContent = valor;
    if (destaque) { v.style.fontSize = '1.2rem'; v.style.fontWeight = '700'; }
    d.appendChild(s);
    d.appendChild(v);
    return d;
  }
  function consultar() {
    if (!selMarca.value || !selModelo.value || !selAno.value) {
      mensagem('erro', 'selecione marca, modelo e ano do veículo.');
      return;
    }
    ultimo = { tipo: tipo, marca: selMarca.value, modelo: selModelo.value, ano: selAno.value };
    mensagem('neutro', 'consultando...');
    get(urlVeiculo('')).then(function (v) {
      mensagem('ok', '');
      resultado.appendChild(linha('Veículo', v.brand + ' ' + v.model, false));
      resultado.appendChild(linha('Combustível', v.fuel, false));
      resultado.appendChild(linha('Mês de referência', String(v.referenceMonth).trim(), false));
      resultado.appendChild(linha('Código Fipe', v.codeFipe, false));
      resultado.appendChild(linha('Preço médio', v.price, true));
      var b = document.createElement('button');
      b.type = 'button';
      b.textContent = 'Ver histórico de preços';
      b.style.cssText = 'margin-top:12px;padding:10px 16px;font-size:0.95rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;';
      b.addEventListener('click', function () { b.disabled = true; historico(); });
      areaHist.appendChild(b);
    }).catch(function () {
      mensagem('erro', 'não foi possível consultar este veículo. Tente novamente em instantes.');
    });
  }
  function paraNumero(texto) {
    var t = String(texto).replace('R$', '').replace(/\s/g, '').replace(/\./g, '').replace(',', '.');
    return Number(t);
  }
  function moeda(n) {
    return 'R$ ' + n.toLocaleString('pt-BR', { maximumFractionDigits: 0 });
  }
  function rotuloMes(m) {
    var partes = String(m).trim().split('/');
    return partes[0].slice(0, 3) + '/' + String(partes[1]).slice(-2);
  }
  function historico() {
    limparNo(areaHist);
    var aviso = document.createElement('p');
    aviso.style.cssText = 'margin:0;font-size:0.9rem;color:#64748b;';
    aviso.textContent = 'Carregando histórico...';
    areaHist.appendChild(aviso);
    get(BASE + '/references').then(function (refs) {
      var recentes = refs.slice(0, 12);
      return Promise.all(recentes.map(function (ref) {
        return get(urlVeiculo('?reference=' + ref.code)).then(function (v) {
          return { mes: ref.month, valor: paraNumero(v.price) };
        }).catch(function () { return null; });
      }));
    }).then(function (res) {
      var pontos = res.filter(function (p) { return p !== null && !isNaN(p.valor); }).reverse();
      if (pontos.length === 0) { throw new Error('sem dados'); }
      desenhar(pontos);
    }).catch(function () {
      limparNo(areaHist);
      var e = document.createElement('p');
      e.style.cssText = 'margin:0;font-size:0.9rem;color:#b91c1c;';
      e.textContent = 'não foi possível carregar o histórico de preços.';
      areaHist.appendChild(e);
    });
  }
  function desenhar(pontos) {
    limparNo(areaHist);
    var NS = 'http://www.w3.org/2000/svg';
    var W = 560, H = 240, PX = 16, PT = 24, PB = 36;
    var valores = pontos.map(function (p) { return p.valor; });
    var min = Math.min.apply(null, valores);
    var max = Math.max.apply(null, valores);
    var faixa = max - min;
    if (faixa === 0) { faixa = 1; }
    var n = pontos.length;
    function px(i) { return n === 1 ? W / 2 : PX + i * (W - 2 * PX) / (n - 1); }
    function py(v) { return PT + (max - v) * (H - PT - PB) / faixa; }
    var titulo = document.createElement('div');
    titulo.style.cssText = 'font-weight:700;font-size:0.95rem;color:#3730a3;margin-bottom:8px;';
    titulo.textContent = 'Histórico de preços (últimos ' + n + ' meses)';
    areaHist.appendChild(titulo);
    var svg = document.createElementNS(NS, 'svg');
    svg.setAttribute('viewBox', '0 0 ' + W + ' ' + H);
    svg.setAttribute('width', '100%');
    svg.style.cssText = 'background:#ffffff;border:2px solid #c7d2fe;border-radius:12px;display:block;';
    var pts = pontos.map(function (p, i) { return px(i) + ',' + py(p.valor); }).join(' ');
    var linhaSvg = document.createElementNS(NS, 'polyline');
    linhaSvg.setAttribute('points', pts);
    linhaSvg.setAttribute('fill', 'none');
    linhaSvg.setAttribute('stroke', '#4f46e5');
    linhaSvg.setAttribute('stroke-width', '3');
    linhaSvg.setAttribute('stroke-linejoin', 'round');
    svg.appendChild(linhaSvg);
    pontos.forEach(function (p, i) {
      var c = document.createElementNS(NS, 'circle');
      c.setAttribute('cx', px(i));
      c.setAttribute('cy', py(p.valor));
      c.setAttribute('r', '4');
      c.setAttribute('fill', '#6366f1');
      var tt = document.createElementNS(NS, 'title');
      tt.textContent = String(p.mes).trim() + ': ' + moeda(p.valor);
      c.appendChild(tt);
      svg.appendChild(c);
    });
    function texto(x, y, anchor, conteudo) {
      var t = document.createElementNS(NS, 'text');
      t.setAttribute('x', x);
      t.setAttribute('y', y);
      t.setAttribute('text-anchor', anchor);
      t.setAttribute('font-size', '12');
      t.setAttribute('fill', '#475569');
      t.textContent = conteudo;
      svg.appendChild(t);
    }
    texto(PX, H - 12, 'start', rotuloMes(pontos[0].mes));
    texto(W - PX, H - 12, 'end', rotuloMes(pontos[n - 1].mes));
    texto(PX, 14, 'start', 'Máx.: ' + moeda(max));
    texto(W - PX, 14, 'end', 'Mín.: ' + moeda(min));
    areaHist.appendChild(svg);
  }
  function limpar() {
    selMarca.value = '';
    resetar(selModelo, 'Selecione a marca primeiro');
    resetar(selAno, 'Selecione o modelo primeiro');
    ultimo = null;
    mensagem('neutro', TEXTO_INICIAL);
  }
  Object.keys(abas).forEach(function (k) {
    abas[k].addEventListener('click', function () {
      tipo = k;
      marcarAba(k);
      mensagem('neutro', TEXTO_INICIAL);
      carregarMarcas();
    });
  });
  selMarca.addEventListener('change', carregarModelos);
  selModelo.addEventListener('change', carregarAnos);
  document.getElementById('fipe-consultar').addEventListener('click', consultar);
  document.getElementById('fipe-limpar').addEventListener('click', limpar);
  [selMarca, selModelo, selAno].forEach(function (el) {
    el.addEventListener('focus', function () { el.style.borderColor = '#6366f1'; });
    el.addEventListener('blur', function () { el.style.borderColor = '#c7d2fe'; });
  });
  carregarMarcas();
})();
</script>

## Como usar a consulta

1. Escolha o tipo de veículo: **Carros**, **Motos** ou **Caminhões**.
2. Selecione a **Marca** na primeira lista.
3. Selecione o **Modelo**. A lista é carregada de acordo com a marca escolhida.
4. Selecione o **Ano Modelo** (e o combustível, quando houver mais de uma versão).
5. Clique em **Consultar Preço** para ver o mês de referência, o código Fipe e o preço médio.
6. Clique em **Ver histórico de preços** para ver, em gráfico, a variação do valor nos últimos meses.
7. Use o botão **Limpar** para fazer uma nova consulta.

Os dados são carregados online, então é preciso estar conectado à internet. Se a consulta falhar, aguarde alguns instantes e tente novamente.

## Entendendo os termos

- **Tabela Fipe:** tabela de preços médios de veículos praticados no mercado brasileiro, divulgada todos os meses pela Fundação Instituto de Pesquisas Econômicas (Fipe).
- **Marca:** fabricante do veículo, como Fiat, Honda ou Volkswagen.
- **Modelo:** versão específica do veículo dentro da marca, incluindo motorização e acabamento.
- **Ano Modelo:** ano de referência do projeto do veículo, que pode ser diferente do ano de fabricação. Veículos zero km aparecem com o ano 32000.
- **Mês de referência:** mês a que se refere o preço consultado. A Fipe atualiza os valores mensalmente.
- **Código Fipe:** código único que identifica o modelo na tabela, no formato 000000-0.
- **Preço médio:** valor médio de mercado do veículo no mês de referência. É um parâmetro, e não o preço final de uma venda.
- **Combustível:** tipo de combustível do veículo, como gasolina, álcool, diesel ou flex.
- **Histórico de preços:** evolução do preço médio do mesmo veículo ao longo dos meses.

## Para que serve a Tabela Fipe

A Tabela Fipe é usada como referência na compra e venda de veículos novos e usados, no cálculo de seguros, financiamentos, impostos como o IPVA e avaliações de patrimônio. O preço real de negociação pode ser maior ou menor, conforme o estado de conservação, a quilometragem, a região e a demanda do mercado.