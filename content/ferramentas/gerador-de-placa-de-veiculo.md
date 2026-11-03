---
title: "Gerador de Placas de Automóveis"
seoTitle: "Gerador de Placas de Automóveis"
description: "Gerador de Placas de Automóveis: gere placas no padrão antigo e no Mercosul. Grátis e online, sem cadastro."
summary: "Gere placas no padrão antigo e no Mercosul."
date: 2026-11-03
draft: false
category: "documentos"
tags: ["placas", "veículos", "gerador", "dados de teste", "documentos"]
keywords: ["gerador de placas de automóveis", "gerador de placas de automóveis online", "placas", "veículos", "gerador"]
---

Basta escolher o padrão e o estado abaixo e depois clicar em **Gerar Placa**.

<div id="gerador-placa" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🚗 Gerador de Placas de Automóveis</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Escolha as opções e gere uma placa na hora.</p>
<label for="placa-padrao" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Padrão da Placa</label>
<select id="placa-padrao" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<option value="antigo">Padrão antigo (AAA-1234)</option>
<option value="mercosul">Mercosul (AAA1B23)</option>
</select>
<label for="placa-pontuacao" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Gerar com pontuação (hífen)?</label>
<select id="placa-pontuacao" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<option value="sim">Sim</option>
<option value="nao">Não</option>
</select>
<label for="placa-estado" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Estado de Origem da Placa</label>
<select id="placa-estado" style="width:100%;padding:12px 14px;margin-bottom:20px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<option value="">Indiferente</option>
<option value="AC">AC</option>
<option value="AL">AL</option>
<option value="AM">AM</option>
<option value="AP">AP</option>
<option value="BA">BA</option>
<option value="CE">CE</option>
<option value="DF">DF</option>
<option value="ES">ES</option>
<option value="GO">GO</option>
<option value="MA">MA</option>
<option value="MG">MG</option>
<option value="MS">MS</option>
<option value="MT">MT</option>
<option value="PA">PA</option>
<option value="PB">PB</option>
<option value="PE">PE</option>
<option value="PI">PI</option>
<option value="PR">PR</option>
<option value="RJ">RJ</option>
<option value="RN">RN</option>
<option value="RS">RS</option>
<option value="RO">RO</option>
<option value="RR">RR</option>
<option value="SC">SC</option>
<option value="SE">SE</option>
<option value="SP">SP</option>
<option value="TO">TO</option>
</select>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="placa-gerar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Gerar Placa</button>
<button type="button" id="placa-copiar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Copiar</button>
<button type="button" id="placa-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="placa-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="placa-resultado">escolha as opções e clique em "Gerar Placa".</span></div>
</div>
<script>
(function () {
  var padrao = document.getElementById('placa-padrao');
  var pontuacao = document.getElementById('placa-pontuacao');
  var estado = document.getElementById('placa-estado');
  var resultado = document.getElementById('placa-resultado');
  var caixa = document.getElementById('placa-resposta');
  var btnCopiar = document.getElementById('placa-copiar');
  var textoInicial = 'escolha as opções e clique em "Gerar Placa".';
  var ultima = '';
  var FAIXAS = [
    ['PR', 'AAA', 'BEZ'], ['SP', 'BFA', 'GKI'], ['MG', 'GKJ', 'HOK'], ['MA', 'HOL', 'HQE'],
    ['MS', 'HQF', 'HTW'], ['CE', 'HTX', 'HZA'], ['SE', 'HZB', 'IAP'], ['RS', 'IAQ', 'JDO'],
    ['DF', 'JDP', 'JKR'], ['BA', 'JKS', 'JSZ'], ['PA', 'JTA', 'JWE'], ['AM', 'JWF', 'JXY'],
    ['MT', 'JXZ', 'KAU'], ['GO', 'KAV', 'KFC'], ['GO', 'NFC', 'NGZ'], ['PE', 'KFD', 'KME'],
    ['RJ', 'KMF', 'LVE'], ['PI', 'LVF', 'LWQ'], ['SC', 'LWR', 'MMM'], ['PB', 'MMN', 'MOW'],
    ['ES', 'MOX', 'MTZ'], ['AL', 'MUA', 'MVK'], ['TO', 'MVL', 'MXG'], ['RN', 'MXH', 'MZM'],
    ['AC', 'MZN', 'NAG'], ['RR', 'NAH', 'NBA'], ['RO', 'NBB', 'NEH'], ['AP', 'NEI', 'NFB']
  ];
  function paraNumero(letras) {
    return letras.split('').reduce(function (acc, c) { return acc * 26 + c.charCodeAt(0) - 65; }, 0);
  }
  function letra(n) { return String.fromCharCode(65 + n); }
  function paraLetras(n) {
    return letra(Math.floor(n / 676)) + letra(Math.floor(n / 26) % 26) + letra(n % 26);
  }
  function sorteio(n) { return Math.floor(Math.random() * n); }
  var LISTA = FAIXAS.map(function (f) {
    return { uf: f[0], ini: paraNumero(f[1]), fim: paraNumero(f[2]) };
  });
  function sincronizar() {
    var mercosul = padrao.value === 'mercosul';
    pontuacao.disabled = mercosul;
    pontuacao.style.opacity = mercosul ? '0.5' : '1';
  }
  function gerar() {
    var uf = estado.value;
    var faixas = LISTA.filter(function (f) { return uf === '' || f.uf === uf; });
    var total = faixas.reduce(function (soma, f) { return soma + f.fim - f.ini + 1; }, 0);
    var r = sorteio(total);
    var achada = null;
    faixas.forEach(function (f) {
      var tam = f.fim - f.ini + 1;
      if (achada === null && r === Math.min(r, tam - 1)) {
        achada = { uf: f.uf, letras: paraLetras(f.ini + r) };
      }
      r = r - tam;
    });
    var mercosul = padrao.value === 'mercosul';
    var placa;
    if (mercosul) {
      placa = achada.letras + String(sorteio(10)) + letra(sorteio(10)) + ('0' + sorteio(100)).slice(-2);
    } else {
      placa = achada.letras + (pontuacao.value === 'sim' ? '-' : '') + ('000' + (sorteio(9999) + 1)).slice(-4);
    }
    ultima = placa;
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    resultado.textContent = '';
    resultado.appendChild(document.createTextNode('a placa gerada é '));
    var forte = document.createElement('strong');
    forte.style.fontSize = '1.4rem';
    forte.style.letterSpacing = '2px';
    forte.style.fontFamily = 'ui-monospace, Menlo, Consolas, monospace';
    forte.textContent = placa;
    resultado.appendChild(forte);
    resultado.appendChild(document.createElement('br'));
    var detalhe = document.createElement('small');
    detalhe.style.color = '#475569';
    detalhe.textContent = 'Padrão ' + (mercosul ? 'Mercosul' : 'antigo') + ' | Estado de origem: ' + achada.uf;
    resultado.appendChild(detalhe);
  }
  function avisoCopiado() {
    btnCopiar.textContent = 'Copiado!';
    setTimeout(function () { btnCopiar.textContent = 'Copiar'; }, 1500);
  }
  function copiarAlternativo() {
    var campo = document.createElement('textarea');
    campo.value = ultima;
    campo.style.position = 'fixed';
    campo.style.opacity = '0';
    document.body.appendChild(campo);
    campo.select();
    try {
      document.execCommand('copy');
      avisoCopiado();
    } catch (e) {
      btnCopiar.textContent = 'Copiar';
    }
    document.body.removeChild(campo);
  }
  function copiar() {
    if (ultima === '') { return; }
    try {
      navigator.clipboard.writeText(ultima).then(avisoCopiado, copiarAlternativo);
    } catch (e) {
      copiarAlternativo();
    }
  }
  function limpar() {
    padrao.value = 'antigo';
    pontuacao.value = 'sim';
    estado.value = '';
    ultima = '';
    sincronizar();
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    resultado.style.color = '#64748b';
    resultado.textContent = textoInicial;
  }
  document.getElementById('placa-gerar').addEventListener('click', gerar);
  btnCopiar.addEventListener('click', copiar);
  document.getElementById('placa-limpar').addEventListener('click', limpar);
  padrao.addEventListener('change', sincronizar);
  [padrao, pontuacao, estado].forEach(function (el) {
    el.addEventListener('focus', function () { el.style.borderColor = '#6366f1'; });
    el.addEventListener('blur', function () { el.style.borderColor = '#c7d2fe'; });
  });
  sincronizar();
})();
</script>

