---
title: "Gerador de Inscrição Estadual"
seoTitle: "Gerador de Inscrição Estadual"
description: "Gerador de Inscrição Estadual: gere inscrições estaduais válidas para qualquer estado. Grátis e online, sem cadastro."
summary: "Gere inscrições estaduais válidas para qualquer estado."
date: 2026-11-02
draft: false
category: "documentos"
tags: ["inscrição estadual", "empresas", "cnpj", "gerador", "dados de teste", "documentos"]
keywords: ["gerador de inscrição estadual", "gerador de inscrição estadual online", "inscrição estadual", "empresas", "cnpj"]
---
<!--INI SUDAH DIKERJAKAN-->

Basta escolher o estado, definir se quer a pontuação e clicar em **Gerar Inscrição Estadual**.

<div id="calc-inscricao-estadual" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">🏢 Gerador de Inscrição Estadual</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Escolha o estado e gere um número válido na hora.</p>
<label for="ie-estado" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Qual estado?</label>
<select id="ie-estado" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
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
<option value="SP" selected>SP - São Paulo</option>
<option value="SC">SC - Santa Catarina</option>
<option value="SE">SE - Sergipe</option>
<option value="TO">TO - Tocantins</option>
</select>
<span style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Gerar com pontuação?</span>
<div style="display:flex;gap:20px;margin-bottom:20px;">
<label for="ie-pont-sim" style="display:inline-flex;align-items:center;gap:6px;font-size:1rem;cursor:pointer;"><input type="radio" id="ie-pont-sim" name="ie-pontuacao" value="sim" checked style="width:18px;height:18px;accent-color:#4f46e5;cursor:pointer;"> Sim</label>
<label for="ie-pont-nao" style="display:inline-flex;align-items:center;gap:6px;font-size:1rem;cursor:pointer;"><input type="radio" id="ie-pont-nao" name="ie-pontuacao" value="nao" style="width:18px;height:18px;accent-color:#4f46e5;cursor:pointer;"> Não</label>
</div>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="ie-gerar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Gerar Inscrição Estadual</button>
<button type="button" id="ie-copiar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Copiar</button>
<button type="button" id="ie-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="ie-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;word-break:break-all;"><strong style="color:#3730a3;">Resposta:</strong> <span id="ie-resultado">escolha o estado e clique em "Gerar Inscrição Estadual".</span><div id="ie-info" style="margin-top:6px;font-size:0.85rem;color:#475569;"></div></div>
</div>
<script>
(function () {
  var selEstado = document.getElementById('ie-estado');
  var radios = document.getElementsByName('ie-pontuacao');
  var btnGerar = document.getElementById('ie-gerar');
  var btnCopiar = document.getElementById('ie-copiar');
  var btnLimpar = document.getElementById('ie-limpar');
  var caixa = document.getElementById('ie-resposta');
  var resultado = document.getElementById('ie-resultado');
  var info = document.getElementById('ie-info');
  var textoInicial = 'escolha o estado e clique em "Gerar Inscrição Estadual".';
  var ultimo = '';
  var P9 = [9, 8, 7, 6, 5, 4, 3, 2];
  function rnd(n) {
    var s = '';
    while (s.length !== n) { s += String(Math.floor(Math.random() * 10)); }
    return s;
  }
  function rndInt(min, max) { return min + Math.floor(Math.random() * (max - min + 1)); }
  function pad(v, n) {
    var s = String(v);
    while (s.length !== n) { s = '0' + s; }
    return s;
  }
  function dig(s) { return s.split('').map(Number); }
  function soma(s, pesos) {
    var d = dig(s);
    return pesos.reduce(function (acc, p, i) { return acc + p * d[i]; }, 0);
  }
  function dvA(s) { var r = s % 11; return 2 > r ? 0 : 11 - r; }
  function dvB(s) { var d = 11 - (s % 11); return d > 9 ? 0 : d; }
  function entre(n, a, b) { return n >= a ? b >= n : false; }
  function aplicar(num, mask) {
    var i = 0;
    return mask.split('').map(function (c) {
      if (c === '9') { var d = num.charAt(i); i += 1; return d; }
      return c;
    }).join('');
  }
  function dvBA(s, m10) {
    var r = s % (m10 ? 10 : 11);
    if (m10) { return r === 0 ? 0 : 10 - r; }
    return 2 > r ? 0 : 11 - r;
  }
  function mgDv1(base) {
    var t = base.substring(0, 3) + '0' + base.substring(3);
    var total = 0;
    dig(t).forEach(function (n, i) {
      var p = n * (i % 2 === 0 ? 1 : 2);
      total += p > 9 ? p - 9 : p;
    });
    return (10 - (total % 10)) % 10;
  }
  var GERADORES = {
    AC: function () {
      var b = '01' + rnd(9);
      b += dvB(soma(b, [4, 3, 2, 9, 8, 7, 6, 5, 4, 3, 2]));
      b += dvB(soma(b, [5, 4, 3, 2, 9, 8, 7, 6, 5, 4, 3, 2]));
      return [b, '99.999.999/999-99'];
    },
    AL: function () {
      var tipos = [0, 3, 5, 7, 8];
      var b = '24' + tipos[rndInt(0, 4)] + rnd(5);
      var d = (soma(b, P9) * 10) % 11;
      if (d === 10) { d = 0; }
      return [b + d, null];
    },
    AP: function () {
      var b = '03' + rnd(6);
      var n = parseInt(b, 10);
      var p = 0;
      var d = 0;
      if (entre(n, 3000001, 3017000)) { p = 5; d = 0; }
      else if (entre(n, 3017001, 3019022)) { p = 9; d = 1; }
      var dv = 11 - ((p + soma(b, P9)) % 11);
      if (dv === 10) { dv = 0; }
      else if (dv === 11) { dv = d; }
      return [b + dv, null];
    },
    AM: function () {
      var b = '04' + rnd(6);
      var s = soma(b, P9);
      var dv = s > 10 ? dvA(s) : 11 - s;
      return [b + dv, '99.999.999-9'];
    },
    BA: function () {
      var b = rnd(7);
      var m10 = ['0', '1', '2', '3', '4', '5', '8'].indexOf(b.charAt(1)) !== -1;
      var d2 = dvBA(soma(b, [8, 7, 6, 5, 4, 3, 2]), m10);
      var d1 = dvBA(soma(b + d2, [9, 8, 7, 6, 5, 4, 3, 2]), m10);
      return [b + d1 + d2, '9999999-99'];
    },
    CE: function () {
      var b = '06' + rnd(6);
      return [b + dvB(soma(b, P9)), '99999999-9'];
    },
    DF: function () {
      var b = '07' + rnd(9);
      b += dvB(soma(b, [4, 3, 2, 9, 8, 7, 6, 5, 4, 3, 2]));
      b += dvB(soma(b, [5, 4, 3, 2, 9, 8, 7, 6, 5, 4, 3, 2]));
      return [b, '99999999999-99'];
    },
    ES: function () {
      var b = rnd(8);
      return [b + dvA(soma(b, P9)), '999.999.99-9'];
    },
    GO: function () {
      var pref = ['10', '11', '20'];
      var b = pref[rndInt(0, 2)] + rnd(6);
      var r = soma(b, P9) % 11;
      var dv;
      if (r === 0) { dv = 0; }
      else if (r === 1) { dv = entre(parseInt(b, 10), 10103105, 10119997) ? 1 : 0; }
      else { dv = 11 - r; }
      return [b + dv, '99.999.999-9'];
    },
    MA: function () {
      var b = '12' + rnd(6);
      return [b + dvA(soma(b, P9)), null];
    },
    MT: function () {
      var b = rnd(10);
      return [b + dvA(soma(b, [3, 2, 9, 8, 7, 6, 5, 4, 3, 2])), '9999999999-9'];
    },
    MS: function () {
      var b = '28' + rnd(6);
      return [b + dvB(soma(b, P9)), null];
    },
    MG: function () {
      var b = rnd(9) + '00';
      b += mgDv1(b);
      var r = soma(b, [3, 2, 11, 10, 9, 8, 7, 6, 5, 4, 3, 2]) % 11;
      b += (2 > r ? 0 : 11 - r);
      return [b, '999.999.999/9999'];
    },
    PA: function () {
      var b = '15' + rnd(6);
      return [b + dvA(soma(b, P9)), '99-999999-9'];
    },
    PB: function () {
      var b = rnd(8);
      return [b + dvB(soma(b, P9)), '99999999-9'];
    },
    PR: function () {
      var b = rnd(8);
      b += dvA(soma(b, [3, 2, 7, 6, 5, 4, 3, 2]));
      b += dvA(soma(b, [4, 3, 2, 7, 6, 5, 4, 3, 2]));
      return [b, '999.99999-99'];
    },
    PE: function () {
      var b = rnd(7);
      b += dvA(soma(b, [8, 7, 6, 5, 4, 3, 2]));
      b += dvA(soma(b, P9));
      return [b, '9999999-99'];
    },
    PI: function () {
      var b = rnd(8);
      return [b + dvB(soma(b, P9)), null];
    },
    RJ: function () {
      var b = rnd(7);
      return [b + dvA(soma(b, [2, 7, 6, 5, 4, 3, 2])), '99.999.99-9'];
    },
    RN: function () {
      var longo = Math.random() > 0.5;
      var b = '20' + rnd(longo ? 7 : 6);
      var pesos = longo ? [10, 9, 8, 7, 6, 5, 4, 3, 2] : P9;
      var d = (soma(b, pesos) * 10) % 11;
      if (d === 10) { d = 0; }
      return [b + d, longo ? '99.9.999.999-9' : '99.999.999-9'];
    },
    RS: function () {
      var b = pad(rndInt(1, 467), 3) + rnd(6);
      return [b + dvB(soma(b, [2, 9, 8, 7, 6, 5, 4, 3, 2])), '999/9999999'];
    },
    RO: function () {
      var b = rnd(13);
      var d = 11 - (soma(b, [6, 5, 4, 3, 2, 9, 8, 7, 6, 5, 4, 3, 2]) % 11);
      if (d > 9) { d -= 10; }
      return [b + d, '9999999999999-9'];
    },
    RR: function () {
      var b = '24' + rnd(6);
      return [b + (soma(b, [1, 2, 3, 4, 5, 6, 7, 8]) % 9), '99999999-9'];
    },
    SC: function () {
      var b = rnd(8);
      return [b + dvA(soma(b, P9)), '999.999.999'];
    },
    SP: function () {
      var b = rnd(8);
      b += (soma(b, [1, 3, 4, 5, 6, 7, 8, 10]) % 11) % 10;
      b += rnd(2);
      b += (soma(b, [3, 2, 10, 9, 8, 7, 6, 5, 4, 3, 2]) % 11) % 10;
      return [b, '999.999.999.999'];
    },
    SE: function () {
      var b = rnd(8);
      return [b + dvB(soma(b, P9)), '99999999-9'];
    },
    TO: function () {
      var tipos = ['01', '02', '03', '99'];
      var p1 = rnd(2);
      var p3 = rnd(6);
      var d = dvA(soma(p1 + p3, P9));
      return [p1 + tipos[rndInt(0, 3)] + p3 + d, null];
    }
  };
  function pontuado() {
    var sim = true;
    Array.prototype.forEach.call(radios, function (r) {
      if (r.checked) { sim = r.value === 'sim'; }
    });
    return sim;
  }
  function gerar() {
    var res = GERADORES[selEstado.value]();
    var txt = res[0];
    if (pontuado()) {
      if (res[1]) { txt = aplicar(res[0], res[1]); }
    }
    ultimo = txt;
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    resultado.style.fontWeight = '700';
    resultado.style.fontSize = '1.2rem';
    resultado.textContent = txt;
    info.textContent = 'Inscrição Estadual válida para ' + selEstado.options[selEstado.selectedIndex].text + '.';
  }
  function avisoBotao(texto) {
    btnCopiar.textContent = texto;
    setTimeout(function () { btnCopiar.textContent = 'Copiar'; }, 1500);
  }
  function copiar() {
    if (ultimo === '') { avisoBotao('Gere primeiro'); return; }
    var texto = ultimo;
    var ok = function () { avisoBotao('Copiado!'); };
    var alternativa = function () {
      var ta = document.createElement('textarea');
      ta.value = texto;
      ta.style.position = 'fixed';
      ta.style.opacity = '0';
      document.body.appendChild(ta);
      ta.select();
      try { document.execCommand('copy'); ok(); } catch (e) { avisoBotao('Erro ao copiar'); }
      document.body.removeChild(ta);
    };
    if (navigator.clipboard) {
      navigator.clipboard.writeText(texto).then(ok, alternativa);
    } else {
      alternativa();
    }
  }
  function limpar() {
    ultimo = '';
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    resultado.style.color = '#64748b';
    resultado.style.fontWeight = '400';
    resultado.style.fontSize = '1rem';
    resultado.textContent = textoInicial;
    info.textContent = '';
  }
  btnGerar.addEventListener('click', gerar);
  btnCopiar.addEventListener('click', copiar);
  btnLimpar.addEventListener('click', limpar);
  selEstado.addEventListener('focus', function () { selEstado.style.borderColor = '#6366f1'; });
  selEstado.addEventListener('blur', function () { selEstado.style.borderColor = '#c7d2fe'; });
})();
</script>

