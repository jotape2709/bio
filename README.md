# Ler antes de calcular · página de links

Página de links autoral do livro **Ler antes de calcular**, de João Pedro (jotape.exp).
O endereço desta página vai impresso no livro via QR code; os links internos podem mudar à vontade.

- Um único `index.html`, sem build: HTML + CSS + um pouco de JS.
- Identidade jotape.exp: fundo carvão, violeta e lilás, Latin Modern Roman e o quadrado de (a + b)².
- Motion design com [GSAP 3.15](https://gsap.com) (auto-hospedado), respeitando "reduzir movimento".

## Estrutura

```
index.html                 página completa (links no topo do arquivo)
vercel.json                cache e cabeçalhos de segurança
assets/fonts/              Latin Modern Roman em WOFF2 (subconjuntos) + licença GUST
assets/vendor/             gsap-3.15.0.min.js
assets/img/                favicon.svg, apple-touch-icon.png, og.jpg (prévia do WhatsApp)
```

## Editar os links

Abra `index.html`. O bloco `LINKS` é a primeira coisa do arquivo:

```js
const SITE = 'https://jotape-exp.vercel.app';

const LINKS = Object.freeze({
  whatsapp:    'https://chat.whatsapp.com/…',  // Grupo do WhatsApp
  site:        SITE + '/',
  livro:       SITE + '/livros',
  // …
});
```

- **Convite do WhatsApp redefinido?** Troque só a linha `whatsapp`, faça commit e push. A Vercel publica em segundos.
- **Domínio do site mudou?** Troque só `SITE`; as páginas internas acompanham.
- Use sempre `https://`. Um link vazio ou inválido esconde o item, sem quebrar a página.
- Os textos dos botões ficam no HTML, logo abaixo, marcados com `data-link="chave"`.

## Publicar na Vercel

1. Em [vercel.com/new](https://vercel.com/new), importe este repositório.
2. **Project Name:** `ler-antes-de-calcular` (gera `https://ler-antes-de-calcular.vercel.app`).
3. **Framework Preset:** `Other`. Deixe Build Command e Output Directory vazios.
4. Deploy.

Se a Vercel não aceitar esse nome (ou você usar um domínio próprio), troque o endereço nas
**4 linhas marcadas** no `<head>` do `index.html` (`canonical`, `og:url`, `og:image`, `twitter:image`).
Sem isso, a prévia do link no WhatsApp fica sem imagem.

## QR code impresso: o endereço nunca pode mudar

- Gere o QR **depois** do primeiro deploy, a partir do endereço final, e teste-o em mais de um celular.
- O subdomínio `*.vercel.app` pertence ao projeto: não renomeie nem apague o projeto na Vercel.
  Um **domínio próprio** (ex.: `jotape.com.br`) é a opção mais segura a longo prazo, desde que renovado.
- Não use encurtadores de terceiros: se o serviço sair do ar, o QR impresso morre junto.
- Impressão: módulos escuros sobre fundo claro (QR invertido falha em alguns leitores),
  correção de erro M ou Q, pelo menos 2 cm de lado e margem branca de 4 módulos.

## Motion design

- **Entrada:** a figura se constrói como uma prova sem palavras (contorno → a² → 2ab → b²), com
  cada termo de (a + b)² = a² + 2ab + b² surgindo junto da peça. O título entra por linhas
  mascaradas, o lema é "escrito" da esquerda para a direita, botões e sumário sobem em sequência.
- **Leitura da figura:** tocar no quadrado separa as peças e lê a identidade em voz alta, por escrito:
  cada trecho ("a ao quadrado", "dois a b"…) acende a peça e o termo correspondentes.
- Só `transform`, `opacity`, `clip-path` e `stroke-dashoffset` são animados (GPU, sem reflow).
- A entrada espera as fontes (até 0,9 s) para não trocar de fonte no meio da animação.
- **Robustez:** sem GSAP, a página aparece completa e o toque na figura continua funcionando.
  Com "reduzir movimento" ativo no sistema, tudo aparece sem animação.

## Desempenho e acessibilidade

Medido localmente com Lighthouse (mobile, 4G simulado): Performance 98, Acessibilidade 100,
Boas práticas 100, SEO 100, CLS 0, sem violações no axe-core.

- Cerca de 105 KB transferidos (com compressão); fontes e GSAP com cache de 1 ano (`immutable`).
- Fontes auto-hospedadas e pré-carregadas: nenhuma requisição a terceiros.
  Se um dia trocar um arquivo em `assets/fonts` ou `assets/vendor`, **mude o nome do arquivo**
  (o cache longo manteria a versão antiga nos navegadores).
- Contraste AA em todos os textos, foco visível, alvos de toque com 56 px ou mais,
  links externos com `rel="noopener"` e aviso "(abre em nova aba)" para leitores de tela.

## Créditos e licenças

- Latin Modern Roman 2.005, GUST e-foundry, [GUST Font License](assets/fonts/GUST-FONT-LICENSE.txt).
  Os arquivos são subconjuntos sem alteração de desenho (veja `assets/fonts/README.txt`).
- GSAP 3.15.0, GreenSock, [licença padrão sem custo](https://gsap.com/standard-license).
- Conteúdo, textos e identidade visual: João Pedro, jotape.exp.
