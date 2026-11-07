---
title: "Recibo Online"
seoTitle: "Recibo Online"
description: "Recibo Online: preencha e baixe um recibo de pagamento. Grátis e online, sem cadastro."
summary: "Preencha e baixe um recibo de pagamento."
date: 2026-11-07
draft: false
category: "financas"
tags: ["recibo", "pagamentos", "finanças"]
keywords: ["recibo online", "recibo", "pagamentos", "finanças"]
---

Preencha os campos abaixo e o recibo é montado na hora. Depois, clique em **Imprimir** para imprimir ou salvar em PDF.

<style>
@media print {
  body * { visibility: hidden !important; }
  #rec-recibo-area, #rec-recibo-area * { visibility: visible !important; }
  #rec-recibo-area { position: absolute; left: 0; top: 0; width: 100%; }
}
</style>
<div id="calc-recibo" style="max-width:760px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🧾 Recibo Online</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Preencha os dados e veja o recibo pronto para imprimir.</p>
<div style="display:flex;gap:16px;flex-wrap:wrap;">
<div style="flex:1;min-width:220px;">
<label for="rec-logo" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Logomarca (opcional)</label>
<input id="rec-logo" type="file" accept="image/*" style="width:100%;padding:10px 12px;margin-bottom:16px;font-size:0.9rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;">
</div>
<div style="flex:1;min-width:220px;">
<label for="rec-valor" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Valor (R$)</label>
<input id="rec-valor" type="text" inputmode="decimal" placeholder="Ex.: 1.500,00" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
</div>
</div>
<div style="display:flex;gap:16px;flex-wrap:wrap;">
<div style="flex:2;min-width:220px;">
<label for="rec-pagador" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Recebi(emos) de</label>
<input id="rec-pagador" type="text" placeholder="Nome de quem pagou" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
</div>
<div style="flex:1;min-width:180px;">
<label for="rec-doc-pagador" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">CPF/CNPJ de quem pagou</label>
<input id="rec-doc-pagador" type="text" placeholder="Ex.: 000.000.000-00" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
</div>
</div>
<label for="rec-referente" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Referente à(ao)</label>
<input id="rec-referente" type="text" placeholder="Ex.: aluguel do mês de novembro" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<div style="display:flex;gap:16px;flex-wrap:wrap;">
<div style="flex:1;min-width:220px;">
<label for="rec-cidade" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Cidade</label>
<input id="rec-cidade" type="text" placeholder="Ex.: São Paulo" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
</div>
<div style="flex:1;min-width:220px;">
<label for="rec-data" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Data</label>
<input id="rec-data" type="date" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
</div>
</div>
<div style="display:flex;gap:16px;flex-wrap:wrap;">
<div style="flex:2;min-width:220px;">
<label for="rec-emitente" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Nome de quem recebeu (assinatura)</label>
<input id="rec-emitente" type="text" placeholder="Nome do emitente" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
</div>
<div style="flex:1;min-width:180px;">
<label for="rec-doc-emitente" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">CPF/CNPJ de quem recebeu</label>
<input id="rec-doc-emitente" type="text" placeholder="Ex.: 00.000.000/0000-00" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
</div>
</div>
<label for="rec-vias" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Número de vias</label>
<select id="rec-vias" style="width:100%;padding:12px 14px;margin-bottom:20px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<option value="1">1 via</option>
<option value="2">2 vias</option>
</select>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="rec-imprimir" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Imprimir</button>
<button type="button" id="rec-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="rec-erro" aria-live="polite" style="display:none;margin-top:20px;padding:16px;background:#fef2f2;border:2px dashed #fca5a5;border-radius:12px;color:#b91c1c;font-size:1rem;line-height:1.6;"></div>
<div style="margin-top:20px;">
<div style="margin-bottom:8px;font-weight:700;color:#3730a3;">Pré-visualização</div>
<div id="rec-recibo-area"></div>
</div>
</div>
<script>
(function () {
  var MESES = ['janeiro', 'fevereiro', 'março', 'abril', 'maio', 'junho', 'julho', 'agosto', 'setembro', 'outubro', 'novembro', 'dezembro'];
  var UN = ['zero', 'um', 'dois', 'três', 'quatro', 'cinco', 'seis', 'sete', 'oito', 'nove', 'dez', 'onze', 'doze', 'treze', 'catorze', 'quinze', 'dezesseis', 'dezessete', 'dezoito', 'dezenove'];
  var DZ = ['', '', 'vinte', 'trinta', 'quarenta', 'cinquenta', 'sessenta', 'setenta', 'oitenta', 'noventa'];
  var CT = ['', 'cento', 'duzentos', 'trezentos', 'quatrocentos', 'quinhentos', 'seiscentos', 'setecentos', 'oitocentos', 'novecentos'];
  var logoSrc = '';
  var area = document.getElementById('rec-recibo-area');
  var caixaErro = document.getElementById('rec-erro');
  var logoInput = document.getElementById('rec-logo');
  var ids = ['rec-valor', 'rec-pagador', 'rec-doc-pagador', 'rec-referente', 'rec-cidade', 'rec-data', 'rec-emitente', 'rec-doc-emitente', 'rec-vias'];
  var campos = ids.map(function (id) { return document.getElementById(id); });
  var F = {};
  ids.forEach(function (id, i) { F[id] = campos[i]; });
  function pad(n) { return (n > 9 ? '' : '0') + n; }
  function hoje() {
    var d = new Date();
    return d.getFullYear() + '-' + pad(d.getMonth() + 1) + '-' + pad(d.getDate());
  }
  function numero(v) {
    var t = String(v).trim().replace(/\s/g, '');
    if (t.indexOf(',') > -1) { t = t.replace(/\./g, '').replace(',', '.'); }
    if (t === '' || isNaN(Number(t))) { return NaN; }
    return Number(t);
  }
  function ate999(n) {
    if (n === 0) { return ''; }
    if (n === 100) { return 'cem'; }
    var partes = [];
    var c = Math.floor(n / 100);
    var r = n % 100;
    if (c > 0) { partes.push(CT[c]); }
    if (r > 0) {
      if (20 > r) {
        partes.push(UN[r]);
      } else {
        var d = Math.floor(r / 10);
        var u = r % 10;
        partes.push(DZ[d] + (u > 0 ? ' e ' + UN[u] : ''));
      }
    }
    return partes.join(' e ');
  }
  function extensoInteiro(n) {
    if (n === 0) { return 'zero'; }
    var escalas = [[1000000000, 'bilhão', 'bilhões'], [1000000, 'milhão', 'milhões'], [1000, 'mil', 'mil']];
    var grupos = [];
    var textos = [];
    var resto = n;
    for (var i = 0; escalas.length > i; i++) {
      var g = Math.floor(resto / escalas[i][0]);
      resto = resto % escalas[i][0];
      if (g > 0) {
        var t;
        if (escalas[i][0] === 1000) {
          t = (g === 1) ? 'mil' : ate999(g) + ' mil';
        } else {
          t = (g === 1) ? 'um ' + escalas[i][1] : ate999(g) + ' ' + escalas[i][2];
        }
        grupos.push(g);
        textos.push(t);
      }
    }
    if (resto > 0) {
      grupos.push(resto);
      textos.push(ate999(resto));
    }
    var saida = textos[0];
    for (var j = 1; textos.length > j; j++) {
      var v = grupos[j];
      var ultimo = (j === textos.length - 1);
      var junta = ultimo ? (100 > v || v % 100 === 0) : false;
      saida += (junta ? ' e ' : ', ') + textos[j];
    }
    return saida;
  }
  function extensoMoeda(centavosTotal) {
    var reais = Math.floor(centavosTotal / 100);
    var cent = centavosTotal % 100;
    var partes = [];
    if (reais > 0) {
      partes.push(extensoInteiro(reais) + (reais % 1000000 === 0 ? ' de ' : ' ') + (reais === 1 ? 'real' : 'reais'));
    }
    if (cent > 0) {
      partes.push(extensoInteiro(cent) + ' ' + (cent === 1 ? 'centavo' : 'centavos'));
    }
    if (partes.length === 0) { return 'zero reais'; }
    return partes.join(' e ');
  }
  function fmt(n) {
    return n.toLocaleString('pt-BR', { minimumFractionDigits: 2, maximumFractionDigits: 2 });
  }
  function el(tag, css, texto) {
    var e = document.createElement(tag);
    if (css) { e.style.cssText = css; }
    if (texto !== undefined) { e.textContent = texto; }
    return e;
  }
  function dataExtenso(valor) {
    var p = String(valor).split('-');
    if (p.length !== 3) { return '____ de ______________ de ______'; }
    var mes = MESES[Number(p[1]) - 1];
    if (!mes) { return '____ de ______________ de ______'; }
    return String(Number(p[2])) + ' de ' + mes + ' de ' + p[0];
  }
  function mostrarErro(msg) {
    if (msg) {
      caixaErro.textContent = msg;
      caixaErro.style.display = 'block';
    } else {
      caixaErro.textContent = '';
      caixaErro.style.display = 'none';
    }
  }
  function criarVia(d) {
    var via = el('div', 'padding:20px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#1e293b;font-size:0.95rem;line-height:1.7;box-sizing:border-box;page-break-inside:avoid;margin-bottom:14px;');
    var topo = el('div', 'display:flex;justify-content:space-between;align-items:center;gap:12px;margin-bottom:12px;');
    var caixaLogo = el('div', 'min-height:48px;display:flex;align-items:center;');
    if (logoSrc) {
      var img = document.createElement('img');
      img.src = logoSrc;
      img.alt = 'Logomarca';
      img.style.cssText = 'max-height:64px;max-width:160px;';
      caixaLogo.appendChild(img);
    }
    topo.appendChild(caixaLogo);
    topo.appendChild(el('div', 'font-weight:700;font-size:1.1rem;color:#3730a3;white-space:nowrap;', 'Valor: R$ ' + d.valorFmt));
    via.appendChild(topo);
    via.appendChild(el('div', 'text-align:center;font-weight:700;font-size:1.3rem;letter-spacing:2px;color:#3730a3;margin-bottom:12px;', 'RECIBO'));
    var nome = d.pagador || '______________________________';
    var doc = d.docPagador || '________________';
    var ref = d.referente || '______________________________';
    via.appendChild(el('p', 'margin:0 0 10px;', 'Recebi(emos) de ' + nome + ', CPF/CNPJ nº ' + doc + ', a importância de ' + d.extenso + ' referente à(ao) ' + ref + '.'));
    via.appendChild(el('p', 'margin:0 0 10px;', 'Para maior clareza firmo(amos) o presente recibo para que produza os seus efeitos, dando plena, rasa e irrevogável quitação, pelo valor recebido.'));
    via.appendChild(el('p', 'margin:0 0 6px;text-align:right;', (d.cidade || '______________') + ', ' + d.data));
    via.appendChild(el('div', 'border-top:1px solid #64748b;margin:36px auto 6px;max-width:340px;'));
    via.appendChild(el('div', 'text-align:center;font-weight:600;', d.emitente || ' '));
    via.appendChild(el('div', 'text-align:center;color:#475569;font-size:0.9rem;', 'CPF/CNPJ: ' + (d.docEmitente || '________________')));
    return via;
  }
  function atualizar() {
    var bruto = F['rec-valor'].value;
    var valor = 0;
    var msg = '';
    if (bruto.trim() !== '') {
      var n = numero(bruto);
      if (isNaN(n)) {
        msg = 'informe um valor numérico válido.';
      } else if (0 >= n) {
        msg = 'o valor deve ser maior que zero.';
      } else if (n >= 1000000000000) {
        msg = 'o valor deve ser menor que 1 trilhão.';
      } else {
        valor = n;
      }
    }
    mostrarErro(msg);
    var centavos = Math.round(valor * 100);
    var dados = {
      valorFmt: fmt(centavos / 100),
      extenso: extensoMoeda(centavos),
      pagador: F['rec-pagador'].value.trim(),
      docPagador: F['rec-doc-pagador'].value.trim(),
      referente: F['rec-referente'].value.trim(),
      cidade: F['rec-cidade'].value.trim(),
      data: dataExtenso(F['rec-data'].value),
      emitente: F['rec-emitente'].value.trim(),
      docEmitente: F['rec-doc-emitente'].value.trim()
    };
    var vias = Number(F['rec-vias'].value) === 2 ? 2 : 1;
    area.textContent = '';
    for (var i = 0; vias > i; i++) {
      area.appendChild(criarVia(dados));
    }
  }
  function limpar() {
    campos.forEach(function (c) { c.value = ''; });
    F['rec-data'].value = hoje();
    F['rec-vias'].value = '1';
    logoInput.value = '';
    logoSrc = '';
    atualizar();
    F['rec-valor'].focus();
  }
  logoInput.addEventListener('change', function () {
    var arquivo = logoInput.files && logoInput.files[0];
    if (!arquivo) { logoSrc = ''; atualizar(); return; }
    if (arquivo.type.indexOf('image/') !== 0) {
      logoInput.value = '';
      logoSrc = '';
      mostrarErro('selecione um arquivo de imagem para a logomarca.');
      atualizar();
      return;
    }
    var leitor = new FileReader();
    leitor.onload = function () {
      logoSrc = String(leitor.result);
      atualizar();
    };
    leitor.readAsDataURL(arquivo);
  });
  campos.forEach(function (c) {
    c.addEventListener('input', atualizar);
    c.addEventListener('change', atualizar);
    c.addEventListener('focus', function () { c.style.borderColor = '#6366f1'; });
    c.addEventListener('blur', function () { c.style.borderColor = '#c7d2fe'; });
  });
  document.getElementById('rec-imprimir').addEventListener('click', function () { window.print(); });
  document.getElementById('rec-limpar').addEventListener('click', limpar);
  F['rec-data'].value = hoje();
  atualizar();
})();
</script>

