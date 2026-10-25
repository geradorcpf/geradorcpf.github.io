---
title: "Consulta de Número do Banco (DOC e TED)"
seoTitle: "Consulta de Número do Banco (DOC e TED)"
description: "Consulta de Número do Banco (DOC e TED): encontre o código de um banco para DOC e TED. Grátis e online, sem cadastro."
summary: "Encontre o código de um banco para DOC e TED."
date: 2026-10-25
draft: false
category: "documentos"
tags: ["bancos", "conta bancária", "consulta", "doc e ted", "documentos"]
keywords: ["consulta de número do banco (doc e ted)", "consulta de número do banco (doc e ted) online", "bancos", "conta bancária", "consulta"]
---
<!--sudah dikerjakan-->

Basta digitar o nome ou o código do banco abaixo e a lista é filtrada na hora. Você também pode clicar em um dos bancos principais para ver o código dele.

<div id="calc-banco" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🏦 Consulta de Número do Banco</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Encontre o código do banco para DOC e TED.</p>
<div style="margin-bottom:6px;font-weight:600;font-size:0.95rem;">Bancos principais</div>
<div id="bnk-principais" style="display:flex;gap:8px;flex-wrap:wrap;margin-bottom:20px;"></div>
<label for="bnk-busca" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Código ou nome do banco</label>
<input id="bnk-busca" type="text" placeholder="Ex.: itaú ou 341" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:20px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="bnk-filtrar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Filtrar Lista</button>
<button type="button" id="bnk-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="bnk-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="bnk-info">carregando a lista de bancos...</span></div>
<div style="margin-top:12px;max-height:360px;overflow:auto;background:#ffffff;border:2px solid #c7d2fe;border-radius:12px;">
<table style="width:100%;border-collapse:collapse;text-align:left;">
<thead><tr><th style="position:sticky;top:0;padding:10px 12px;background:#e0e7ff;color:#3730a3;font-size:0.9rem;">Código</th><th style="position:sticky;top:0;padding:10px 12px;background:#e0e7ff;color:#3730a3;font-size:0.9rem;">Nome do Banco</th></tr></thead>
<tbody id="bnk-corpo"></tbody>
</table>
</div>
</div>
<script>
(function () {
  var dados = [
    '654|BANCO A.J. RENNER S.A.', '246|BANCO ABC BRASIL S.A.', '075|BANCO ABN AMRO S.A.', '025|BANCO ALFA S.A.',
    '641|BANCO ALVORADA S.A.', '213|BANCO ARBI S.A.', '019|BANCO AZTECA DO BRASIL S.A.', '024|BANCO BANDEPE S.A.',
    '740|BANCO BARCLAYS S.A.', '107|BANCO BBM S/A', '096|BANCO BM\u0026FBOVESPA DE SERVIÇOS DE LIQUIDAÇÃO E CUSTÓDIA S.A.',
    '318|BANCO BMG S.A.', '752|BANCO BNP PARIBAS BRASIL S.A.', '248|BANCO BOAVISTA INTERATLANTICO S.A.',
    '218|BANCO BONSUCESSO S.A.', '063|BANCO BRADESCARD S.A.', '036|BANCO BRADESCO BBI S.A.',
    '122|BANCO BRADESCO BERJ S.A.', '204|BANCO BRADESCO CARTÕES S.A.', '394|BANCO BRADESCO FINANCIAMENTOS S.A.',
    '237|BANCO BRADESCO S.A.', '208|BANCO BTG PACTUAL S.A.', '263|BANCO CACIQUE S.A.',
    '473|BANCO CAIXA GERAL - BRASIL S.A.', '412|BANCO CAPITAL S.A.', '040|BANCO CARGILL S.A.',
    '266|BANCO CEDULA S.A.', '739|BANCO CETELEM S.A.', '233|BANCO CIFRA S.A.', '745|BANCO CITIBANK S.A.',
    '241|BANCO CLASSICO S.A.', 'M19|BANCO CNH INDUSTRIAL CAPITAL S.A.', '095|BANCO CONFIDENCE DE CÂMBIO S.A.',
    '756|BANCO COOPERATIVO DO BRASIL S.A. - BANCOOB', '748|BANCO COOPERATIVO SICREDI S.A.',
    '222|BANCO CRÉDIT AGRICOLE BRASIL S.A.', '505|BANCO CREDIT SUISSE (BRASIL) S.A.', '003|BANCO DA AMAZONIA S.A.',
    '083|BANCO DA CHINA BRASIL S.A.', '707|BANCO DAYCOVAL S.A.', '300|BANCO DE LA NACION ARGENTINA',
    '495|BANCO DE LA PROVINCIA DE BUENOS AIRES', '494|BANCO DE LA REPUBLICA ORIENTAL DEL URUGUAY',
    'M06|BANCO DE LAGE LANDEN BRASIL S.A.', '456|BANCO DE TOKYO-MITSUBISHI UFJ BRASIL S.A.',
    '001|BANCO DO BRASIL S.A.', '047|BANCO DO ESTADO DE SERGIPE S.A.', '037|BANCO DO ESTADO DO PARÁ S.A.',
    '041|BANCO DO ESTADO DO RIO GRANDE DO SUL S.A.', '004|BANCO DO NORDESTE DO BRASIL S.A.',
    '265|BANCO FATOR S.A.', '224|BANCO FIBRA S.A.', '626|BANCO FICSA S.A.', 'M18|BANCO FORD S.A.',
    '121|BANCO GERADOR S.A.', 'M07|BANCO GMAC S.A.', '612|BANCO GUANABARA S.A.', 'M22|BANCO HONDA S.A.',
    'M11|BANCO IBM S.A.', '604|BANCO INDUSTRIAL DO BRASIL S.A.', '320|BANCO INDUSTRIAL E COMERCIAL S.A.',
    '653|BANCO INDUSVAL S.A.', '630|BANCO INTERCAP S.A.', '077|BANCO INTERMEDIUM S.A.',
    '249|BANCO INVESTCRED UNIBANCO S.A.', '184|BANCO ITAÚ BBA S.A.', '029|BANCO ITAÚ BMG CONSIGNADO S.A.',
    '479|BANCO ITAUBANK S.A.', '074|BANCO J. SAFRA S.A.', '376|BANCO J.P. MORGAN S.A.',
    '217|BANCO JOHN DEERE S.A.', '076|BANCO KDB DO BRASIL S.A.', '757|BANCO KEB DO BRASIL S.A.',
    '600|BANCO LUSO BRASILEIRO S.A.', '243|BANCO MÁXIMA S.A.', 'M12|BANCO MAXINVEST S.A.',
    '389|BANCO MERCANTIL DO BRASIL S.A.', '370|BANCO MIZUHO DO BRASIL S.A.', '746|BANCO MODAL S.A.',
    'M10|BANCO MONEO S.A.', '066|BANCO MORGAN STANLEY S.A.', '079|BANCO ORIGINAL DO AGRONEGÓCIO S.A.',
    '212|BANCO ORIGINAL S.A.', 'M17|BANCO OURINVEST S.A.', '623|BANCO PAN S.A.', '611|BANCO PAULISTA S.A.',
    '613|BANCO PECUNIA S.A.', '094|BANCO PETRA S.A.', '643|BANCO PINE S.A.', '735|BANCO POTTENCIAL S.A.',
    'M24|BANCO PSA FINANCE BRASIL S.A.', '747|BANCO RABOBANK INTERNATIONAL BRASIL S.A.',
    '088|BANCO RANDON S.A.', '633|BANCO RENDIMENTO S.A.', '741|BANCO RIBEIRAO PRETO S.A.',
    '120|BANCO RODOBENS S.A.', '422|BANCO SAFRA S.A.', '033|BANCO SANTANDER (BRASIL) S.A.',
    '743|BANCO SEMEAR S.A.', '754|BANCO SISTEMA S.A.', '366|BANCO SOCIETE GENERALE BRASIL S.A.',
    '637|BANCO SOFISA S.A.', '464|BANCO SUMITOMO MITSUI BRASILEIRO S.A.', '082|BANCO TOPÁZIO S.A.',
    'M20|BANCO TOYOTA DO BRASIL S.A.', '634|BANCO TRIANGULO S.A.', '018|BANCO TRICURY S.A.',
    'M14|BANCO VOLKSWAGEN S.A.', 'M23|BANCO VOLVO BRASIL S.A.', '655|BANCO VOTORANTIM S.A.',
    '610|BANCO VR S.A.', '119|BANCO WESTERN UNION DO BRASIL S.A.', '124|BANCO WOORI BANK DO BRASIL S.A.',
    '021|BANESTES S.A. BANCO DO ESTADO DO ESPIRITO SANTO',
    '719|BANIF - BANCO INTERNACIONAL DO FUNCHAL (BRASIL), S.A.',
    '755|BANK OF AMERICA MERRILL LYNCH BANCO MÚLTIPLO S.A.', '081|BBN BANCO BRASILEIRO DE NEGÓCIOS S.A.',
    '250|BCV - BANCO DE CRÉDITO E VAREJO S/A', '017|BNY MELLON BANCO S.A.', '069|BPN BRASIL BANCO MÚLTIPLO S.A.',
    '125|BRASIL PLURAL S.A. BANCO MÚLTIPLO', '070|BRB - BANCO DE BRASILIA S.A.', '477|CITIBANK N.A.',
    '487|DEUTSCHE BANK S.A. - BANCO ALEMAO', '064|GOLDMAN SACHS DO BRASIL BANCO MULTIPLO S.A.',
    '062|HIPERCARD BANCO MÚLTIPLO S.A.', '132|ICBC DO BRASIL BANCO MÚLTIPLO S.A.', '492|ING BANK N.V.',
    '652|ITAÚ UNIBANCO HOLDING S.A.', '341|ITAÚ UNIBANCO S.A.', '488|JPMORGAN CHASE BANK, NATIONAL ASSOCIATION',
    '014|NATIXIS BRASIL S.A. BANCO MÚLTIPLO', '753|NOVO BANCO CONTINENTAL S.A. - BANCO MÚLTIPLO',
    '254|PARANÁ BANCO S.A.', '751|SCOTIABANK BRASIL S.A. BANCO MÚLTIPLO'
  ];
  var principais = [
    ['001', 'BANCO DO BRASIL S.A.', 'Banco do Brasil'],
    ['745', 'BANCO CITIBANK S.A.', 'Citibank'],
    ['422', 'BANCO SAFRA S.A.', 'Safra'],
    ['341', 'ITAÚ UNIBANCO S.A.', 'Itaú'],
    ['237', 'BANCO BRADESCO S.A.', 'Bradesco'],
    ['033', 'BANCO SANTANDER (BRASIL) S.A.', 'Santander']
  ];
  var campo = document.getElementById('bnk-busca');
  var corpo = document.getElementById('bnk-corpo');
  var info = document.getElementById('bnk-info');
  var caixa = document.getElementById('bnk-resposta');
  var areaPrincipais = document.getElementById('bnk-principais');
  function norm(s) {
    return String(s).toLowerCase().normalize('NFD').replace(/[\u0300-\u036f]/g, '');
  }
  function celula(txt, destaque) {
    var td = document.createElement('td');
    td.textContent = txt;
    td.style.cssText = 'padding:8px 12px;border-bottom:1px solid #e0e7ff;font-size:0.9rem;color:#1e293b;' + (destaque ? 'font-weight:700;color:#3730a3;white-space:nowrap;' : '');
    return td;
  }
  function estado(cor, fundo, texto, msg) {
    caixa.style.borderColor = cor;
    caixa.style.background = fundo;
    info.style.color = texto;
    info.textContent = msg;
  }
  function desenhar(lista) {
    corpo.textContent = '';
    lista.forEach(function (item) {
      var partes = item.split('|');
      var tr = document.createElement('tr');
      tr.appendChild(celula(partes[0], true));
      tr.appendChild(celula(partes[1], false));
      corpo.appendChild(tr);
    });
  }
  function filtrar() {
    var termos = norm(campo.value).trim().split(/\s+/).filter(function (t) { return t !== ''; });
    var lista = dados.filter(function (item) {
      var alvo = norm(item.replace('|', ' '));
      return termos.every(function (t) { return alvo.indexOf(t) !== -1; });
    });
    desenhar(lista);
    if (lista.length === 0) {
      estado('#fca5a5', '#fef2f2', '#b91c1c', 'nenhum banco encontrado. Tente outro nome ou código.');
    } else if (termos.length === 0) {
      estado('#c7d2fe', '#ffffff', '#64748b', 'mostrando todos os ' + lista.length + ' bancos. Digite um nome ou código para filtrar.');
    } else if (lista.length === 1) {
      estado('#86efac', '#f0fdf4', '#166534', 'o número do banco é ' + lista[0].split('|')[0] + ' (' + lista[0].split('|')[1] + ').');
    } else {
      estado('#86efac', '#f0fdf4', '#166534', lista.length + ' bancos encontrados na lista abaixo.');
    }
  }
  function limpar() {
    campo.value = '';
    filtrar();
    campo.focus();
  }
  principais.forEach(function (p) {
    var b = document.createElement('button');
    b.type = 'button';
    b.title = p[1];
    b.textContent = p[0] + ' · ' + p[2];
    b.style.cssText = 'padding:8px 12px;font-size:0.9rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;';
    b.addEventListener('click', function () {
      campo.value = p[0];
      filtrar();
    });
    areaPrincipais.appendChild(b);
  });
  document.getElementById('bnk-filtrar').addEventListener('click', filtrar);
  document.getElementById('bnk-limpar').addEventListener('click', limpar);
  campo.addEventListener('input', filtrar);
  campo.addEventListener('keydown', function (e) { if (e.key === 'Enter') { filtrar(); } });
  campo.addEventListener('focus', function () { campo.style.borderColor = '#6366f1'; });
  campo.addEventListener('blur', function () { campo.style.borderColor = '#c7d2fe'; });
  filtrar();
})();
</script>

