---
title: "Gerador de Certidões de Óbito"
seoTitle: "Gerador de Certidões de Óbito"
description: "Gerador de Certidões de Óbito: gere números válidos de certidão de óbito. Grátis e online, sem cadastro."
summary: "Gere números válidos de certidão de óbito."
date: 2026-10-29
draft: false
category: "documentos"
tags: ["certidões", "cartório", "gerador", "dados de teste", "documentos"]
keywords: ["gerador de certidões de óbito", "gerador de certidões de óbito online", "certidões", "cartório", "gerador"]
---

Basta escolher se o número deve ter pontuação e depois clicar em **Gerar Certidão**.

<div id="gerador-obito" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">📄 Gerador de Certidões de Óbito</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Escolha a opção e gere um número válido na hora.</p>
<span style="display:block;margin-bottom:8px;font-weight:600;font-size:0.95rem;">Gerar com pontuação?</span>
<div style="display:flex;gap:20px;margin-bottom:20px;padding:12px 14px;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;box-sizing:border-box;">
<label for="obt-pontos-sim" style="display:inline-flex;align-items:center;gap:8px;font-size:1rem;cursor:pointer;"><input type="radio" id="obt-pontos-sim" name="obt-pontos" value="sim" checked style="width:18px;height:18px;margin:0;accent-color:#4f46e5;cursor:pointer;">Sim</label>
<label for="obt-pontos-nao" style="display:inline-flex;align-items:center;gap:8px;font-size:1rem;cursor:pointer;"><input type="radio" id="obt-pontos-nao" name="obt-pontos" value="nao" style="width:18px;height:18px;margin:0;accent-color:#4f46e5;cursor:pointer;">Não</label>
</div>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="obt-gerar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Gerar Certidão</button>
<button type="button" id="obt-copiar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Copiar</button>
<button type="button" id="obt-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="obt-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Certidão gerada:</strong> <span id="obt-resultado" style="word-break:break-all;">clique em "Gerar Certidão".</span></div>
</div>
<script>
(function () {
  var resultado = document.getElementById('obt-resultado');
  var caixa = document.getElementById('obt-resposta');
  var botaoCopiar = document.getElementById('obt-copiar');
  var textoPadrao = 'clique em "Gerar Certidão".';
  var ultimo = '';
  function aleatorio(min, max) {
    return Math.floor(Math.random() * (max - min + 1)) + min;
  }
  function zeros(n, tam) {
    return ('0000000000' + String(n)).slice(-tam);
  }
  function digito(base) {
    var soma = 0;
    var mult = 32 - base.length;
    for (var i = 0; i !== base.length; i++) {
      soma += Number(base.charAt(i)) * mult;
      mult = (mult + 1) % 11;
    }
    var resto = soma % 11;
    return resto === 10 ? 1 : resto;
  }
  function gerar() {
    var anoAtual = new Date().getFullYear();
    var base = zeros(aleatorio(100000, 999999), 6) +
      '01' +
      '55' +
      String(aleatorio(2010, anoAtual)) +
      '4' +
      zeros(aleatorio(1, 99999), 5) +
      zeros(aleatorio(1, 300), 3) +
      zeros(aleatorio(1, 9999999), 7);
    var d1 = digito(base);
    var d2 = digito(base + String(d1));
    var dv = String(d1) + String(d2);
    var comPontos = document.getElementById('obt-pontos-sim').checked;
    var numero;
    if (comPontos) {
      numero = base.slice(0, 6) + '.' + base.slice(6, 8) + '.' + base.slice(8, 10) + '.' + base.slice(10, 14) + '.' + base.slice(14, 15) + '.' + base.slice(15, 20) + '.' + base.slice(20, 23) + '.' + base.slice(23, 30) + '-' + dv;
    } else {
      numero = base + dv;
    }
    ultimo = numero;
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    resultado.style.fontFamily = 'ui-monospace,SFMono-Regular,Menlo,Consolas,monospace';
    resultado.style.fontWeight = '700';
    resultado.style.fontSize = '1.05rem';
    resultado.textContent = numero;
  }
  function copiarFallback(texto) {
    var campo = document.createElement('textarea');
    campo.value = texto;
    campo.setAttribute('readonly', '');
    campo.style.position = 'fixed';
    campo.style.opacity = '0';
    document.body.appendChild(campo);
    campo.select();
    try { document.execCommand('copy'); } catch (e) {}
    document.body.removeChild(campo);
  }
  function avisoCopiado() {
    botaoCopiar.textContent = 'Copiado!';
    setTimeout(function () { botaoCopiar.textContent = 'Copiar'; }, 1500);
  }
  function copiar() {
    if (ultimo === '') { return; }
    if (navigator.clipboard) {
      if (navigator.clipboard.writeText) {
        navigator.clipboard.writeText(ultimo).then(avisoCopiado, function () {
          copiarFallback(ultimo);
          avisoCopiado();
        });
        return;
      }
    }
    copiarFallback(ultimo);
    avisoCopiado();
  }
  function limpar() {
    ultimo = '';
    document.getElementById('obt-pontos-sim').checked = true;
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    resultado.style.color = '#64748b';
    resultado.style.fontFamily = 'inherit';
    resultado.style.fontWeight = '400';
    resultado.style.fontSize = 'inherit';
    resultado.textContent = textoPadrao;
  }
  document.getElementById('obt-gerar').addEventListener('click', gerar);
  botaoCopiar.addEventListener('click', copiar);
  document.getElementById('obt-limpar').addEventListener('click', limpar);
})();
</script>

