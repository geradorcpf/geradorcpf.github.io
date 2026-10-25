---
title: "Consulta de CEP"
seoTitle: "Consulta de CEP: online e grátis"
description: "Consulta de CEP: encontre o endereço de um CEP ou o CEP de um endereço. Grátis e online, sem cadastro."
summary: "Encontre o endereço de um CEP ou o CEP de um endereço."
date: 2026-10-25
draft: false
category: "documentos"
tags: ["cep", "endereço", "consulta", "documentos"]
keywords: ["consulta de cep", "consulta de cep online", "cep", "endereço", "consulta"]
---
<!--sudah dikerjakan-->

Basta digitar o CEP (ou o endereço) abaixo e depois clicar em **Consultar**.

<div id="calc-cep" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">📮 Consulta de CEP</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Encontre o endereço de um CEP ou o CEP de um endereço.</p>
<div style="display:flex;gap:10px;flex-wrap:wrap;margin-bottom:18px;">
<button type="button" id="cep-aba-cep" style="flex:1;min-width:140px;padding:10px 14px;font-size:0.95rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:2px solid transparent;border-radius:10px;cursor:pointer;">Buscar por CEP</button>
<button type="button" id="cep-aba-end" style="flex:1;min-width:140px;padding:10px 14px;font-size:0.95rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Buscar por endereço</button>
</div>
<div id="cep-box-cep">
<label for="cep-campo-cep" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">CEP</label>
<input id="cep-campo-cep" type="text" inputmode="numeric" maxlength="9" placeholder="Ex.: 01001-000" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:20px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
</div>
<div id="cep-box-end" style="display:none;">
<label for="cep-campo-uf" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Estado (UF)</label>
<select id="cep-campo-uf" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;"><option value="">Selecione</option><option value="AC">AC</option><option value="AL">AL</option><option value="AP">AP</option><option value="AM">AM</option><option value="BA">BA</option><option value="CE">CE</option><option value="DF">DF</option><option value="ES">ES</option><option value="GO">GO</option><option value="MA">MA</option><option value="MT">MT</option><option value="MS">MS</option><option value="MG">MG</option><option value="PA">PA</option><option value="PB">PB</option><option value="PR">PR</option><option value="PE">PE</option><option value="PI">PI</option><option value="RJ">RJ</option><option value="RN">RN</option><option value="RS">RS</option><option value="RO">RO</option><option value="RR">RR</option><option value="SC">SC</option><option value="SP">SP</option><option value="SE">SE</option><option value="TO">TO</option></select>
<label for="cep-campo-cidade" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Cidade</label>
<input id="cep-campo-cidade" type="text" placeholder="Ex.: São Paulo" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<label for="cep-campo-logradouro" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Logradouro</label>
<input id="cep-campo-logradouro" type="text" placeholder="Ex.: Avenida Paulista" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:20px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
</div>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="cep-consultar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Consultar</button>
<button type="button" id="cep-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="cep-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <div id="cep-resultado" style="display:inline;">preencha os campos e clique em "Consultar".</div></div>
</div>
<script>
(function () {
  var URL_BASE = 'https://viacep.com.br/ws/';
  var MSG_INICIAL = 'preencha os campos e clique em "Consultar".';
  var modo = 'cep';
  var abaCep = document.getElementById('cep-aba-cep');
  var abaEnd = document.getElementById('cep-aba-end');
  var boxCep = document.getElementById('cep-box-cep');
  var boxEnd = document.getElementById('cep-box-end');
  var campoCep = document.getElementById('cep-campo-cep');
  var campoUf = document.getElementById('cep-campo-uf');
  var campoCidade = document.getElementById('cep-campo-cidade');
  var campoLogradouro = document.getElementById('cep-campo-logradouro');
  var caixa = document.getElementById('cep-resposta');
  var resultado = document.getElementById('cep-resultado');
  var estiloAtivo = 'flex:1;min-width:140px;padding:10px 14px;font-size:0.95rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:2px solid transparent;border-radius:10px;cursor:pointer;';
  var estiloInativo = 'flex:1;min-width:140px;padding:10px 14px;font-size:0.95rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;';
  var contador = 0;
  function estado(tipo) {
    if (tipo === 'ok') {
      caixa.style.borderColor = '#86efac';
      caixa.style.background = '#f0fdf4';
      resultado.style.color = '#166534';
    } else if (tipo === 'erro') {
      caixa.style.borderColor = '#fca5a5';
      caixa.style.background = '#fef2f2';
      resultado.style.color = '#b91c1c';
    } else {
      caixa.style.borderColor = '#c7d2fe';
      caixa.style.background = '#ffffff';
      resultado.style.color = '#64748b';
    }
  }
  function mensagem(tipo, texto) {
    estado(tipo);
    resultado.style.display = 'inline';
    resultado.textContent = texto;
  }
  function campo(rotulo, valor) {
    var linha = document.createElement('div');
    linha.style.cssText = 'margin:2px 0;';
    var r = document.createElement('strong');
    r.style.color = '#3730a3';
    r.textContent = rotulo + ': ';
    linha.appendChild(r);
    linha.appendChild(document.createTextNode(valor ? valor : '-'));
    return linha;
  }
  function mostrar(lista) {
    estado('ok');
    resultado.style.display = 'block';
    resultado.textContent = '';
    var titulo = document.createElement('div');
    titulo.style.cssText = 'margin-bottom:6px;font-weight:600;';
    titulo.textContent = lista.length === 1 ? 'Endereço encontrado:' : lista.length + ' endereços encontrados:';
    resultado.appendChild(titulo);
    lista.forEach(function (item, i) {
      var cartao = document.createElement('div');
      cartao.style.cssText = i === 0 ? 'padding:6px 0;' : 'padding:10px 0 6px;border-top:1px solid #bbf7d0;';
      cartao.appendChild(campo('CEP', item.cep));
      cartao.appendChild(campo('Logradouro', item.logradouro));
      cartao.appendChild(campo('Bairro', item.bairro));
      cartao.appendChild(campo('Cidade / UF', item.localidade + ' / ' + item.uf));
      cartao.appendChild(campo('Código IBGE', item.ibge));
      resultado.appendChild(cartao);
    });
  }
  function buscar(url, vazio) {
    contador = contador + 1;
    var meuNumero = contador;
    mensagem('neutro', 'consultando...');
    fetch(url).then(function (resp) {
      if (!resp.ok) { throw new Error('http'); }
      return resp.json();
    }).then(function (dados) {
      if (meuNumero !== contador) { return; }
      var lista = Array.isArray(dados) ? dados : [dados];
      if (lista.length === 0 || lista[0].erro) { mensagem('erro', vazio); return; }
      mostrar(lista);
    }).catch(function () {
      if (meuNumero !== contador) { return; }
      mensagem('erro', 'não foi possível consultar agora. Confira os dados e tente novamente.');
    });
  }
  function consultar() {
    if (modo === 'cep') {
      var digitos = campoCep.value.replace(/\D/g, '');
      if (digitos.length !== 8) { mensagem('erro', 'informe um CEP com 8 dígitos.'); return; }
      buscar(URL_BASE + digitos + '/json/', 'CEP não encontrado.');
      return;
    }
    var uf = campoUf.value;
    var cidade = campoCidade.value.trim();
    var rua = campoLogradouro.value.trim();
    if (uf === '') { mensagem('erro', 'selecione o estado (UF).'); return; }
    if (cidade.length === 0) { mensagem('erro', 'informe a cidade.'); return; }
    if (rua.length === 0) { mensagem('erro', 'informe o logradouro.'); return; }
    if (rua.length === 1 || rua.length === 2) { mensagem('erro', 'o logradouro deve ter pelo menos 3 letras.'); return; }
    buscar(URL_BASE + uf + '/' + encodeURIComponent(cidade) + '/' + encodeURIComponent(rua) + '/json/', 'nenhum CEP encontrado para esse endereço.');
  }
  function trocarModo(novo) {
    modo = novo;
    boxCep.style.display = novo === 'cep' ? 'block' : 'none';
    boxEnd.style.display = novo === 'cep' ? 'none' : 'block';
    abaCep.style.cssText = novo === 'cep' ? estiloAtivo : estiloInativo;
    abaEnd.style.cssText = novo === 'cep' ? estiloInativo : estiloAtivo;
    contador = contador + 1;
    mensagem('neutro', MSG_INICIAL);
  }
  function limpar() {
    campoCep.value = '';
    campoUf.value = '';
    campoCidade.value = '';
    campoLogradouro.value = '';
    contador = contador + 1;
    mensagem('neutro', MSG_INICIAL);
    if (modo === 'cep') { campoCep.focus(); } else { campoUf.focus(); }
  }
  campoCep.addEventListener('input', function () {
    var d = campoCep.value.replace(/\D/g, '').slice(0, 8);
    campoCep.value = d.length > 5 ? d.slice(0, 5) + '-' + d.slice(5) : d;
  });
  abaCep.addEventListener('click', function () { trocarModo('cep'); });
  abaEnd.addEventListener('click', function () { trocarModo('end'); });
  document.getElementById('cep-consultar').addEventListener('click', consultar);
  document.getElementById('cep-limpar').addEventListener('click', limpar);
  [campoCep, campoUf, campoCidade, campoLogradouro].forEach(function (el) {
    el.addEventListener('keydown', function (e) { if (e.key === 'Enter') { consultar(); } });
    el.addEventListener('focus', function () { el.style.borderColor = '#6366f1'; });
    el.addEventListener('blur', function () { el.style.borderColor = '#c7d2fe'; });
  });
})();
</script>