## Como usar o gerador

1. Em **Qual estado?**, escolha a UF para a qual você precisa da Inscrição Estadual (por exemplo, SP ou MG).
2. Em **Gerar com pontuação?**, marque **Sim** para receber o número com pontos, traços e barras, ou **Não** para receber só os dígitos.
3. Clique em **Gerar Inscrição Estadual**. O número aparece na caixa **Resposta**.
4. Clique em **Copiar** para levar o número para a área de transferência e colar onde precisar.
5. Clique em **Gerar Inscrição Estadual** de novo para obter outro número, ou em **Limpar** para recomeçar.

Cada estado tem sua própria regra de formação, por isso o tamanho e o formato do número mudam conforme a UF escolhida. Alguns estados não têm máscara oficial, e neles o número sai igual com ou sem pontuação. Os números são gerados de forma aleatória e servem para testar sistemas, formulários e cadastros. Eles passam na validação matemática do estado, mas não pertencem a nenhuma empresa real.

## Entendendo os termos

- **Inscrição Estadual (IE):** número de identificação de uma empresa contribuinte de ICMS na Secretaria da Fazenda do seu estado.
- **Contribuinte:** empresa ou pessoa que realiza operações sujeitas ao ICMS, como a venda de mercadorias, e por isso precisa ter Inscrição Estadual.
- **ICMS:** Imposto sobre Circulação de Mercadorias e Serviços, cobrado pelos estados.
- **Estado (UF):** unidade da federação que emite a inscrição. Cada UF segue o seu próprio padrão de numeração.
- **SEFAZ:** Secretaria da Fazenda estadual, órgão que emite e controla as Inscrições Estaduais.
- **Pontuação:** pontos, traços e barras que separam os grupos de dígitos, como em 110.042.490.114. Sem pontuação, o número aparece apenas com os dígitos.
- **Dígito verificador:** último dígito (ou os dois últimos) do número, calculado a partir dos anteriores com uma fórmula própria de cada estado. Ele permite conferir se o número é válido.
- **CNPJ:** cadastro nacional da empresa. A Inscrição Estadual é um registro separado, emitido pelo estado, e uma mesma empresa pode ter uma por estado em que atua.
- **Número válido:** número que respeita a regra de cálculo do estado. Ser válido não significa que ele exista na base da SEFAZ.
- **Dados de teste:** informações fictícias usadas por desenvolvedores, analistas e estudantes para testar sistemas sem usar dados reais.

## Para que serve a Inscrição Estadual gerada

O gerador ajuda a preencher campos de Inscrição Estadual em ambientes de teste, validar máscaras e regras de cadastro e criar massa de dados para sistemas de gestão ou emissão de notas fiscais. Não use os números gerados para fins indevidos: a responsabilidade pelo uso é de quem os utiliza.