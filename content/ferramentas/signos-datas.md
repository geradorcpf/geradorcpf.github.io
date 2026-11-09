---
title: "Signos e Datas"
seoTitle: "Signos e Datas"
description: "Signos e Datas: veja o signo de cada data e as datas de cada signo. Grátis e online, sem cadastro."
summary: "Veja o signo de cada data e as datas de cada signo."
date: 2026-11-09
draft: false
category: "datas"
tags: ["signos", "astrologia", "datas"]
keywords: ["signos e datas", "signos e datas online", "signos", "astrologia", "datas"]
---

Basta escolher o dia e o mês de nascimento abaixo e depois clicar em **Descobrir Signo**.

<div id="calc-signos" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">✨ Signos e Datas</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Indique a data de nascimento e veja o signo na hora.</p>
<div style="display:flex;gap:10px;flex-wrap:wrap;margin-bottom:20px;">
<div style="flex:1;min-width:110px;">
<label for="sig-dia" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Dia</label>
<select id="sig-dia" style="width:100%;padding:12px 14px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;"></select>
</div>
<div style="flex:2;min-width:160px;">
<label for="sig-mes" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Mês</label>
<select id="sig-mes" style="width:100%;padding:12px 14px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;"></select>
</div>
</div>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="sig-calcular" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Descobrir Signo</button>
<button type="button" id="sig-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="sig-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="sig-resultado">escolha o dia e o mês e clique em "Descobrir Signo".</span></div>
</div>
<script>
(function () {
  var selDia = document.getElementById('sig-dia');
  var selMes = document.getElementById('sig-mes');
  var resultado = document.getElementById('sig-resultado');
  var caixa = document.getElementById('sig-resposta');
  var meses = ['Janeiro', 'Fevereiro', 'Março', 'Abril', 'Maio', 'Junho', 'Julho', 'Agosto', 'Setembro', 'Outubro', 'Novembro', 'Dezembro'];
  var diasNoMes = [31, 29, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31];
  var signos = [
    { nome: 'Áries', simbolo: '♈', ini: 321, fim: 420, periodo: '21 de março a 20 de abril' },
    { nome: 'Touro', simbolo: '♉', ini: 421, fim: 520, periodo: '21 de abril a 20 de maio' },
    { nome: 'Gêmeos', simbolo: '♊', ini: 521, fim: 620, periodo: '21 de maio a 20 de junho' },
    { nome: 'Câncer', simbolo: '♋', ini: 621, fim: 721, periodo: '21 de junho a 21 de julho' },
    { nome: 'Leão', simbolo: '♌', ini: 722, fim: 822, periodo: '22 de julho a 22 de agosto' },
    { nome: 'Virgem', simbolo: '♍', ini: 823, fim: 922, periodo: '23 de agosto a 22 de setembro' },
    { nome: 'Libra', simbolo: '♎', ini: 923, fim: 1022, periodo: '23 de setembro a 22 de outubro' },
    { nome: 'Escorpião', simbolo: '♏', ini: 1023, fim: 1121, periodo: '23 de outubro a 21 de novembro' },
    { nome: 'Sagitário', simbolo: '♐', ini: 1122, fim: 1221, periodo: '22 de novembro a 21 de dezembro' },
    { nome: 'Capricórnio', simbolo: '♑', ini: 1222, fim: 120, periodo: '22 de dezembro a 20 de janeiro' },
    { nome: 'Aquário', simbolo: '♒', ini: 121, fim: 219, periodo: '21 de janeiro a 19 de fevereiro' },
    { nome: 'Peixes', simbolo: '♓', ini: 220, fim: 320, periodo: '20 de fevereiro a 20 de março' }
  ];
  var i, op;
  op = document.createElement('option');
  op.value = '';
  op.textContent = 'Dia';
  selDia.appendChild(op);
  for (i = 1; i !== 32; i++) {
    op = document.createElement('option');
    op.value = String(i);
    op.textContent = String(i);
    selDia.appendChild(op);
  }
  op = document.createElement('option');
  op.value = '';
  op.textContent = 'Mês';
  selMes.appendChild(op);
  for (i = 0; i !== 12; i++) {
    op = document.createElement('option');
    op.value = String(i + 1);
    op.textContent = meses[i];
    selMes.appendChild(op);
  }
  function erro(msg) {
    caixa.style.borderColor = '#fca5a5';
    caixa.style.background = '#fef2f2';
    resultado.style.color = '#b91c1c';
    resultado.textContent = msg;
  }
  function achar(valor) {
    var k, s;
    for (k = 0; k !== signos.length; k++) {
      s = signos[k];
      if (s.ini > s.fim) {
        if (valor >= s.ini) { return s; }
        if (s.fim >= valor) { return s; }
      } else {
        if (valor >= s.ini) {
          if (s.fim >= valor) { return s; }
        }
      }
    }
    return null;
  }
  function calcular() {
    var d = Number(selDia.value);
    var m = Number(selMes.value);
    if (!d || !m) { erro('escolha o dia e o mês de nascimento.'); return; }
    if (d > diasNoMes[m - 1]) { erro('essa data não existe: ' + meses[m - 1] + ' não tem dia ' + d + '.'); return; }
    var s = achar(m * 100 + d);
    if (!s) { erro('não foi possível identificar o signo.'); return; }
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    while (resultado.firstChild) { resultado.removeChild(resultado.firstChild); }
    resultado.appendChild(document.createTextNode('Quem nasceu em ' + d + ' de ' + meses[m - 1].toLowerCase() + ' é do signo de '));
    var forte = document.createElement('strong');
    forte.style.fontSize = '1.2rem';
    forte.textContent = s.simbolo + ' ' + s.nome;
    resultado.appendChild(forte);
    resultado.appendChild(document.createElement('br'));
    var pequeno = document.createElement('small');
    pequeno.style.color = '#475569';
    pequeno.textContent = 'Período de ' + s.nome + ': ' + s.periodo;
    resultado.appendChild(pequeno);
  }
  function limpar() {
    selDia.value = '';
    selMes.value = '';
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    resultado.style.color = '#64748b';
    resultado.textContent = 'escolha o dia e o mês e clique em "Descobrir Signo".';
    selDia.focus();
  }
  document.getElementById('sig-calcular').addEventListener('click', calcular);
  document.getElementById('sig-limpar').addEventListener('click', limpar);
  [selDia, selMes].forEach(function (el) {
    el.addEventListener('keydown', function (e) { if (e.key === 'Enter') { calcular(); } });
    el.addEventListener('focus', function () { el.style.borderColor = '#6366f1'; });
    el.addEventListener('blur', function () { el.style.borderColor = '#c7d2fe'; });
  });
})();
</script>

