---
title: "Não Seguidores no Instagram"
seoTitle: "Não Seguidores no Instagram"
description: "Não Seguidores no Instagram: veja quem você segue no Instagram e não segue você de volta. Grátis e online, sem cadastro."
summary: "Veja quem você segue no Instagram e não segue você de volta."
date: 2026-11-05
draft: false
category: "social"
tags: ["instagram", "seguidores", "redes sociais"]
keywords: ["não seguidores no instagram", "não seguidores no instagram online", "instagram", "seguidores", "redes sociais"]
---

Envie os arquivos de **seguidores** e **seguindo** exportados do Instagram (ou cole os nomes de usuário) e clique em **Ver Não Seguidores**. Você não precisa informar login nem senha.

<div id="calc-nao-seguidores" style="max-width:480px;margin:24px 0;padding:24px;background:linear-gradient(135deg,#f8fafc 0%,#eef2ff 100%);border:1px solid #c7d2fe;border-radius:16px;box-shadow:0 8px 24px rgba(79,70,229,0.12);font-family:system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;color:#1e293b;box-sizing:border-box;">
<h2 style="margin:0 0 4px;font-size:1.25rem;color:#3730a3;">👥 Não Seguidores no Instagram</h2>
<p style="margin:0 0 18px;font-size:0.9rem;color:#64748b;">Descubra quem você segue e não segue você de volta.</p>
<label for="ins-seg-arquivo" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Seguidores (arquivo)</label>
<input id="ins-seg-arquivo" type="file" accept=".json,.html,.htm,.txt" multiple style="width:100%;padding:10px 12px;margin-bottom:10px;font-size:0.9rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;">
<label for="ins-seg-texto" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Seguidores (ou cole os nomes)</label>
<textarea id="ins-seg-texto" rows="3" placeholder="Ex.: maria, joao.silva, @ana_souza" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:16px;font-size:1rem;font-family:inherit;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;resize:vertical;"></textarea>
<label for="ins-sig-arquivo" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Seguindo (arquivo)</label>
<input id="ins-sig-arquivo" type="file" accept=".json,.html,.htm,.txt" multiple style="width:100%;padding:10px 12px;margin-bottom:10px;font-size:0.9rem;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;">
<label for="ins-sig-texto" style="display:block;margin-bottom:6px;font-weight:600;font-size:0.95rem;">Seguindo (ou cole os nomes)</label>
<textarea id="ins-sig-texto" rows="3" placeholder="Ex.: maria, pedro_99, @loja.oficial" autocomplete="off" style="width:100%;padding:12px 14px;margin-bottom:20px;font-size:1rem;font-family:inherit;border:2px solid #c7d2fe;border-radius:10px;background:#ffffff;color:#1e293b;box-sizing:border-box;outline:none;resize:vertical;"></textarea>
<div style="display:flex;gap:10px;flex-wrap:wrap;">
<button type="button" id="ins-calcular" style="flex:1;min-width:140px;padding:13px 18px;font-size:1rem;font-weight:700;color:#ffffff;background:linear-gradient(135deg,#4f46e5,#6366f1);border:none;border-radius:10px;cursor:pointer;box-shadow:0 4px 12px rgba(79,70,229,0.35);">Ver Não Seguidores</button>
<button type="button" id="ins-limpar" style="padding:13px 18px;font-size:1rem;font-weight:600;color:#4f46e5;background:#ffffff;border:2px solid #c7d2fe;border-radius:10px;cursor:pointer;">Limpar</button>
</div>
<div id="ins-resposta" aria-live="polite" style="margin-top:20px;padding:16px;background:#ffffff;border:2px dashed #c7d2fe;border-radius:12px;color:#64748b;font-size:1rem;line-height:1.6;"><strong style="color:#3730a3;">Resposta:</strong> <span id="ins-resultado">envie os arquivos (ou cole os nomes) e clique em "Ver Não Seguidores".</span></div>
</div>
<script>
(function () {
  var segArq = document.getElementById('ins-seg-arquivo');
  var segTxt = document.getElementById('ins-seg-texto');
  var sigArq = document.getElementById('ins-sig-arquivo');
  var sigTxt = document.getElementById('ins-sig-texto');
  var resultado = document.getElementById('ins-resultado');
  var caixa = document.getElementById('ins-resposta');
  var padrao = 'envie os arquivos (ou cole os nomes) e clique em "Ver Não Seguidores".';
  var reLink = /instagram\.com\/(?:_u\/)?([A-Za-z0-9._]+)/i;
  function fmt(n) { return n.toLocaleString('pt-BR'); }
  function addUser(set, nome) {
    var n = String(nome).trim().replace(/^@/, '').toLowerCase();
    if (n && /^[a-z0-9._]+$/.test(n)) { set[n] = true; }
  }
  function fromText(texto, set) {
    String(texto).split(/[\s,;]+/).forEach(function (p) {
      var m = p.match(reLink);
      addUser(set, m ? m[1] : p);
    });
  }
  function fromHtml(texto, set) {
    var doc = new DOMParser().parseFromString(texto, 'text/html');
    Array.prototype.forEach.call(doc.querySelectorAll('a'), function (a) {
      var m = (a.getAttribute('href') || '').match(reLink);
      if (m) { addUser(set, m[1]); }
    });
  }
  function walk(o, set) {
    if (Array.isArray(o)) {
      o.forEach(function (i) { walk(i, set); });
      return;
    }
    if (o !== null && typeof o === 'object') {
      if (Array.isArray(o.string_list_data)) {
        var achou = false;
        o.string_list_data.forEach(function (s) {
          if (s && s.value) { addUser(set, s.value); achou = true; }
        });
        if (!achou && o.title) { addUser(set, o.title); }
        return;
      }
      Object.keys(o).forEach(function (k) { walk(o[k], set); });
    }
  }
  function parseArquivo(texto, set) {
    var t = String(texto).trim();
    var c = t.charAt(0);
    if (c === '{' || c === '[') {
      try { walk(JSON.parse(t), set); return; } catch (e) { }
    }
    if (t.indexOf('href') !== -1) { fromHtml(t, set); return; }
    fromText(t, set);
  }
  function readFiles(input, set, done) {
    var files = input.files;
    if (!files || files.length === 0) { done(); return; }
    var pendentes = files.length;
    function fim() {
      pendentes -= 1;
      if (pendentes === 0) { done(); }
    }
    Array.prototype.forEach.call(files, function (f) {
      var r = new FileReader();
      r.onload = function () { parseArquivo(r.result, set); fim(); };
      r.onerror = function () { fim(); };
      r.readAsText(f);
    });
  }
  function erro(msg) {
    caixa.style.borderColor = '#fca5a5';
    caixa.style.background = '#fef2f2';
    resultado.style.color = '#b91c1c';
    resultado.textContent = msg;
  }
  function mostrar(nao, totalSeg, totalSig) {
    caixa.style.borderColor = '#86efac';
    caixa.style.background = '#f0fdf4';
    resultado.style.color = '#166534';
    resultado.textContent = '';
    var resumo = document.createElement('div');
    resumo.textContent = 'Você segue ' + fmt(totalSig) + ' perfis e tem ' + fmt(totalSeg) + ' seguidores. ';
    var forte = document.createElement('strong');
    forte.setAttribute('style', 'font-size:1.2rem;');
    forte.textContent = fmt(nao.length) + (nao.length === 1 ? ' perfil não segue' : ' perfis não seguem') + ' você de volta.';
    resumo.appendChild(forte);
    resultado.appendChild(resumo);
    if (nao.length === 0) { return; }
    var lista = document.createElement('div');
    lista.setAttribute('style', 'max-height:320px;overflow:auto;margin-top:12px;');
    nao.forEach(function (u) {
      var a = document.createElement('a');
      a.href = 'https://www.instagram.com/' + u + '/';
      a.target = '_blank';
      a.rel = 'noopener noreferrer';
      a.textContent = '@' + u;
      a.setAttribute('style', 'display:block;padding:8px 10px;margin-bottom:6px;background:#eef2ff;border-radius:8px;color:#3730a3;text-decoration:none;font-weight:600;font-size:0.95rem;');
      lista.appendChild(a);
    });
    resultado.appendChild(lista);
  }
  function calcular() {
    var seg = {};
    var sig = {};
    readFiles(segArq, seg, function () {
      readFiles(sigArq, sig, function () {
        fromText(segTxt.value, seg);
        fromText(sigTxt.value, sig);
        var listaSeg = Object.keys(seg);
        var listaSig = Object.keys(sig);
        if (listaSeg.length === 0 || listaSig.length === 0) {
          erro('informe as duas listas: quem segue você e quem você segue.');
          return;
        }
        var nao = listaSig.filter(function (u) { return !seg[u]; }).sort();
        mostrar(nao, listaSeg.length, listaSig.length);
      });
    });
  }
  function limpar() {
    segArq.value = '';
    sigArq.value = '';
    segTxt.value = '';
    sigTxt.value = '';
    caixa.style.borderColor = '#c7d2fe';
    caixa.style.background = '#ffffff';
    resultado.style.color = '#64748b';
    resultado.textContent = padrao;
    segTxt.focus();
  }
  document.getElementById('ins-calcular').addEventListener('click', calcular);
  document.getElementById('ins-limpar').addEventListener('click', limpar);
  [segTxt, sigTxt].forEach(function (el) {
    el.addEventListener('focus', function () { el.style.borderColor = '#6366f1'; });
    el.addEventListener('blur', function () { el.style.borderColor = '#c7d2fe'; });
  });
})();
</script>

