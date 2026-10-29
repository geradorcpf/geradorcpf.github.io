---
title: "Gerador de Conta Bancária"
seoTitle: "Gerador de Conta Bancária"
description: "Gerador de Conta Bancária: gere agência e conta bancária válidas para testes. Grátis e online, sem cadastro."
summary: "Gere agência e conta bancária válidas para testes."
date: 2026-10-29
draft: false
category: "documentos"
tags: ["bancos", "conta bancária", "gerador", "dados de teste", "documentos"]
keywords: ["gerador de conta bancária", "gerador de conta bancária online", "bancos", "conta bancária", "gerador"]
---

Escolha o banco e o estado (ambos são opcionais) e depois clique em **Gerar Conta**.

<div id="gerador-conta" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🏦 Gerador de Conta Bancária</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Gere agência e conta com dígito verificador válido para testes.</p>
<label for="cb-banco" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Banco (opcional)</label>
<select id="cb-banco" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;cursor:pointer;">
<option value="indiferente">Indiferente</option>
<option value="bb">Banco do Brasil</option>
<option value="bradesco">Bradesco</option>
<option value="citibank">Citibank</option>
<option value="itau">Itaú</option>
<option value="santander">Santander</option>
</select>
<label for="cb-estado" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Estado (opcional)</label>
<select id="cb-estado" style="width:100%;padding:12px 14px;margin-bottom:20px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;cursor:pointer;">
<option value="indiferente">Indiferente</option>
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
<button type="button" id="cb-gerar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Gerar Conta</button>
<button type="button" id="cb-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="cb-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="cb-resultado">escolha as opções e clique em "Gerar Conta".</span></div>
</div>
<script>
(function () {
  var selBanco = document.getElementById('cb-banco');
  var selEstado = document.getElementById('cb-estado');
  var caixa = document.getElementById('cb-resposta');
  var BANCOS = {
    bb: { cod: '001', nome: 'Banco do Brasil' },
    bradesco: { cod: '237', nome: 'Bradesco' },
    citibank: { cod: '745', nome: 'Citibank' },
    itau: { cod: '341', nome: 'Itaú' },
    santander: { cod: '033', nome: 'Santander' }
  };
  var CHAVES = ['bb', 'bradesco', 'citibank', 'itau', 'santander'];
  var CIDADES = {
    AC: 'Rio Branco,Cruzeiro do Sul,Sena Madureira',
    AL: 'Maceió,Arapiraca,Palmeira dos Índios',
    AM: 'Manaus,Parintins,Itacoatiara',
    AP: 'Macapá,Santana,Laranjal do Jari',
    BA: 'Salvador,Feira de Santana,Vitória da Conquista',
    CE: 'Fortaleza,Juazeiro do Norte,Sobral',
    DF: 'Brasília,Taguatinga,Ceilândia',
    ES: 'Vitória,Vila Velha,Serra',
    GO: 'Goiânia,Anápolis,Aparecida de Goiânia',
    MA: 'São Luís,Imperatriz,Caxias',
    MG: 'Belo Horizonte,Uberlândia,Juiz de Fora',
    MS: 'Campo Grande,Dourados,Três Lagoas',
    MT: 'Cuiabá,Rondonópolis,Sinop',
    PA: 'Belém,Santarém,Marabá',
    PB: 'João Pessoa,Campina Grande,Patos',
    PE: 'Recife,Olinda,Caruaru',
    PI: 'Teresina,Parnaíba,Picos',
    PR: 'Curitiba,Londrina,Maringá',
    RJ: 'Rio de Janeiro,Niterói,Petrópolis',
    RN: 'Natal,Mossoró,Parnamirim',
    RS: 'Porto Alegre,Caxias do Sul,Pelotas',
    RO: 'Porto Velho,Ji-Paraná,Ariquemes',
    RR: 'Boa Vista,Rorainópolis,Caracaraí',
    SC: 'Florianópolis,Joinville,Blumenau',
    SE: 'Aracaju,Lagarto,Itabaiana',
    SP: 'São Paulo,Campinas,Santos',
    TO: 'Palmas,Araguaína,Gurupi'
  };
  var UFS = Object.keys(CIDADES);
  function sorteio(n) { return Math.floor(Math.random() * n); }
  function escolher(lista) { return lista[sorteio(lista.length)]; }
  function digitos(qtd) {
    var s = String(1 + sorteio(9));
    while (s.length !== qtd) { s += String(sorteio(10)); }
    return s;
  }
  function soma(texto, pesos) {
    var total = 0;
    for (var i = 0; i !== texto.length; i++) {
      total += Number(texto.charAt(i)) * pesos[i];
    }
    return total;
  }
  function dvBB(texto, pesos) {
    var r = 11 - (soma(texto, pesos) % 11);
    if (r === 10) { return 'X'; }
    if (r === 11) { return '0'; }
    return String(r);
  }
  function dvBradesco(texto, pesos) {
    var r = soma(texto, pesos) % 11;
    if (r === 0) { return '0'; }
    if (r === 1) { return 'P'; }
    return String(11 - r);
  }
  function dvItau(texto) {
    var pesos = [2, 1, 2, 1, 2, 1, 2, 1, 2];
    var total = 0;
    for (var i = 0; i !== texto.length; i++) {
      var p = Number(texto.charAt(i)) * pesos[i];
      total += Math.floor(p / 10) + (p % 10);
    }
    return String((10 - (total % 10)) % 10);
  }
  function dvSantander(texto) {
    var pesos = [9, 7, 3, 1, 0, 0, 9, 7, 1, 3, 1, 9, 7, 3];
    var total = 0;
    for (var i = 0; i !== texto.length; i++) {
      total += (Number(texto.charAt(i)) * pesos[i]) % 10;
    }
    return String((10 - (total % 10)) % 10);
  }
  function dvCiti(texto) {
    var r = soma(texto, [8, 7, 6, 5, 4, 3, 2]) % 11;
    return (r === 0 || r === 1) ? '0' : String(11 - r);
  }
  var GERADORES = {
    bb: function () {
      var ag = digitos(4);
      var cc = digitos(8);
      return { agencia: ag + '-' + dvBB(ag, [5, 4, 3, 2]), conta: cc + '-' + dvBB(cc, [9, 8, 7, 6, 5, 4, 3, 2]) };
    },
    bradesco: function () {
      var ag = digitos(4);
      var cc = digitos(7);
      return { agencia: ag + '-' + dvBradesco(ag, [5, 4, 3, 2]), conta: cc + '-' + dvBradesco(cc, [2, 7, 6, 5, 4, 3, 2]) };
    },
    citibank: function () {
      var ag = digitos(4);
      var cc = digitos(7);
      return { agencia: ag, conta: cc + '-' + dvCiti(cc) };
    },
    itau: function () {
      var ag = digitos(4);
      var cc = digitos(5);
      return { agencia: ag, conta: cc + '-' + dvItau(ag + cc) };
    },
    santander: function () {
      var ag = digitos(4);
      var cc = digitos(8);
      return { agencia: ag, conta: cc + '-' + dvSantander(ag + '00' + cc) };
    }
  };
  function copiar(texto, botao) {
    function feito() {
      botao.textContent = 'Copiado!';
      setTimeout(function () { botao.textContent = 'Copiar'; }, 1200);
    }
    if (navigator.clipboard && navigator.clipboard.writeText) {
      navigator.clipboard.writeText(texto).then(feito, function () {});
      return;
    }
    var area = document.createElement('textarea');
    area.value = texto;
    document.body.appendChild(area);
    area.select();
    try { document.execCommand('copy'); feito(); } catch (e) {}
    document.body.removeChild(area);
  }
  function mostrar(linhas) {
    caixa.textContent = '';
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    caixa.style.color = '#166534';
    var titulo = document.createElement('strong');
    titulo.style.color = '#166534';
    titulo.textContent = 'Resposta:';
    caixa.appendChild(titulo);
    linhas.forEach(function (item) {
      var linha = document.createElement('div');
      linha.style.cssText = 'display:flex;align-items:center;justify-content:space-between;gap:10px;padding:8px 0;border-bottom:1px solid #bbf7d0;';
      var rotulo = document.createElement('span');
      rotulo.style.cssText = 'color:#475569;font-size:0.9rem;';
      rotulo.textContent = item[0];
      var valor = document.createElement('strong');
      valor.style.cssText = 'flex:1;text-align:right;font-size:1.05rem;word-break:break-word;';
      valor.textContent = item[1];
      var botao = document.createElement('button');
      botao.type = 'button';
      botao.textContent = 'Copiar';
      botao.style.cssText = 'padding:4px 10px;font-size:0.8rem;font-weight:600;color:#4f46e5;background:#ffffff;border:1px solid #c7d2fe;border-radius:8px;cursor:pointer;';
      botao.addEventListener('click', function () { copiar(item[1], botao); });
      linha.appendChild(rotulo);
      linha.appendChild(valor);
      linha.appendChild(botao);
      caixa.appendChild(linha);
    });
  }
  function gerar() {
    var chave = selBanco.value === 'indiferente' ? escolher(CHAVES) : selBanco.value;
    var uf = selEstado.value === 'indiferente' ? escolher(UFS) : selEstado.value;
    var banco = BANCOS[chave];
    var dados = GERADORES[chave]();
    var cidade = escolher(CIDADES[uf].split(','));
    mostrar([
      ['Conta Corrente', dados.conta],
      ['Agência', dados.agencia],
      ['Banco', banco.cod + ' - ' + banco.nome],
      ['Cidade', cidade],
      ['Estado', uf]
    ]);
  }
  function limpar() {
    selBanco.value = 'indiferente';
    selEstado.value = 'indiferente';
    caixa.textContent = '';
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    caixa.style.color = '#64748b';
    var titulo = document.createElement('strong');
    titulo.style.color = '#3730a3';
    titulo.textContent = 'Resposta:';
    var texto = document.createElement('span');
    texto.textContent = ' escolha as opções e clique em "Gerar Conta".';
    caixa.appendChild(titulo);
    caixa.appendChild(texto);
  }
  document.getElementById('cb-gerar').addEventListener('click', gerar);
  document.getElementById('cb-limpar').addEventListener('click', limpar);
})();
</script>