## Como usar o gerador de recibo

1. Se quiser, envie a **Logomarca** da sua empresa no primeiro campo (imagem em PNG, JPG ou similar).
2. Digite o **Valor (R$)** recebido. O valor por extenso é escrito automaticamente no texto do recibo.
3. Preencha o nome e o **CPF/CNPJ** de quem pagou, no campo **Recebi(emos) de**.
4. Descreva o motivo do pagamento em **Referente à(ao)**, por exemplo: aluguel, venda de produto ou prestação de serviço.
5. Informe a **Cidade** e a **Data** do recibo. A data de hoje já vem preenchida.
6. Digite o nome e o **CPF/CNPJ** de quem recebeu o dinheiro. Esses dados aparecem abaixo da linha de assinatura.
7. Escolha **1 via** ou **2 vias** e confira a **Pré-visualização** abaixo dos botões.
8. Clique em **Imprimir** para imprimir o recibo ou salvar em PDF (escolha "Salvar como PDF" na janela de impressão). Depois, assine na linha indicada.
9. Use o botão **Limpar** para apagar todos os campos e preencher um novo recibo.

Você pode digitar o valor com vírgula ou ponto (por exemplo, `1500,50` ou `1500.50`). Os dados ficam apenas no seu navegador e não são enviados a nenhum servidor.

## Entendendo os termos

- **Recibo:** documento que comprova que alguém recebeu determinada quantia ou pagamento.
- **Logomarca:** imagem com a marca da empresa ou do profissional, exibida no topo do recibo.
- **Valor:** quantia em reais (R$) recebida, mostrada em números e também por extenso no texto.
- **Valor por extenso:** o mesmo valor escrito em palavras, como "mil e quinhentos reais", para evitar rasuras e dúvidas.
- **Recebi(emos) de:** nome da pessoa ou empresa que fez o pagamento, também chamada de pagador.
- **Emitente:** quem recebe o dinheiro e emite o recibo, assinando o documento.
- **CPF/CNPJ:** número de identificação da pessoa física (CPF) ou da empresa (CNPJ).
- **Referente à(ao):** motivo do pagamento, ou seja, o que está sendo quitado.
- **Quitação:** declaração de que o valor foi pago e de que nada mais é devido por aquele pagamento.
- **Via:** cópia do recibo. Normalmente uma via fica com quem pagou e outra com quem recebeu.