## Como usar a ferramenta

1. Escolha o **dia** de nascimento no primeiro campo.
2. Escolha o **mês** de nascimento no segundo campo.
3. Clique em **Descobrir Signo** (ou pressione Enter) para ver o signo e o período dele.
4. Use o botão **Limpar** para apagar a seleção e consultar outra data.

O ano de nascimento não é necessário, porque as datas dos signos são as mesmas todos os anos. Datas que não existem, como 31 de abril ou 30 de fevereiro, são avisadas na resposta.

## Entendendo os termos

- **Signo:** cada uma das 12 divisões do zodíaco. O signo de uma pessoa é definido pela data de nascimento.
- **Zodíaco:** faixa imaginária do céu dividida em 12 partes, cada uma associada a um signo.
- **Astrologia:** estudo que relaciona a posição dos astros com a personalidade e os acontecimentos da vida das pessoas.
- **Signo solar:** o signo em que o Sol estava no momento do nascimento. É o signo mais conhecido e o que esta ferramenta mostra.
- **Período:** intervalo de datas em que cada signo vale, por exemplo, de 21 de março a 20 de abril para Áries.
- **Cúspide:** dia de transição entre dois signos. Quem nasce nessa data pode ter características dos dois.
- **Elemento:** grupo de três signos que compartilham a mesma natureza: fogo, terra, ar ou água.
- **Data de nascimento:** dia e mês em que a pessoa nasceu, usados para descobrir o signo.

## Datas dos signos

| Signo | Período |
|---|---|
| ♈ Áries | 21 de março a 20 de abril |
| ♉ Touro | 21 de abril a 20 de maio |
| ♊ Gêmeos | 21 de maio a 20 de junho |
| ♋ Câncer | 21 de junho a 21 de julho |
| ♌ Leão | 22 de julho a 22 de agosto |
| ♍ Virgem | 23 de agosto a 22 de setembro |
| ♎ Libra | 23 de setembro a 22 de outubro |
| ♏ Escorpião | 23 de outubro a 21 de novembro |
| ♐ Sagitário | 22 de novembro a 21 de dezembro |
| ♑ Capricórnio | 22 de dezembro a 20 de janeiro |
| ♒ Aquário | 21 de janeiro a 19 de fevereiro |
| ♓ Peixes | 20 de fevereiro a 20 de março |

## Exemplo

Uma pessoa nasceu em 15 de agosto. Qual é o seu signo?

1. Escolha o dia **15** e o mês **Agosto**.
2. Clique em **Descobrir Signo**.
3. Agosto de 15 está entre 22 de julho e 22 de agosto.

**Resposta:** o signo é **Leão** ♌.