---
title: "Gerador de Certidões de Nascimento, Casamento e Óbito"
seoTitle: "Gerador de Certidões de Nascimento, Casamento e Óbito"
description: "Gerador de Certidões de Nascimento, Casamento e Óbito: gere números de certidão de nascimento, casamento e óbito. Grátis e online, sem cadastro."
summary: "Gere números de certidão de nascimento, casamento e óbito."
date: 2026-10-29
draft: false
category: "documentos"
tags: ["certidões", "cartório", "gerador", "dados de teste", "documentos"]
keywords: ["gerador de certidões de nascimento, casamento e óbito", "gerador de certidões de nascimento, casamento e óbito online", "certidões", "cartório", "gerador"]
---
<!--INI SUDAH DIKERJAKAN-->

Escolha o tipo de certidão, defina se quer o número com pontuação e depois clique em **Gerar Certidão**.

<div id="gerador-certidoes" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">📄 Gerador de Certidões</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Selecione as opções e gere um número de certidão na hora.</p>
<span style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">1. Gerar com Pontuação?</span>
<div style="display:flex;gap:20px;flex-wrap:wrap;margin-bottom:16px;">
<label for="cert-pontos-sim" style="display:inline-flex;align-items:center;gap:8px;font-size:1rem;cursor:pointer;"><input type="radio" id="cert-pontos-sim" name="cert-pontos" checked style="width:18px;height:18px;accent-color:#4f46e5;cursor:pointer;">Sim</label>
<label for="cert-pontos-nao" style="display:inline-flex;align-items:center;gap:8px;font-size:1rem;cursor:pointer;"><input type="radio" id="cert-pontos-nao" name="cert-pontos" style="width:18px;height:18px;accent-color:#4f46e5;cursor:pointer;">Não</label>
</div>
<label for="cert-tipo" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">2. Qual certidão?</label>
<select id="cert-tipo" style="width:100%;padding:12px 14px;margin-bottom:20px;font-size:1rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;">
<option value="0">Indiferente</option>
<option value="1">Nascimento</option>
<option value="2">Casamento</option>
<option value="3">Casamento Efeito Religioso</option>
<option value="4">Óbito</option>
</select>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="cert-gerar" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Gerar Certidão</button>
<button type="button" id="cert-copiar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Copiar</button>
<button type="button" id="cert-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="cert-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Certidão Gerada:</strong> <span id="cert-resultado">selecione as opções e clique em "Gerar Certidão".</span></div>
</div>
<script>
(function () {
  var tipo = document.getElementById('cert-tipo');
  var comPontos = document.getElementById('cert-pontos-sim');
  var resultado = document.getElementById('cert-resultado');
  var caixa = document.getElementById('cert-resposta');
  var btnCopiar = document.getElementById('cert-copiar');
  var textoInicial = 'selecione as opções e clique em "Gerar Certidão".';
  var nomes = { '1': 'Nascimento', '2': 'Casamento', '3': 'Casamento Efeito Religioso', '4': 'Óbito' };
  var ultimo = '';
  function rnd(min, max) { return Math.floor(Math.random() * (max - min + 1)) + min; }
  function pad(n, tam) { return String(n).padStart(tam, '0'); }
  function dv(base, pesoInicial) {
    var soma = 0;
    var peso = pesoInicial;
    for (var i = 0; i !== base.length; i++) {
      soma += Number(base.charAt(i)) * peso;
      peso = (peso === 10) ? 0 : peso + 1;
    }
    var resto = soma % 11;
    return (resto === 10) ? 1 : resto;
  }
  function aviso(msg) {
    caixa.style.borderColor = '#fca5a5';
    caixa.style.background = '#fef2f2';
    resultado.style.color = '#b91c1c';
    resultado.textContent = msg;
  }
  function mostrar(numero, nomeTipo) {
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    resultado.textContent = '';
    var forte = document.createElement('strong');
    forte.style.cssText = 'font-size:1.15rem;font-family:ui-monospace,SFMono-Regular,Menlo,Consolas,monospace;word-break:break-all;';
    forte.textContent = numero;
    var quebra = document.createElement('br');
    var pequeno = document.createElement('small');
    pequeno.style.color = '#475569';
    pequeno.textContent = 'Tipo: ' + nomeTipo;
    resultado.appendChild(forte);
    resultado.appendChild(quebra);
    resultado.appendChild(pequeno);
    ultimo = numero;
  }
  function gerar() {
    var t = tipo.value;
    if (t === '0') { t = String(rnd(1, 4)); }
    var partes = [
      String(rnd(100000, 999999)),
      '01',
      '55',
      String(rnd(2010, new Date().getFullYear())),
      t,
      pad(rnd(1, 300), 5),
      pad(rnd(1, 300), 3),
      pad(rnd(1, 9999999), 7)
    ];
    var base = partes.join('');
    var d1 = dv(base, 2);
    var d2 = dv(base + String(d1), 1);
    var digitos = String(d1) + String(d2);
    var numero = comPontos.checked ? partes.join('.') + '-' + digitos : base + digitos;
    mostrar(numero, nomes[t]);
  }
  function copiarFallback() {
    var area = document.createElement('textarea');
    area.value = ultimo;
    area.style.position = 'fixed';
    area.style.opacity = '0';
    document.body.appendChild(area);
    area.select();
    try { document.execCommand('copy'); } catch (e) {}
    document.body.removeChild(area);
    copiado();
  }
  function copiado() {
    btnCopiar.textContent = 'Copiado!';
    setTimeout(function () { btnCopiar.textContent = 'Copiar'; }, 1500);
  }
  function copiar() {
    if (ultimo === '') { aviso('gere uma certidão primeiro para copiar.'); return; }
    try {
      navigator.clipboard.writeText(ultimo).then(copiado, copiarFallback);
    } catch (e) {
      copiarFallback();
    }
  }
  function limpar() {
    comPontos.checked = true;
    tipo.value = '0';
    ultimo = '';
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    resultado.style.color = '#64748b';
    resultado.textContent = textoInicial;
  }
  document.getElementById('cert-gerar').addEventListener('click', gerar);
  btnCopiar.addEventListener('click', copiar);
  document.getElementById('cert-limpar').addEventListener('click', limpar);
  tipo.addEventListener('focus', function () { tipo.style.borderColor = '#6366f1'; });
  tipo.addEventListener('blur', function () { tipo.style.borderColor = '#c7d2fe'; });
})();
</script>