## Como usar o gerador

1. Escolha o **Padrão da Placa**: padrão antigo (AAA-1234) ou Mercosul (AAA1B23).
2. No padrão antigo, defina se a placa deve sair **com pontuação** (hífen) ou sem ela. No Mercosul essa opção fica desativada, pois a placa não leva hífen.
3. Selecione o **Estado de Origem** ou deixe em **Indiferente** para um estado sorteado.
4. Clique em **Gerar Placa** para ver o resultado. Clique de novo para gerar outra.
5. Use **Copiar** para levar a placa para a área de transferência e **Limpar** para voltar às opções iniciais.

As placas são geradas de forma aleatória e respeitam apenas o formato e as faixas de letras de cada estado. Elas servem para testes de software e não correspondem necessariamente a veículos reais.

## Entendendo os termos

- **Placa de veículo:** identificação alfanumérica única de um veículo, exibida na frente e na traseira.
- **Padrão antigo:** formato em uso desde 1990, com três letras e quatro números (AAA-1234).
- **Padrão Mercosul:** formato com três letras, um número, uma letra e dois números (AAA1B23), adotado desde 2018.
- **Pontuação:** hífen que separa as letras dos números no padrão antigo (ABC-1234).
- **Estado de origem:** unidade da federação onde o veículo foi emplacado pela primeira vez.
- **Faixa de letras:** sequência de três letras reservada a cada estado, como BFA a GKI para São Paulo.
- **Indiferente:** opção que sorteia qualquer estado para a placa.
- **Dados de teste:** informações fictícias usadas para validar sistemas sem expor dados reais.

## Exemplos de placas

| Padrão | Formato | Exemplo |
| --- | --- | --- |
| Antigo com pontuação | AAA-1234 | BFA-4821 |
| Antigo sem pontuação | AAA1234 | BFA4821 |
| Mercosul | AAA1B23 | BFA4E21 |