## Como usar a consulta

1. Veja os **bancos principais** no topo da ferramenta. Clique em um deles para encontrar o código na hora.
2. Para outros bancos, digite parte do **nome** (por exemplo, `bradesco`) ou o **código** (por exemplo, `237`) no campo de busca.
3. Clique em **Filtrar Lista** (ou pressione Enter) para reduzir a lista. A busca também é atualizada enquanto você digita.
4. Confira o **código** na primeira coluna da tabela e use-o no campo "banco" ao fazer o DOC ou TED.
5. Use o botão **Limpar** para apagar a busca e voltar a ver a lista completa.

Você não precisa se preocupar com acentos nem com letras maiúsculas ou minúsculas: buscar por `itau` encontra "ITAÚ" normalmente. Se digitar mais de uma palavra, a lista mostra só os bancos que contêm todas elas.

## Entendendo os termos

- **Número do banco (código do banco):** identificação de três caracteres de cada instituição financeira, usada para indicar para qual banco o dinheiro vai. Exemplo: 001 é o Banco do Brasil.
- **DOC:** Documento de Ordem de Crédito, um tipo de transferência entre contas de bancos diferentes. Foi descontinuado pelo Banco Central em 2024, mas o código do banco continua sendo o mesmo nas outras transferências.
- **TED:** Transferência Eletrônica Disponível, transferência entre bancos diferentes que o dinheiro cai no mesmo dia útil, dentro do horário de funcionamento.
- **Banco:** instituição financeira que guarda o dinheiro dos clientes e oferece contas, cartões, crédito e transferências.
- **Agência:** unidade do banco onde a conta foi aberta, identificada por um número.
- **Conta:** número da conta bancária do favorecido, normalmente seguido de um dígito verificador.
- **Favorecido:** pessoa ou empresa que vai receber o dinheiro da transferência.
- **Filtrar Lista:** ação que reduz a tabela para mostrar apenas os bancos que combinam com o texto digitado.
- **Bancos principais:** os seis bancos mais usados, mostrados no topo para consulta rápida: Banco do Brasil, Citibank, Safra, Itaú, Bradesco e Santander.