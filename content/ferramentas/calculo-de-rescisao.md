---
title: "Cálculo de Rescisão de Contrato"
seoTitle: "Cálculo de Rescisão de Contrato"
description: "Cálculo de Rescisão de Contrato: estime as verbas de uma rescisão de contrato de trabalho. Grátis e online, sem cadastro."
summary: "Estime as verbas de uma rescisão de contrato de trabalho."
date: 2026-10-24
draft: false
category: "financas"
tags: ["rescisão", "trabalho", "direitos trabalhistas", "calculadora"]
keywords: ["cálculo de rescisão de contrato", "cálculo de rescisão de contrato online", "rescisão", "trabalho", "direitos trabalhistas"]
---
<!--sudah dikerjakan-->

Preencha os dados do contrato abaixo e clique em **Calcular Rescisão** para estimar o valor do acerto trabalhista.

<div id="calc-rescisao" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🧾 Calculadora de Rescisão de Contrato</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Informe os dados do contrato e veja a estimativa na hora.</p>
<label for="resc-salario" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Salário base (R$)</label>
<input id="resc-salario" type="text" inputmode="decimal" placeholder="Ex.: 3000,00" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<label for="resc-dependentes" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Nº de dependentes</label>
<input id="resc-dependentes" type="text" inputmode="numeric" placeholder="Ex.: 0" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<label for="resc-inicio" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Início do contrato de trabalho</label>
<input id="resc-inicio" type="date" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;font-family:inherit;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<label for="resc-fim" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Fim do contrato de trabalho</label>
<input id="resc-fim" type="date" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;font-family:inherit;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<label for="resc-motivo" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Motivo da rescisão contratual</label>
<select id="resc-motivo" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;font-family:inherit;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<option value="pedido">Pedido de demissão</option>
<option value="justa">Dispensa com justa causa</option>
<option value="semjusta" selected>Dispensa sem justa causa</option>
<option value="experiencia">Fim do contrato de experiência</option>
</select>
<label for="resc-ferias" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Você possui férias vencidas?</label>
<select id="resc-ferias" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;font-family:inherit;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<option value="nao" selected>Não</option>
<option value="sim">Sim</option>
</select>
<label for="resc-aviso" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">O aviso prévio foi cumprido?</label>
<select id="resc-aviso" style="width:100%;padding:12px 14px;margin-bottom:20px;font-size:1rem;font-family:inherit;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<option value="sim" selected>Sim</option>
<option value="nao">Não</option>
</select>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="resc-calcular" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Calcular Rescisão</button>
<button type="button" id="resc-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="resc-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="resc-resultado">preencha os campos e clique em "Calcular Rescisão".</span></div>
<p style="margin:14px 0 0;font-size:0.8rem;color:#64748b;line-height:1.5;">Importante: esta ferramenta dá apenas uma noção do valor da rescisão e não substitui um profissional habilitado (contador ou advogado trabalhista).</p>
</div>
<script>
(function () {
  var elSalario = document.getElementById('resc-salario');
  var elDep = document.getElementById('resc-dependentes');
  var elInicio = document.getElementById('resc-inicio');
  var elFim = document.getElementById('resc-fim');
  var elMotivo = document.getElementById('resc-motivo');
  var elFerias = document.getElementById('resc-ferias');
  var elAviso = document.getElementById('resc-aviso');
  var caixa = document.getElementById('resc-resposta');
  var resultado = document.getElementById('resc-resultado');
  var TEXTO_INICIAL = 'preencha os campos e clique em "Calcular Rescisão".';
  function numero(v) {
    var t = String(v).trim().replace(/\s/g, '');
    if (t.indexOf(',') > -1) { t = t.replace(/\./g, '').replace(',', '.'); }
    if (t === '' || isNaN(Number(t))) { return NaN; }
    return Number(t);
  }
  function r2(n) { return Math.round((n + 0.0000001) * 100) / 100; }
  function brl(n) { return n.toLocaleString('pt-BR', { style: 'currency', currency: 'BRL' }); }
  function lerData(v) {
    var p = String(v).split('-');
    if (p.length !== 3) { return null; }
    var o = { y: Number(p[0]), m: Number(p[1]), d: Number(p[2]) };
    if (isNaN(o.y) || isNaN(o.m) || isNaN(o.d)) { return null; }
    if (o.y > 1899) { return o; }
    return null;
  }
  function utc(o) { return Date.UTC(o.y, o.m - 1, o.d); }
  function diasNoMes(y, m) { return new Date(Date.UTC(y, m, 0)).getUTCDate(); }
  function somarDias(o, n) {
    var t = new Date(utc(o) + n * 86400000);
    return { y: t.getUTCFullYear(), m: t.getUTCMonth() + 1, d: t.getUTCDate() };
  }
  function anosCompletos(ini, fim) {
    var a = fim.y - ini.y;
    if (ini.m * 100 + ini.d > fim.m * 100 + fim.d) { a = a - 1; }
    return a;
  }
  function meses(ini, fim) {
    var y = ini.y;
    var m = ini.m;
    var d = ini.d;
    var total = 0;
    var dias = 0;
    while (true) {
      if (y > fim.y) { break; }
      if (y === fim.y && m === fim.m) {
        dias = fim.d - d + 1;
        if (dias > 14) { total = total + 1; }
        break;
      }
      dias = diasNoMes(y, m) - d + 1;
      if (dias > 14) { total = total + 1; }
      m = m + 1;
      if (m > 12) { m = 1; y = y + 1; }
      d = 1;
    }
    return total;
  }
  function calcInss(base) {
    var faixas = [[1621.00, 0.075], [2902.84, 0.09], [4354.27, 0.12], [8475.55, 0.14]];
    var ant = 0;
    var total = 0;
    var i = 0;
    for (i = 0; i !== faixas.length; i++) {
      if (base > ant) { total = total + (Math.min(base, faixas[i][0]) - ant) * faixas[i][1]; }
      ant = faixas[i][0];
    }
    return r2(total);
  }
  function calcIrrf(bruto, descInss, dep) {
    if (0 >= bruto) { return 0; }
    var legal = descInss + dep * 189.59;
    var ded = legal > 607.20 ? legal : 607.20;
    var base = bruto - ded;
    if (0 >= base) { return 0; }
    var t = [[2428.80, 0, 0], [2826.65, 0.075, 182.16], [3751.05, 0.15, 394.16], [4664.68, 0.225, 675.49], [Infinity, 0.275, 908.73]];
    var i = 0;
    while (base > t[i][0]) { i = i + 1; }
    var imp = base * t[i][1] - t[i][2];
    if (0 >= imp) { return 0; }
    var red = 0;
    if (5000 >= bruto) {
      red = Math.min(imp, 312.89);
    } else if (7350 >= bruto) {
      red = Math.max(0, 978.62 - 0.133145 * bruto);
    }
    return r2(Math.max(0, imp - red));
  }
  function limparResultado() {
    while (resultado.firstChild) { resultado.removeChild(resultado.firstChild); }
  }
  function erro(msg) {
    caixa.style.borderColor = '#fca5a5';
    caixa.style.background = '#fef2f2';
    resultado.style.color = '#b91c1c';
    limparResultado();
    resultado.textContent = msg;
  }
  function titulo(pai, texto) {
    var t = document.createElement('div');
    t.style.cssText = 'margin-top:14px;font-weight:700;color:#3730a3;';
    t.textContent = texto;
    pai.appendChild(t);
  }
  function linha(pai, rotulo, valor, destaque) {
    var l = document.createElement('div');
    l.style.cssText = 'display:flex;justify-content:space-between;gap:12px;padding:6px 0;border-bottom:1px solid #e2e8f0;font-size:0.95rem;' + (destaque ? 'font-weight:700;color:#166534;' : 'color:#334155;');
    var a = document.createElement('span');
    a.textContent = rotulo;
    var b = document.createElement('span');
    b.style.cssText = 'white-space:nowrap;';
    b.textContent = valor;
    l.appendChild(a);
    l.appendChild(b);
    pai.appendChild(l);
  }
  function atualizarAviso() {
    var mot = elMotivo.value;
    elAviso.disabled = (mot === 'justa' || mot === 'experiencia');
  }
  function calcular() {
    var sal = numero(elSalario.value);
    if (isNaN(sal) || 0 >= sal) { erro('informe um salário base válido, maior que zero.'); return; }
    var dep = 0;
    if (String(elDep.value).trim() !== '') {
      dep = numero(elDep.value);
      if (isNaN(dep) || 0 > dep || dep !== Math.floor(dep)) { erro('informe um número inteiro de dependentes (0 ou mais).'); return; }
    }
    var ini = lerData(elInicio.value);
    var fim = lerData(elFim.value);
    if (ini === null || fim === null) { erro('informe as datas de início e de fim do contrato.'); return; }
    if (utc(ini) > utc(fim)) { erro('a data de fim deve ser igual ou posterior à data de início.'); return; }
    var motivo = elMotivo.value;
    var cumprido = (elAviso.value === 'sim');
    var anos = anosCompletos(ini, fim);
    if (elFerias.value === 'sim' && 1 > anos) { erro('férias vencidas exigem pelo menos 1 ano completo de contrato.'); return; }
    var ref = fim;
    var diasAviso = 0;
    var avisoInd = 0;
    var descAviso = 0;
    if (motivo === 'semjusta') {
      diasAviso = 30 + 3 * Math.min(anos, 20);
      if (!cumprido) {
        avisoInd = r2(sal / 30 * diasAviso);
        ref = somarDias(fim, diasAviso);
      }
    }
    if (motivo === 'pedido' && !cumprido) { descAviso = r2(sal); }
    var diasSaldo = Math.min(fim.d, 30);
    var saldo = r2(sal / 30 * diasSaldo);
    var m13 = 0;
    var v13 = 0;
    var mf = 0;
    var vFerProp = 0;
    var tFerProp = 0;
    if (motivo !== 'justa') {
      var ini13 = (ini.y === ref.y) ? ini : { y: ref.y, m: 1, d: 1 };
      m13 = Math.min(12, meses(ini13, ref));
      v13 = r2(sal / 12 * m13);
      var anosRef = anosCompletos(ini, ref);
      var inicioPeriodo = { y: ini.y + anosRef, m: ini.m, d: ini.d };
      mf = Math.min(12, meses(inicioPeriodo, ref));
      vFerProp = r2(sal / 12 * mf);
      tFerProp = r2(vFerProp / 3);
    }
    var vFerVenc = 0;
    var tFerVenc = 0;
    if (elFerias.value === 'sim') {
      vFerVenc = r2(sal);
      tFerVenc = r2(sal / 3);
    }
    var inssSaldo = calcInss(saldo);
    var irrfSaldo = calcIrrf(saldo, inssSaldo, dep);
    var inss13 = calcInss(v13);
    var irrf13 = calcIrrf(v13, inss13, dep);
    var totalProv = saldo + avisoInd + v13 + vFerProp + tFerProp + vFerVenc + tFerVenc;
    var totalDesc = inssSaldo + irrfSaldo + inss13 + irrf13 + descAviso;
    var liquido = r2(totalProv - totalDesc);
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    limparResultado();
    titulo(resultado, 'Verbas a receber');
    linha(resultado, 'Saldo de salário (' + diasSaldo + ' dias)', brl(saldo), false);
    if (avisoInd > 0) { linha(resultado, 'Aviso prévio indenizado (' + diasAviso + ' dias)', brl(avisoInd), false); }
    if (motivo !== 'justa') {
      linha(resultado, '13º salário proporcional (' + m13 + '/12)', brl(v13), false);
      linha(resultado, 'Férias proporcionais (' + mf + '/12)', brl(vFerProp), false);
      linha(resultado, '1/3 sobre férias proporcionais', brl(tFerProp), false);
    }
    if (vFerVenc > 0) {
      linha(resultado, 'Férias vencidas', brl(vFerVenc), false);
      linha(resultado, '1/3 sobre férias vencidas', brl(tFerVenc), false);
    }
    linha(resultado, 'Total bruto', brl(r2(totalProv)), true);
    titulo(resultado, 'Descontos');
    linha(resultado, 'INSS sobre saldo de salário', brl(inssSaldo), false);
    linha(resultado, 'IRRF sobre saldo de salário', brl(irrfSaldo), false);
    if (v13 > 0) {
      linha(resultado, 'INSS sobre 13º salário', brl(inss13), false);
      linha(resultado, 'IRRF sobre 13º salário', brl(irrf13), false);
    }
    if (descAviso > 0) { linha(resultado, 'Aviso prévio não cumprido', brl(descAviso), false); }
    linha(resultado, 'Total de descontos', brl(r2(totalDesc)), true);
    titulo(resultado, 'Valor líquido estimado');
    linha(resultado, 'Total líquido da rescisão', brl(liquido), true);
    var nota = document.createElement('div');
    nota.style.cssText = 'margin-top:12px;font-size:0.8rem;color:#475569;line-height:1.5;';
    nota.textContent = 'Não inclui o saque do FGTS nem a multa de 40%, que dependem do saldo real da conta. Valores estimados com as tabelas de INSS e IRRF de 2026.';
    resultado.appendChild(nota);
  }
  function limpar() {
    elSalario.value = '';
    elDep.value = '';
    elInicio.value = '';
    elFim.value = '';
    elMotivo.value = 'semjusta';
    elFerias.value = 'nao';
    elAviso.value = 'sim';
    atualizarAviso();
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    resultado.style.color = '#64748b';
    limparResultado();
    resultado.textContent = TEXTO_INICIAL;
    elSalario.focus();
  }
  document.getElementById('resc-calcular').addEventListener('click', calcular);
  document.getElementById('resc-limpar').addEventListener('click', limpar);
  elMotivo.addEventListener('change', atualizarAviso);
  [elSalario, elDep, elInicio, elFim, elMotivo, elFerias, elAviso].forEach(function (el) {
    el.addEventListener('focus', function () { el.style.borderColor = '#6366f1'; });
    el.addEventListener('blur', function () { el.style.borderColor = '#c7d2fe'; });
  });
  [elSalario, elDep].forEach(function (el) {
    el.addEventListener('keydown', function (e) { if (e.key === 'Enter') { calcular(); } });
  });
  atualizarAviso();
})();
</script>

