---
title: "Gerador de CEP"
seoTitle: "Gerador de CEP"
description: "Gerador de CEP: gere CEPs aleatórios no formato correto para testes. Grátis e online, sem cadastro."
summary: "Gere CEPs aleatórios no formato correto para testes."
date: 2026-10-28
draft: false
category: "documentos"
tags: ["cep", "endereço", "gerador", "dados de teste", "documentos"]
keywords: ["gerador de cep", "gerador de cep online", "cep", "endereço", "gerador"]
---

Para gerar um CEP de qualquer lugar do Brasil, basta clicar em **Gerar CEP**. Se quiser, escolha antes um estado, a quantidade de CEPs e se eles devem sair com ou sem pontuação.

<div id="gerador-cep" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">📮 Gerador de CEP</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Escolha as opções e gere CEPs aleatórios na hora.</p>
<label for="cep-estado" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Estado (opcional)</label>
<select id="cep-estado" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<option value="">Qualquer estado (Brasil inteiro)</option>
<option value="AC">AC - Acre</option>
<option value="AL">AL - Alagoas</option>
<option value="AP">AP - Amapá</option>
<option value="AM">AM - Amazonas</option>
<option value="BA">BA - Bahia</option>
<option value="CE">CE - Ceará</option>
<option value="DF">DF - Distrito Federal</option>
<option value="ES">ES - Espírito Santo</option>
<option value="GO">GO - Goiás</option>
<option value="MA">MA - Maranhão</option>
<option value="MT">MT - Mato Grosso</option>
<option value="MS">MS - Mato Grosso do Sul</option>
<option value="MG">MG - Minas Gerais</option>
<option value="PA">PA - Pará</option>
<option value="PB">PB - Paraíba</option>
<option value="PR">PR - Paraná</option>
<option value="PE">PE - Pernambuco</option>
<option value="PI">PI - Piauí</option>
<option value="RJ">RJ - Rio de Janeiro</option>
<option value="RN">RN - Rio Grande do Norte</option>
<option value="RS">RS - Rio Grande do Sul</option>
<option value="RO">RO - Rondônia</option>
<option value="RR">RR - Roraima</option>
<option value="SC">SC - Santa Catarina</option>
<option value="SP">SP - São Paulo</option>
<option value="SE">SE - Sergipe</option>
<option value="TO">TO - Tocantins</option>
</select>
<label for="cep-quantidade" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Quantidade (1 a 50)</label>
<input id="cep-quantidade" type="text" inputmode="numeric" value="1" placeholder="Ex.: 5" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<span style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Gerar com pontuação?</span>
<div style="display:flex;gap:20px;margin-bottom:20px;">
<label for="cep-pontuacao-sim" style="display:flex;align-items:center;gap:6px;font-size:1rem;cursor:pointer;"><input type="radio" id="cep-pontuacao-sim" name="cep-pontuacao" value="sim" checked> Sim</label>
<label for="cep-pontuacao-nao" style="display:flex;align-items:center;gap:6px;font-size:1rem;cursor:pointer;"><input type="radio" id="cep-pontuacao-nao" name="cep-pontuacao" value="nao"> Não</label>
</div>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="cep-gerar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Gerar CEP</button>
<button type="button" id="cep-copiar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Copiar</button>
<button type="button" id="cep-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="cep-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong>
<div id="cep-resultado" style="margin-top:6px;">escolha as opções e clique em "Gerar CEP".</div></div>
</div>
<script>
(function () {
  var faixas = {
    AC: [[69900000, 69999999]],
    AL: [[57000000, 57999999]],
    AP: [[68900000, 68999999]],
    AM: [[69000000, 69299999], [69400000, 69899999]],
    BA: [[40000000, 48999999]],
    CE: [[60000000, 63999999]],
    DF: [[70000000, 72799999], [73000000, 73699999]],
    ES: [[29000000, 29999999]],
    GO: [[72800000, 72999999], [73700000, 76799999]],
    MA: [[65000000, 65999999]],
    MT: [[78000000, 78899999]],
    MS: [[79000000, 79999999]],
    MG: [[30000000, 39999999]],
    PA: [[66000000, 68899999]],
    PB: [[58000000, 58999999]],
    PR: [[80000000, 87999999]],
    PE: [[50000000, 56999999]],
    PI: [[64000000, 64999999]],
    RJ: [[20000000, 28999999]],
    RN: [[59000000, 59999999]],
    RS: [[90000000, 99999999]],
    RO: [[76800000, 76999999], [78900000, 78999999]],
    RR: [[69300000, 69399999]],
    SC: [[88000000, 89999999]],
    SP: [[1000000, 19999999]],
    SE: [[49000000, 49999999]],
    TO: [[77000000, 77995999]]
  };
  var ufs = Object.keys(faixas);
  var estado = document.getElementById('cep-estado');
  var quantidade = document.getElementById('cep-quantidade');
  var resultado = document.getElementById('cep-resultado');
  var caixa = document.getElementById('cep-resposta');
  var botaoCopiar = document.getElementById('cep-copiar');
  var lista = [];
  function sortear(min, max) {
    return Math.floor(Math.random() * (max - min + 1)) + min;
  }
  function gerarNumero(uf) {
    var f = faixas[uf];
    var total = 0;
    f.forEach(function (r) { total += r[1] - r[0] + 1; });
    var pos = sortear(0, total - 1);
    var alvo = f[0][0];
    for (var i = 0; i !== f.length; i++) {
      var tam = f[i][1] - f[i][0] + 1;
      if (pos >= tam) {
        pos -= tam;
      } else {
        alvo = f[i][0] + pos;
        break;
      }
    }
    var s = String(alvo);
    while (s.length !== 8) { s = '0' + s; }
    return s;
  }
  function formatar(s, comPontuacao) {
    return comPontuacao ? s.slice(0, 5) + '-' + s.slice(5) : s;
  }
  function limparResultado() {
    while (resultado.firstChild) { resultado.removeChild(resultado.firstChild); }
  }
  function erro(msg) {
    lista = [];
    caixa.style.borderColor = '#fca5a5';
    caixa.style.background = '#fef2f2';
    resultado.style.color = '#b91c1c';
    limparResultado();
    resultado.textContent = msg;
  }
  function gerar() {
    var q = parseInt(quantidade.value, 10);
    if (!(q > 0) || q > 50) { erro('informe uma quantidade entre 1 e 50.'); return; }
    var comPontuacao = document.getElementById('cep-pontuacao-sim').checked;
    lista = [];
    limparResultado();
    for (var i = 0; i !== q; i++) {
      var uf = estado.value !== '' ? estado.value : ufs[sortear(0, ufs.length - 1)];
      var cep = formatar(gerarNumero(uf), comPontuacao);
      lista.push({ cep: cep, uf: uf });
      var linha = document.createElement('div');
      linha.style.cssText = 'padding:6px 0;border-bottom:1px solid #e2e8f0;';
      var numero = document.createElement('strong');
      numero.style.cssText = 'font-size:1.2rem;letter-spacing:0.5px;';
      numero.textContent = cep;
      var sigla = document.createElement('small');
      sigla.style.cssText = 'margin-left:10px;color:#475569;';
      sigla.textContent = uf;
      linha.appendChild(numero);
      linha.appendChild(sigla);
      resultado.appendChild(linha);
    }
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
  }
  function copiarFallback(texto) {
    var area = document.createElement('textarea');
    area.value = texto;
    area.style.position = 'fixed';
    area.style.opacity = '0';
    document.body.appendChild(area);
    area.select();
    try { document.execCommand('copy'); } catch (e) {}
    document.body.removeChild(area);
  }
  function copiar() {
    if (lista.length === 0) { erro('gere um CEP antes de copiar.'); return; }
    var texto = lista.map(function (item) { return item.cep; }).join('\n');
    if (navigator.clipboard) {
      navigator.clipboard.writeText(texto).catch(function () { copiarFallback(texto); });
    } else {
      copiarFallback(texto);
    }
    botaoCopiar.textContent = 'Copiado!';
    setTimeout(function () { botaoCopiar.textContent = 'Copiar'; }, 1500);
  }
  function limpar() {
    lista = [];
    estado.value = '';
    quantidade.value = '1';
    document.getElementById('cep-pontuacao-sim').checked = true;
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    resultado.style.color = '#64748b';
    limparResultado();
    resultado.textContent = 'escolha as opções e clique em "Gerar CEP".';
    quantidade.focus();
  }
  document.getElementById('cep-gerar').addEventListener('click', gerar);
  botaoCopiar.addEventListener('click', copiar);
  document.getElementById('cep-limpar').addEventListener('click', limpar);
  quantidade.addEventListener('keydown', function (e) { if (e.key === 'Enter') { gerar(); } });
  [estado, quantidade].forEach(function (el) {
    el.addEventListener('focus', function () { el.style.borderColor = '#6366f1'; });
    el.addEventListener('blur', function () { el.style.borderColor = '#c7d2fe'; });
  });
})();
</script>

