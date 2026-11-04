---
title: "Gerador de Veículos"
seoTitle: "Gerador de Veículos"
description: "Gerador de Veículos: gere veículos fictícios com placa, Renavam e chassi. Grátis e online, sem cadastro."
summary: "Gere veículos fictícios com placa, Renavam e chassi."
date: 2026-11-04
draft: false
category: "documentos"
tags: ["veículos", "renavam", "placas", "gerador", "dados de teste", "documentos"]
keywords: ["gerador de veículos", "gerador de veículos online", "veículos", "renavam", "placas"]
---

Basta escolher as opções abaixo (todas são opcionais) e depois clicar em **Gerar Veículo**.

<div id="gerador-veiculos" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🚗 Gerador de Veículos</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Gere um veículo fictício com Renavam e placa válidos.</p>
<label for="vei-uf" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Qual Estado? (opcional)</label>
<select id="vei-uf" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;"></select>
<label for="vei-marca" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Marca do Veículo? (opcional)</label>
<select id="vei-marca" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;"></select>
<span style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Gerar com pontuação?</span>
<div style="display:flex;gap:20px;margin-bottom:20px;">
<label for="vei-pont-sim" style="display:flex;align-items:center;gap:6px;font-size:1rem;cursor:pointer;"><input type="radio" name="vei-pont" id="vei-pont-sim" style="accent-color:#4f46e5;width:18px;height:18px;"> Sim</label>
<label for="vei-pont-nao" style="display:flex;align-items:center;gap:6px;font-size:1rem;cursor:pointer;"><input type="radio" name="vei-pont" id="vei-pont-nao" checked style="accent-color:#4f46e5;width:18px;height:18px;"> Não</label>
</div>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="vei-gerar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Gerar Veículo</button>
<button type="button" id="vei-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="vei-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><span id="vei-msg"><strong style="color:#3730a3;">Resposta:</strong> clique em "Gerar Veículo" para criar um veículo.</span><div id="vei-campos" style="display:none;"></div></div>
</div>
<script>
(function () {
  var DADOS = {
    'Audi': ['A3', 'A4', 'Q3', 'Q5'],
    'BMW': ['118i', '320i', 'X1', 'X3'],
    'Chery': ['Tiggo 5X', 'Tiggo 7', 'Arrizo 6'],
    'Chrysler': ['300C', 'PT Cruiser', 'Pacifica'],
    'Citroen': ['C3', 'C4 Cactus', 'C4 Lounge', 'Aircross'],
    'Fiat': ['Uno', 'Palio', 'Siena', 'Mobi', 'Argo', 'Cronos', 'Strada', 'Toro'],
    'Ford': ['Ka', 'Fiesta', 'Focus', 'Fusion', 'EcoSport', 'Ranger'],
    'GM - Chevrolet': ['Celta', 'Corsa', 'Onix', 'Prisma', 'Cruze', 'Tracker', 'S10'],
    'Honda': ['Civic', 'Fit', 'City', 'HR-V', 'CR-V'],
    'Hyundai': ['HB20', 'Creta', 'Tucson', 'ix35', 'Azera'],
    'JAC': ['J3', 'J5', 'T40'],
    'Jeep': ['Renegade', 'Compass', 'Commander', 'Wrangler'],
    'Kia Motors': ['Picanto', 'Cerato', 'Sportage', 'Sorento'],
    'Land Rover': ['Discovery', 'Evoque', 'Defender'],
    'Mercedes-Benz': ['A 200', 'C 180', 'GLA 200', 'Classe E'],
    'MINI': ['Cooper', 'Countryman'],
    'Mitsubishi': ['Lancer', 'ASX', 'Pajero', 'L200 Triton'],
    'Nissan': ['March', 'Versa', 'Sentra', 'Kicks', 'Frontier'],
    'Peugeot': ['207', '208', '308', '2008'],
    'Porsche': ['911', 'Cayenne', 'Macan'],
    'RAM': ['1500', '2500'],
    'Renault': ['Clio', 'Sandero', 'Logan', 'Duster', 'Kwid', 'Captur'],
    'Subaru': ['Impreza', 'Forester', 'XV'],
    'Suzuki': ['Swift', 'Vitara', 'Jimny'],
    'Toyota': ['Etios', 'Yaris', 'Corolla', 'Hilux', 'SW4', 'RAV4'],
    'Troller': ['T4'],
    'Volvo': ['S60', 'XC60', 'XC90'],
    'VW - VolksWagen': ['Gol', 'Fox', 'Up!', 'Polo', 'Virtus', 'Voyage', 'Saveiro', 'T-Cross', 'Golf', 'Jetta']
  };
  var UFS = ['AC', 'AL', 'AM', 'AP', 'BA', 'CE', 'DF', 'ES', 'GO', 'MA', 'MG', 'MS', 'MT', 'PA', 'PB', 'PE', 'PI', 'PR', 'RJ', 'RN', 'RS', 'RO', 'RR', 'SC', 'SE', 'SP', 'TO'];
  var CORES = ['Branca', 'Preta', 'Prata', 'Cinza', 'Vermelha', 'Azul', 'Verde', 'Amarela', 'Marrom', 'Bege', 'Laranja', 'Dourada', 'Vinho'];
  var LETRAS = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ';
  var CAMPOS = [['uf', 'Estado'], ['marca', 'Marca'], ['modelo', 'Modelo'], ['ano', 'Ano'], ['renavam', 'RENAVAM'], ['placa', 'Placa'], ['cor', 'Cor']];
  var selUf = document.getElementById('vei-uf');
  var selMarca = document.getElementById('vei-marca');
  var radioSim = document.getElementById('vei-pont-sim');
  var caixa = document.getElementById('vei-resposta');
  var msg = document.getElementById('vei-msg');
  var campos = document.getElementById('vei-campos');
  var linhas = {};
  function opcao(select, valor, texto) {
    var o = document.createElement('option');
    o.value = valor;
    o.textContent = texto;
    select.appendChild(o);
  }
  function preencherSelects() {
    opcao(selUf, '', 'Selecione');
    UFS.forEach(function (uf) { opcao(selUf, uf, uf); });
    opcao(selMarca, '', 'Qualquer marca');
    Object.keys(DADOS).forEach(function (m) { opcao(selMarca, m, m); });
  }
  function rnd(min, max) { return Math.floor(Math.random() * (max - min + 1)) + min; }
  function pick(lista) { return lista[rnd(0, lista.length - 1)]; }
  function digitos(n) {
    return Array.from({ length: n }, function () { return rnd(0, 9); }).join('');
  }
  function letras(n) {
    return Array.from({ length: n }, function () { return LETRAS.charAt(rnd(0, 25)); }).join('');
  }
  function gerarRenavam(pontuado) {
    var base = String(rnd(1, 9)) + digitos(9);
    var pesos = [3, 2, 9, 8, 7, 6, 5, 4, 3, 2];
    var soma = 0;
    pesos.forEach(function (p, i) { soma += Number(base.charAt(i)) * p; });
    var dv = (soma * 10) % 11;
    if (dv > 9) { dv = 0; }
    return pontuado ? base + '-' + dv : base + String(dv);
  }
  function gerarPlaca(ano, pontuado) {
    if (ano > 2018) {
      return letras(3) + digitos(1) + letras(1) + digitos(2);
    }
    return letras(3) + (pontuado ? '-' : '') + digitos(4);
  }
  function copiar(texto, btn) {
    function ok() {
      btn.textContent = 'Copiado!';
      setTimeout(function () { btn.textContent = 'Copiar'; }, 1200);
    }
    function alternativo() {
      var t = document.createElement('textarea');
      t.value = texto;
      document.body.appendChild(t);
      t.select();
      try { document.execCommand('copy'); ok(); } catch (e) {}
      document.body.removeChild(t);
    }
    if (navigator.clipboard && navigator.clipboard.writeText) {
      navigator.clipboard.writeText(texto).then(ok, alternativo);
    } else {
      alternativo();
    }
  }
  function montarCampos() {
    CAMPOS.forEach(function (c) {
      var linha = document.createElement('div');
      linha.style.cssText = 'display:flex;align-items:center;gap:10px;padding:8px 0;border-bottom:1px solid #bbf7d0;';
      var rotulo = document.createElement('span');
      rotulo.style.cssText = 'flex:0 0 84px;font-weight:600;color:#3730a3;';
      rotulo.textContent = c[1] + ':';
      var valor = document.createElement('span');
      valor.style.cssText = 'flex:1;font-weight:700;color:#166534;word-break:break-all;';
      var btn = document.createElement('button');
      btn.type = 'button';
      btn.textContent = 'Copiar';
      btn.style.cssText = 'padding:6px 12px;font-size:0.85rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:8px;cursor:pointer;';
      btn.addEventListener('click', function () { copiar(valor.textContent, btn); });
      linha.appendChild(rotulo);
      linha.appendChild(valor);
      linha.appendChild(btn);
      campos.appendChild(linha);
      linhas[c[0]] = { linha: linha, valor: valor };
    });
  }
  function gerar() {
    var uf = selUf.value;
    var marca = selMarca.value || pick(Object.keys(DADOS));
    var ano = rnd(1995, new Date().getFullYear());
    var pontuado = radioSim.checked;
    linhas.uf.valor.textContent = uf;
    linhas.uf.linha.style.display = uf ? 'flex' : 'none';
    linhas.marca.valor.textContent = marca;
    linhas.modelo.valor.textContent = pick(DADOS[marca]);
    linhas.ano.valor.textContent = String(ano);
    linhas.renavam.valor.textContent = gerarRenavam(pontuado);
    linhas.placa.valor.textContent = gerarPlaca(ano, pontuado);
    linhas.cor.valor.textContent = pick(CORES);
    caixa.style.borderStyle = 'solid';
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    msg.style.display = 'none';
    campos.style.display = 'block';
  }
  function limpar() {
    selUf.value = '';
    selMarca.value = '';
    document.getElementById('vei-pont-nao').checked = true;
    caixa.style.borderStyle = 'dashed';
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    campos.style.display = 'none';
    msg.style.display = 'inline';
  }
  function destaque(el) {
    el.addEventListener('focus', function () { el.style.borderColor = '#6366f1'; });
    el.addEventListener('blur', function () { el.style.borderColor = '#c7d2fe'; });
  }
  preencherSelects();
  montarCampos();
  destaque(selUf);
  destaque(selMarca);
  document.getElementById('vei-gerar').addEventListener('click', gerar);
  document.getElementById('vei-limpar').addEventListener('click', limpar);
})();
</script>

