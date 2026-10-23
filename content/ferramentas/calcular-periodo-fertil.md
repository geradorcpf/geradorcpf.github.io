---
title: "Calcular Período Fértil"
seoTitle: "Calcular Período Fértil: online e grátis"
description: "Calcular Período Fértil: estime seu período fértil a partir do ciclo. Grátis e online, sem cadastro."
summary: "Estime seu período fértil a partir do ciclo."
date: 2026-10-23
draft: false
category: "saude"
tags: ["gravidez", "ciclo menstrual", "saúde", "datas"]
keywords: ["calcular período fértil", "calcular período fértil online", "gravidez", "ciclo menstrual", "saúde"]
---
<!--sudah dikerjakan-->

Basta informar o primeiro dia da sua última menstruação e a duração média do seu ciclo, depois clicar em **Calcular**.

<div id="calc-fertil" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🌸 Calculadora do Período Fértil</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Informe os dados do seu ciclo e veja os dias férteis.</p>
<label for="fer-dia" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Primeiro dia da última menstruação</label>
<div style="display:flex;gap:10px;flex-wrap:wrap;margin-bottom:16px;">
<select id="fer-dia" aria-label="Dia" style="flex:1;min-width:80px;padding:12px 14px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;"></select>
<select id="fer-mes" aria-label="Mês" style="flex:2;min-width:130px;padding:12px 14px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;"></select>
<select id="fer-ano" aria-label="Ano" style="flex:1;min-width:90px;padding:12px 14px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;"></select>
</div>
<label for="fer-ciclo" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Duração média do seu ciclo</label>
<select id="fer-ciclo" style="width:100%;padding:12px 14px;margin-bottom:20px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;"></select>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="fer-calcular" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Calcular</button>
<button type="button" id="fer-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="fer-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Dias Férteis:</strong> <span id="fer-resultado">preencha os campos e clique em "Calcular".</span></div>
</div>
<script>
(function () {
var dia = document.getElementById('fer-dia');
var mes = document.getElementById('fer-mes');
var ano = document.getElementById('fer-ano');
var ciclo = document.getElementById('fer-ciclo');
var resultado = document.getElementById('fer-resultado');
var caixa = document.getElementById('fer-resposta');
var nomesMeses = ['Janeiro', 'Fevereiro', 'Março', 'Abril', 'Maio', 'Junho', 'Julho', 'Agosto', 'Setembro', 'Outubro', 'Novembro', 'Dezembro'];
var hoje = new Date();
var anoAtual = hoje.getFullYear();
var DIA_MS = 86400000;
function opcao(sel, valor, texto) {
var o = document.createElement('option');
o.value = String(valor);
o.textContent = String(texto);
sel.appendChild(o);
}
for (var d = 1; 32 > d; d++) { opcao(dia, d, d); }
for (var m = 0; 12 > m; m++) { opcao(mes, m + 1, nomesMeses[m]); }
for (var y = anoAtual - 1; anoAtual + 2 > y; y++) { opcao(ano, y, y); }
for (var c = 20; 41 > c; c++) { opcao(ciclo, c, c + ' dias'); }
function padrao() {
dia.value = String(hoje.getDate());
mes.value = String(hoje.getMonth() + 1);
ano.value = String(anoAtual);
ciclo.value = '28';
}
function somarDias(data, n) { return new Date(data.getTime() + n * DIA_MS); }
function dataCurta(data) {
return data.toLocaleDateString('pt-BR', { day: '2-digit', month: '2-digit', year: 'numeric', timeZone: 'UTC' });
}
function dataComSemana(data) {
return data.toLocaleDateString('pt-BR', { weekday: 'short', day: '2-digit', month: '2-digit', year: 'numeric', timeZone: 'UTC' });
}
function esvaziar() {
while (resultado.firstChild) { resultado.removeChild(resultado.firstChild); }
}
function erro(msg) {
caixa.style.borderColor = '#fca5a5';
caixa.style.background = '#fef2f2';
resultado.style.color = '#b91c1c';
esvaziar();
resultado.textContent = msg;
}
function linha(rotulo, valor, destaque, cor) {
var bloco = document.createElement('div');
bloco.style.marginBottom = '8px';
var r = document.createElement('strong');
r.textContent = rotulo + ' ';
bloco.appendChild(r);
var v = document.createElement('span');
v.textContent = valor;
if (destaque) { v.style.fontWeight = '700'; v.style.fontSize = '1.1rem'; }
if (cor) { v.style.color = cor; }
bloco.appendChild(v);
resultado.appendChild(bloco);
}
function calcular() {
var diaN = Number(dia.value);
var mesN = Number(mes.value);
var anoN = Number(ano.value);
var cicloN = Number(ciclo.value);
var inicio = new Date(Date.UTC(anoN, mesN - 1, diaN));
if (inicio.getUTCMonth() !== mesN - 1 || inicio.getUTCDate() !== diaN) {
erro('essa data não existe. Verifique o dia e o mês escolhidos.');
return;
}
var ovulacao = somarDias(inicio, cicloN - 14);
var inicioFertil = somarDias(ovulacao, -5);
var fimFertil = somarDias(ovulacao, 1);
var proxima = somarDias(inicio, cicloN);
caixa.style.borderColor = '#86efac';
caixa.style.background = '#f0fdf4';
resultado.style.color = '#166534';
esvaziar();
linha('Período fértil:', dataCurta(inicioFertil) + ' a ' + dataCurta(fimFertil), true);
linha('Provável ovulação:', dataComSemana(ovulacao), false);
linha('Próxima menstruação:', dataComSemana(proxima), false);
var titulo = document.createElement('div');
titulo.style.margin = '12px 0 6px';
titulo.style.fontWeight = '700';
titulo.textContent = 'Dias férteis:';
resultado.appendChild(titulo);
for (var k = 0; 7 > k; k++) {
var dataDia = somarDias(inicioFertil, k);
var ehOvulacao = (k === 5);
var texto = dataComSemana(dataDia) + (ehOvulacao ? ' (ovulação)' : '');
var item = document.createElement('div');
item.style.padding = '4px 0';
item.style.fontWeight = ehOvulacao ? '700' : '400';
item.textContent = texto;
resultado.appendChild(item);
}
var aviso = document.createElement('div');
aviso.style.marginTop = '10px';
aviso.style.fontSize = '0.85rem';
aviso.style.color = '#475569';
aviso.textContent = 'Estimativa baseada em ciclo regular. Não substitui orientação médica nem serve como método contraceptivo.';
resultado.appendChild(aviso);
}
function limpar() {
padrao();
caixa.style.borderColor = '#c7d2fe';
caixa.style.background = '#ffffff';
resultado.style.color = '#64748b';
esvaziar();
resultado.textContent = 'preencha os campos e clique em "Calcular".';
}
padrao();
document.getElementById('fer-calcular').addEventListener('click', calcular);
document.getElementById('fer-limpar').addEventListener('click', limpar);
[dia, mes, ano, ciclo].forEach(function (el) {
el.addEventListener('focus', function () { el.style.borderColor = '#6366f1'; });
el.addEventListener('blur', function () { el.style.borderColor = '#c7d2fe'; });
});
})();
</script>