## Como usar a ferramenta

1. No aplicativo do Instagram, peça a exportação dos seus dados: abra **Configurações** > **Central de Contas** > **Suas informações e permissões** > **Exportar suas informações** > **Criar exportação**. Escolha **Exportar para o dispositivo**, marque **Seguidores e seguindo** e selecione o formato **JSON** (os nomes dos menus podem variar conforme a versão do app).
2. Quando o Instagram avisar que o arquivo está pronto, baixe e descompacte o ZIP.
3. No campo **Seguidores (arquivo)**, envie o arquivo `followers_1.json` (se houver mais de um, como `followers_2.json`, selecione todos).
4. No campo **Seguindo (arquivo)**, envie o arquivo `following.json`.
5. Clique em **Ver Não Seguidores** para ver a lista de perfis que você segue e que não seguem você de volta.
6. Use o botão **Limpar** para apagar tudo e fazer uma nova consulta.

Se preferir, em vez de enviar arquivos, você pode colar os nomes de usuário nos campos de texto, separados por espaço, vírgula ou quebra de linha. Os arquivos em formato HTML também são aceitos. Todo o processamento acontece no seu navegador: nenhum dado é enviado ou salvo em servidores, e a ferramenta nunca pede sua senha.

## Entendendo os termos

- **Seguidor:** perfil que acompanha as suas publicações no Instagram.
- **Seguindo:** perfil que você acompanha, ou seja, aquele que você escolheu seguir.
- **Não seguidor:** perfil que você segue, mas que não segue você de volta. É o resultado mostrado pela ferramenta.
- **Nome de usuário:** identificador único do perfil, que vem depois do @ (por exemplo, @maria.silva). Não diferencia maiúsculas de minúsculas.
- **Exportação de dados:** recurso oficial do Instagram que gera um arquivo com as informações da sua conta, incluindo as listas de seguidores e de quem você segue.
- **JSON:** formato de arquivo de texto estruturado usado pelo Instagram na exportação. É o mais indicado para esta ferramenta.
- **HTML:** formato alternativo da exportação, que abre como uma página no navegador. Também pode ser enviado.
- **Processamento local:** os dados são comparados no próprio navegador, sem passar por nenhum servidor.