## Como usar o gerador

1. Se quiser, escolha o **Estado** (UF) do veículo no primeiro campo.
2. Se quiser, escolha a **Marca do Veículo**. Deixando em "Qualquer marca", o gerador sorteia uma.
3. Marque **Sim** em "Gerar com pontuação" para que o Renavam e as placas no formato antigo saiam com hífen, ou **Não** para sair só com letras e números.
4. Clique em **Gerar Veículo** para ver marca, modelo, ano, Renavam, placa e cor.
5. Use o botão **Copiar** ao lado de cada campo para copiar o valor, ou **Limpar** para voltar ao início e gerar outro veículo.

Os dados são fictícios e servem para testes de software, preenchimento de formulários e demonstrações. Não use os dados gerados para fins ilegais ou para se passar por um veículo real.

## Entendendo os termos

- **Veículo fictício:** veículo gerado de forma aleatória, que não existe de verdade e não pertence a ninguém.
- **Estado (UF):** unidade da federação em que o veículo seria registrado, como SP, MG ou RJ.
- **Pontuação:** sinais de formatação, como o hífen entre as letras e os números da placa antiga (ABC-1234) ou antes do dígito final do Renavam.
- **Marca:** fabricante do veículo, como Fiat, Toyota ou Volkswagen.
- **Modelo:** nome comercial do veículo dentro da marca, como Uno, Corolla ou Gol.
- **Ano:** ano de fabricação do veículo.
- **RENAVAM:** Registro Nacional de Veículos Automotores, número de 11 dígitos que identifica o veículo no sistema de trânsito brasileiro. O último dígito é o dígito verificador.
- **Dígito verificador:** dígito final calculado a partir dos anteriores, usado para conferir se o número é válido.
- **Placa:** identificação do veículo, formada por letras e números. O gerador usa o formato antigo (ABC-1234) para veículos até 2018 e o formato Mercosul (ABC1D23) a partir de 2019.
- **Placa Mercosul:** padrão adotado no Brasil a partir de 2018, com três letras, um número, uma letra e dois números, sem hífen.
- **Cor:** cor predominante da pintura do veículo.