## Como usar a calculadora

1. Digite o **Salário base** mensal bruto (por exemplo, `3000,00` ou `3000.00`).
2. Informe o **Nº de dependentes** para fins de Imposto de Renda (deixe em branco ou `0` se não houver).
3. Escolha a data de **Início do contrato de trabalho** e a data de **Fim do contrato de trabalho**.
4. Selecione o **Motivo da rescisão contratual**.
5. Indique se você possui **férias vencidas** e se o **aviso prévio foi cumprido**.
6. Clique em **Calcular Rescisão** (ou pressione Enter nos campos de texto) para ver as verbas, os descontos e o valor líquido estimado.
7. Use o botão **Limpar** para apagar os dados e fazer um novo cálculo.

O campo de aviso prévio só é considerado na dispensa sem justa causa e no pedido de demissão. Nos demais motivos ele fica desativado.

## Entendendo os termos

- **Rescisão de contrato:** encerramento do vínculo de trabalho, com o pagamento das verbas que o trabalhador tem direito a receber.
- **Salário base:** salário mensal bruto, antes dos descontos, usado como base de todos os cálculos.
- **Dependentes:** pessoas que podem ser deduzidas do Imposto de Renda, como filhos e cônjuge. Cada dependente reduz a base de cálculo do imposto.
- **Pedido de demissão:** o trabalhador decide sair. Recebe saldo de salário, 13º e férias proporcionais, além de férias vencidas, se houver.
- **Dispensa sem justa causa:** a empresa dispensa o trabalhador sem falta grave. Recebe todas as verbas, incluindo o aviso prévio.
- **Dispensa com justa causa:** a empresa dispensa por falta grave do trabalhador. Recebe apenas o saldo de salário e as férias vencidas, se houver.
- **Fim do contrato de experiência:** o contrato por prazo determinado chega ao fim na data prevista, sem aviso prévio.
- **Saldo de salário:** salário dos dias trabalhados no último mês, ainda não pagos.
- **Aviso prévio:** comunicação antecipada do desligamento. É de 30 dias, mais 3 dias por ano completo de trabalho, até o máximo de 90 dias.
- **Aviso prévio cumprido:** o trabalhador continua trabalhando durante o período do aviso. Se a empresa dispensa e o aviso não é cumprido, ele é pago como indenização. Se o trabalhador pede demissão e não cumpre, o valor de 30 dias é descontado.
- **13º salário proporcional:** fração de 1/12 do salário por mês trabalhado no ano. Meses com 15 dias ou mais de trabalho contam como mês inteiro.
- **Férias vencidas:** período de 12 meses de trabalho completo cujas férias ainda não foram gozadas. É pago o salário mais 1/3.
- **Férias proporcionais:** fração de 1/12 por mês trabalhado desde o último período de férias completo.
- **1/3 constitucional:** adicional de um terço sobre o valor das férias, garantido pela Constituição.
- **INSS:** contribuição previdenciária descontada do saldo de salário e do 13º salário, com alíquotas progressivas.
- **IRRF:** Imposto de Renda retido na fonte, calculado sobre o saldo de salário e o 13º salário, considerando os dependentes.
- **FGTS e multa de 40%:** o saldo do FGTS e a multa pela dispensa sem justa causa dependem do valor real depositado na conta e por isso não entram neste cálculo.