## Como usar a calculadora

1. Escolha o **dia**, o **mês** e o **ano** do primeiro dia da sua última menstruação.
2. Selecione a **duração média do seu ciclo** (de 20 a 40 dias).
3. Clique em **Calcular** para ver o período fértil, a provável data de ovulação e a previsão da próxima menstruação.
4. Use o botão **Limpar** para voltar aos valores iniciais e fazer um novo cálculo.

Se você não sabe a duração exata do seu ciclo, anote o início de algumas menstruações seguidas e calcule a média de dias entre elas. O padrão mais comum é de 28 dias.

## Entendendo os termos

- **Ciclo menstrual:** intervalo entre o primeiro dia de uma menstruação e o dia anterior ao início da próxima.
- **Primeiro dia da última menstruação:** data em que o sangramento começou no ciclo mais recente. É a referência para todos os cálculos.
- **Duração do ciclo:** número de dias de um ciclo completo. Em geral varia entre 21 e 35 dias.
- **Ovulação:** liberação do óvulo pelo ovário, que costuma ocorrer cerca de 14 dias antes da próxima menstruação.
- **Período fértil:** conjunto de dias em que a chance de engravidar é maior, por causa da ovulação e da sobrevida dos espermatozoides no organismo.
- **Próxima menstruação:** data prevista para o início do próximo ciclo, somando a duração do ciclo ao primeiro dia da última menstruação.

## Como o cálculo é feito

A calculadora estima a ovulação e, a partir dela, define a janela fértil:

- **Ovulação = primeiro dia da última menstruação + (duração do ciclo − 14 dias)**
- **Período fértil = de 5 dias antes até 1 dia depois da ovulação**
- **Próxima menstruação = primeiro dia da última menstruação + duração do ciclo**

## Exemplo resolvido

Uma mulher com ciclo de 28 dias teve o primeiro dia da última menstruação em 01/11/2026. Quando é o seu período fértil?

1. Calcule a ovulação: 28 − 14 = 14 dias após 01/11, ou seja, 15/11/2026.
2. Defina o período fértil: 5 dias antes (10/11) até 1 dia depois (16/11).
3. Calcule a próxima menstruação: 28 dias após 01/11, ou seja, 29/11/2026.

**Resposta:** o período fértil vai de **10/11/2026 a 16/11/2026**, com ovulação provável em 15/11/2026.

> Os resultados são estimativas para ciclos regulares e não substituem a avaliação de um profissional de saúde.