## Como usar a ferramenta

**Para descobrir o endereço de um CEP:**

1. Deixe selecionada a aba **Buscar por CEP**.
2. Digite o CEP com 8 dígitos (o hífen é colocado automaticamente).
3. Clique em **Consultar** (ou pressione Enter) para ver o logradouro, o bairro, a cidade, a UF e o código IBGE.

**Para descobrir o CEP de um endereço:**

1. Clique na aba **Buscar por endereço**.
2. Selecione o **Estado (UF)** e digite o nome da **Cidade**.
3. Digite o **Logradouro** (rua, avenida, praça etc.). Basta o nome ou parte dele, com pelo menos 3 letras.
4. Clique em **Consultar** para ver a lista de endereços e CEPs correspondentes.

Use o botão **Limpar** para apagar os campos e fazer uma nova consulta. A ferramenta precisa de conexão com a internet, pois os dados vêm de uma base pública de CEPs baseada nos Correios.

## Entendendo os termos

- **CEP:** Código de Endereçamento Postal, formado por 8 dígitos (como 01001-000), que identifica uma rua, um bairro ou uma região para facilitar a entrega de correspondências.
- **Logradouro:** nome da via pública, como rua, avenida, travessa, praça ou estrada.
- **Bairro:** divisão de uma cidade em que o endereço está localizado.
- **Cidade:** município a que o endereço pertence.
- **UF:** Unidade Federativa, a sigla de duas letras do estado brasileiro (SP, RJ, MG etc.).
- **Código IBGE:** número de 7 dígitos que identifica cada município brasileiro nos registros oficiais do Instituto Brasileiro de Geografia e Estatística.
- **Correios:** empresa responsável pelo serviço postal no Brasil e pela criação e manutenção do sistema de CEP.