## Como usar o gerador

1. Escolha o **Banco** no primeiro campo. Se deixar em "Indiferente", o gerador sorteia um dos bancos disponíveis.
2. Escolha o **Estado** no segundo campo. Se deixar em "Indiferente", o gerador sorteia um estado.
3. Clique em **Gerar Conta** para ver a conta corrente, a agência, o banco, a cidade e o estado.
4. Use o botão **Copiar** ao lado de cada item para copiar o valor e colar no seu sistema de testes.
5. Clique em **Gerar Conta** de novo para criar outra combinação, ou em **Limpar** para voltar às opções iniciais.

Os números são gerados de forma aleatória, seguindo a regra de cálculo do dígito verificador de cada banco. Eles servem apenas para testes e não correspondem a contas reais.

## Entendendo os termos

- **Conta bancária:** registro mantido por um banco em nome de um cliente, usado para guardar dinheiro e fazer movimentações financeiras.
- **Conta corrente:** tipo de conta usado no dia a dia, para receber salário, pagar contas e fazer transferências. É o número que o gerador cria.
- **Agência:** unidade do banco onde a conta foi aberta, identificada por um número de quatro dígitos.
- **Dígito verificador (DV):** número ou letra no fim da agência ou da conta, calculado a partir dos demais dígitos para detectar erros de digitação.
- **Código do banco:** número de três dígitos que identifica cada instituição financeira no Brasil, como 001 (Banco do Brasil) e 341 (Itaú).
- **Banco (opcional):** instituição financeira usada na geração. Cada banco tem um formato e uma regra de cálculo diferentes.
- **Estado (opcional):** unidade da federação (UF) em que a agência fica. A cidade sorteada pertence ao estado escolhido.
- **Cidade:** município onde fica a agência, sorteado entre as cidades do estado.
- **Dados de teste:** informações fictícias, mas com formato válido, usadas para testar sistemas, formulários e validações sem expor dados de pessoas reais.

## Aviso importante

Este gerador ajuda estudantes, programadores, analistas e testadores a obter contas bancárias com formato válido para testar softwares em desenvolvimento. O uso indevido dos dados gerados é de responsabilidade de quem os utiliza.