## Como usar o gerador

1. No campo **Estado**, escolha um estado (UF) ou deixe em "Qualquer estado" para gerar CEPs de todo o Brasil.
2. Em **Quantidade**, informe quantos CEPs você quer gerar de uma só vez (de 1 a 50).
3. Em **Gerar com pontuação?**, marque **Sim** para o formato com hífen (`12345-678`) ou **Não** para apenas números (`12345678`).
4. Clique em **Gerar CEP** (ou pressione Enter no campo de quantidade) para ver os resultados.
5. Clique em **Copiar** para copiar todos os CEPs gerados, um por linha, e use **Limpar** para voltar às opções iniciais.

## Entendendo os termos

- **CEP:** sigla de Código de Endereçamento Postal, um código de 8 dígitos usado no Brasil para identificar ruas, bairros, cidades e outros pontos de entrega.
- **Correios:** empresa responsável por criar, manter e distribuir os CEPs no país.
- **Estado (UF):** unidade federativa do Brasil, representada por uma sigla de duas letras, como SP, RJ ou MG. Cada estado tem faixas de CEP próprias.
- **Faixa de CEP:** intervalo de números reservado a um estado. Por exemplo, os CEPs de São Paulo começam entre 01000-000 e 19999-999.
- **Pontuação:** o hífen que separa os 5 primeiros dígitos dos 3 últimos no formato `12345-678`.
- **Sufixo:** os 3 últimos dígitos do CEP, que ajudam a identificar o ponto de distribuição, como a rua ou o logradouro.
- **Quantidade:** número de CEPs gerados em uma única vez.
- **Dados de teste:** valores fictícios usados para testar formulários, cadastros e sistemas sem precisar de informações reais.

## Aviso importante

Os CEPs são sorteados dentro das faixas oficiais de cada estado e seguem o formato correto, mas **não são consultados em uma base de endereços**. Isso significa que um CEP gerado pode não corresponder a uma rua real. Use o gerador apenas para testes de software, formulários e validações de formato.