## Como usar o gerador

1. Em **Gerar com Pontuação?**, escolha **Sim** para o número sair com pontos e hífen ou **Não** para sair só com os 32 dígitos.
2. Em **Qual certidão?**, selecione Nascimento, Casamento, Casamento Efeito Religioso ou Óbito. Se escolher **Indiferente**, o gerador sorteia um dos quatro tipos.
3. Clique em **Gerar Certidão** para criar um novo número. Cada clique gera um número diferente.
4. Clique em **Copiar** para levar o número para a área de transferência.
5. Use o botão **Limpar** para voltar às opções iniciais.

Os números são gerados de forma aleatória, respeitando as regras de formação da matrícula, inclusive o cálculo dos dígitos verificadores. Eles servem para estudantes, programadores, analistas e testadores que precisam de dados de teste em sistemas em desenvolvimento. Não correspondem a registros reais, e a má utilização dos dados gerados é de total responsabilidade do usuário.

## Entendendo os termos

- **Certidão:** documento emitido pelo cartório de registro civil que comprova um fato da vida civil, como nascimento, casamento ou óbito.
- **Matrícula:** número único de 32 dígitos que identifica o registro em uma certidão, no padrão definido pelo CNJ.
- **Certidão de nascimento:** comprova o nascimento de uma pessoa. Usa o tipo de livro 1.
- **Certidão de casamento:** comprova o casamento civil. Usa o tipo de livro 2.
- **Casamento Efeito Religioso:** certidão de casamento religioso com efeito civil, quando a cerimônia religiosa é registrada para valer também perante a lei. Usa o tipo de livro 3.
- **Certidão de óbito:** comprova o falecimento de uma pessoa. Usa o tipo de livro 4.
- **Indiferente:** opção que deixa o gerador escolher aleatoriamente o tipo da certidão.
- **Pontuação:** pontos e hífen que separam os grupos do número, como em `104539.01.55.2013.1.00012.021.0000123-21`. Sem pontuação, o número fica só com os 32 dígitos seguidos.
- **Código da serventia:** os 6 primeiros dígitos, que identificam o cartório que fez o registro.
- **Código do acervo:** 2 dígitos que indicam o acervo do cartório. O valor 01 é o acervo próprio.
- **Código do serviço (55):** 2 dígitos fixos que indicam o serviço de registro civil das pessoas naturais.
- **Ano do registro:** 4 dígitos com o ano em que o ato foi registrado.
- **Tipo de livro:** 1 dígito que indica o livro do registro (nascimento, casamento, casamento religioso com efeito civil ou óbito).
- **Número do livro:** 5 dígitos que identificam o livro dentro do cartório.
- **Número da folha:** 3 dígitos que indicam a folha do livro onde está o registro.
- **Número do termo:** 7 dígitos que identificam o registro dentro do livro.
- **Dígito verificador (DV):** os 2 últimos dígitos, calculados a partir dos 30 anteriores. Servem para detectar erros de digitação e confirmar que o número está bem formado.
- **Dados de teste:** informações fictícias usadas para testar sistemas sem depender de documentos reais.