## Como usar o gerador

1. Em **Gerar com pontuação?**, escolha **Sim** para o número separado por pontos e hífen ou **Não** para apenas os 32 dígitos seguidos.
2. Clique em **Gerar Certidão**. Um novo número de certidão de óbito aparece na caixa de resultado.
3. Clique em **Copiar** para levar o número para a área de transferência e colar onde precisar.
4. Clique em **Gerar Certidão** novamente para criar outro número, ou em **Limpar** para voltar ao estado inicial.

Os números são gerados de forma aleatória, seguindo a estrutura e o cálculo dos dígitos verificadores da matrícula de certidões. Eles servem para **testes de software** (formulários, validações e bancos de dados de desenvolvimento) e não correspondem a registros reais de cartório. O uso indevido dos dados gerados é de responsabilidade de quem os utiliza.

## Entendendo os termos

- **Certidão de óbito:** documento emitido pelo cartório de Registro Civil que comprova o falecimento de uma pessoa.
- **Matrícula:** número único de 32 dígitos que identifica a certidão. É o número gerado por esta ferramenta.
- **Código da serventia:** os 6 primeiros dígitos, que identificam o cartório responsável pelo registro.
- **Acervo:** 2 dígitos que indicam o acervo do cartório. O valor 01 representa o acervo próprio.
- **Serviço:** 2 dígitos que indicam o tipo de serviço. O código 55 corresponde ao Registro Civil das Pessoas Naturais.
- **Ano de registro:** 4 dígitos com o ano em que o registro foi feito.
- **Tipo de livro:** 1 dígito que indica o livro do registro. Para óbito, o valor é 4 (Livro C).
- **Livro:** 5 dígitos com o número do livro em que o registro foi lançado.
- **Folha:** 3 dígitos com o número da folha dentro do livro.
- **Termo:** 7 dígitos com o número do registro (termo) dentro do livro.
- **Dígitos verificadores:** os 2 últimos dígitos, calculados a partir dos 30 anteriores pelo módulo 11. Servem para detectar erros de digitação.
- **Pontuação:** pontos e hífen usados para separar os blocos do número e facilitar a leitura.
- **Dados de teste:** informações fictícias, mas com formato válido, usadas por estudantes, programadores e analistas para testar sistemas.

## Estrutura do número

A matrícula tem 32 dígitos, divididos em blocos:

**CCCCCC.AA.SS.AAAA.T.LLLLL.FFF.TTTTTTT-DD**

| Bloco | Dígitos | Significado |
| --- | --- | --- |
| CCCCCC | 6 | Código da serventia |
| AA | 2 | Acervo |
| SS | 2 | Serviço |
| AAAA | 4 | Ano de registro |
| T | 1 | Tipo de livro (4 = óbito) |
| LLLLL | 5 | Livro |
| FFF | 3 | Folha |
| TTTTTTT | 7 | Termo |
| DD | 2 | Dígitos verificadores |

## Exemplo

Número com pontuação: **123456.01.55.2024.4.00012.021.0000123-19**

1. Serventia 123456, acervo 01 e serviço 55.
2. Registro feito em 2024, no livro tipo 4 (óbito).
3. Livro 00012, folha 021 e termo 0000123.
4. Os dígitos verificadores 19 fecham o número.

Sem pontuação, o mesmo número fica: **12345601552024400012021000012319**