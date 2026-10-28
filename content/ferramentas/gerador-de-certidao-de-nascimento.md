---
title: "Gerador de Certidões de Nascimento"
seoTitle: "Gerador de Certidões de Nascimento"
description: "Gerador de Certidões de Nascimento: gere números válidos de certidão de nascimento. Grátis e online, sem cadastro."
summary: "Gere números válidos de certidão de nascimento."
date: 2026-10-28
draft: false
category: "documentos"
tags: ["certidões", "cartório", "gerador", "dados de teste", "documentos"]
keywords: ["gerador de certidões de nascimento", "gerador de certidões de nascimento online", "certidões", "cartório", "gerador"]
---

Basta escolher se quer a pontuação e depois clicar em **Gerar Certidão**.

<div id="calc-certidao" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">📄 Gerador de Certidão de Nascimento</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Escolha a opção e gere um número válido na hora.</p>
<label for="cert-pontuacao" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Gerar com pontuação?</label>
<select id="cert-pontuacao" style="width:100%;padding:12px 14px;margin-bottom:20px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<option value="sim">Sim</option>
<option value="nao">Não</option>
</select>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="cert-gerar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Gerar Certidão</button>
<button type="button" id="cert-copiar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Copiar</button>
<button type="button" id="cert-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="cert-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;word-break:break-all;"><strong style="color:#3730a3;">Resposta:</strong> <span id="cert-resultado">clique em "Gerar Certidão".</span></div>
</div>
<script>
(function () {
  var pont = document.getElementById('cert-pontuacao');
  var resultado = document.getElementById('cert-resultado');
  var caixa = document.getElementById('cert-resposta');
  var botaoCopiar = document.getElementById('cert-copiar');
  var ultimo = '';
  function aleatorio(min, max) { return Math.floor(Math.random() * (max - min + 1)) + min; }
  function zeros(n, tam) { return ('000000000' + n).slice(-tam); }
  function digito(base) {
    var soma = 0;
    var mult = 32 - base.length;
    var i = 0;
    while (i !== base.length) {
      soma += Number(base.charAt(i)) * mult;
      mult++;
      if (mult > 10) { mult = 0; }
      i++;
    }
    var dv = soma % 11;
    return dv === 10 ? 1 : dv;
  }
  function montar() {
    var ano = new Date().getFullYear();
    var base = zeros(aleatorio(100000, 999999), 6) + '01' + '55' + zeros(aleatorio(2000, ano), 4) + '1' + zeros(aleatorio(1, 99999), 5) + zeros(aleatorio(1, 299), 3) + zeros(aleatorio(1, 9999999), 7);
    var d1 = digito(base);
    var d2 = digito(base + String(d1));
    var dv = String(d1) + String(d2);
    if (pont.value === 'sim') {
      return [base.slice(0, 6), base.slice(6, 8), base.slice(8, 10), base.slice(10, 14), base.slice(14, 15), base.slice(15, 20), base.slice(20, 23), base.slice(23, 30)].join('.') + '-' + dv;
    }
    return base + dv;
  }
  function mostrar() {
    ultimo = montar();
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    resultado.style.fontWeight = '700';
    resultado.style.fontFamily = 'ui-monospace,SFMono-Regular,Menlo,Consolas,monospace';
    resultado.textContent = ultimo;
    botaoCopiar.textContent = 'Copiar';
  }
  function copiar() {
    if (ultimo === '') { return; }
    var feito = function () { botaoCopiar.textContent = 'Copiado!'; };
    var alternativo = function () {
      var t = document.createElement('textarea');
      t.value = ultimo;
      t.style.position = 'fixed';
      t.style.opacity = '0';
      document.body.appendChild(t);
      t.select();
      try { document.execCommand('copy'); feito(); } catch (e) { botaoCopiar.textContent = 'Erro'; }
      document.body.removeChild(t);
    };
    if (navigator.clipboard && navigator.clipboard.writeText) {
      navigator.clipboard.writeText(ultimo).then(feito, alternativo);
    } else {
      alternativo();
    }
  }
  function limpar() {
    ultimo = '';
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    resultado.style.color = '#64748b';
    resultado.style.fontWeight = 'normal';
    resultado.style.fontFamily = 'inherit';
    resultado.textContent = 'clique em "Gerar Certidão".';
    botaoCopiar.textContent = 'Copiar';
  }
  document.getElementById('cert-gerar').addEventListener('click', mostrar);
  botaoCopiar.addEventListener('click', copiar);
  document.getElementById('cert-limpar').addEventListener('click', limpar);
  pont.addEventListener('change', function () { if (ultimo !== '') { mostrar(); } });
  pont.addEventListener('focus', function () { pont.style.borderColor = '#6366f1'; });
  pont.addEventListener('blur', function () { pont.style.borderColor = '#c7d2fe'; });
})();
</script>

## Como usar o gerador

1. Escolha no campo **Gerar com pontuação?** se o número deve sair com pontos e hífen (**Sim**) ou só com dígitos (**Não**).
2. Clique em **Gerar Certidão** para criar um novo número de certidão de nascimento.
3. Clique em **Copiar** para levar o número para a área de transferência.
4. Use o botão **Limpar** para apagar o resultado e começar de novo.

Cada clique em **Gerar Certidão** cria um número diferente. Se você mudar a opção de pontuação depois de gerar, o número é gerado de novo no novo formato.

## Entendendo os termos

- **Certidão de nascimento:** documento emitido pelo cartório que comprova o registro de uma pessoa e é a base para os demais documentos civis.
- **Número da certidão (matrícula):** código de 32 dígitos que identifica o registro de forma única em todo o país.
- **Pontuação:** pontos e hífen usados para separar as partes do número, como em 000000.00.00.0000.0.00000.000.0000000-00.
- **Código do cartório:** os 6 primeiros dígitos, que identificam o cartório onde o registro foi feito.
- **Acervo:** 2 dígitos que indicam o acervo do cartório em que o registro está guardado.
- **Serviço de registro civil:** 2 dígitos que indicam o tipo de serviço prestado pelo cartório (registro civil das pessoas naturais).
- **Ano de registro:** 4 dígitos com o ano em que o registro foi lavrado.
- **Tipo de livro:** 1 dígito que indica o tipo do registro. Nas certidões de nascimento, o valor é 1.
- **Livro, folha e termo:** posição exata do registro dentro do cartório. O livro tem 5 dígitos, a folha tem 3 e o termo tem 7.
- **Dígitos verificadores:** os 2 últimos dígitos, calculados a partir dos anteriores para conferir se o número segue a regra de formação.
- **Dados de teste:** números fictícios usados por estudantes, programadores e testadores para validar sistemas e formulários.

**Importante:** os números são gerados de forma aleatória, respeitando a regra de formação, e servem apenas para testes de software. Eles não correspondem a registros reais, e o uso indevido é de responsabilidade de quem os utiliza.