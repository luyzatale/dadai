# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## O que é este repositório

Um site educativo em português sobre inteligência artificial, escrito para **uma pessoa
específica**: Julio César Alexandre, servidor público, leitor culto, iniciante absoluto no
assunto. Presente de Dia dos Pais, feito pela filha dele.

Isso não é trivia biográfica — é a restrição de projeto que governa quase toda decisão.
Antes de escrever qualquer conteúdo, leia **[DIRETRIZES-DE-CONTEUDO.md](DIRETRIZES-DE-CONTEUDO.md)**.
Ele é normativo, não sugestivo.

## Não há build, teste nem dependência

`index.html`, na raiz do repositório, é **um único arquivo autocontido** — HTML, CSS e JavaScript no mesmo
documento, sem framework, sem pacote, sem etapa de compilação. Cerca de 2.500 linhas,
das quais ~900 de CSS e ~210 de JS.

```bash
start index.html              # abrir no navegador padrão (Windows)
```

Não crie `package.json`, bundler ou servidor. A ausência deles é decisão de projeto: o
arquivo tem de abrir com duplo clique, offline, na máquina de alguém que não instala nada.

### Verificação após editar

Não há suíte de testes. Rode esta conferência — ela pegou vários defeitos reais neste projeto
(colisão de cascata, CSS órfão, tag desbalanceada):

```bash
python -c "
import io,re,collections,subprocess,tempfile,os
s=io.open('index.html',encoding='utf-8').read()
b=s[s.index('<body'):s.rindex('</body>')]
void={'meta','br','hr','img','input','link','path','circle','rect','line','polygon','polyline','ellipse','use','iframe'}
st=[];er=[]
for m in re.finditer(r'<(/?)([a-zA-Z][\w-]*)([^>]*?)(/?)>',b):
    c,t,_,sf=m.group(1),m.group(2).lower(),m.group(3),m.group(4)
    if t in void or sf=='/': continue
    if not c: st.append(t)
    elif not st or st[-1]!=t: er.append((st[-1] if st else None,t))
    else: st.pop()
print('tags:','ok' if not er and st==['body'] else (st,er))
css=s[s.index('<style>'):s.index('</style>')]
print('CSS :','ok' if css.count('{')==css.count('}') else 'ERRO')
js=s[s.rindex('<script>')+8:s.rindex('</script>')]
f=tempfile.NamedTemporaryFile('w',suffix='.js',delete=False,encoding='utf-8'); f.write(js); f.close()
r=subprocess.run(['node','--check',f.name],capture_output=True,text=True); os.unlink(f.name)
print('JS  :','ok' if r.returncode==0 else r.stderr[:200])
print('ids :','ok' if not [k for k,v in collections.Counter(re.findall(r'\bid=\"([^\"]+)\"',s)).items() if v>1] else 'DUPLICADO')
print('noopener:', s.count('target=\"_blank\"')==s.count('rel=\"noopener noreferrer\"'))
"
```

O console do Windows é cp1252 e **quebra ao imprimir acentos ou caracteres chineses**. Em
scripts de verificação, use `.encode('ascii','replace')` ou imprima só o veredito.

## Arquitetura: o site é um roteador de páginas

Cada `<section id="...">` dentro de `<main>` é **uma página inteira**, não um bloco de
rolagem. O JS esconde todas menos uma, via atributo `hidden`.

Três consequências que precisam ser respeitadas juntas em qualquer mudança estrutural:

1. **A ordem no DOM é a ordem do site.** `paginas = document.querySelectorAll("main section[id]")`
   define a sequência de anterior/próximo. Reordenar seções significa mover os blocos
   `<section>` no arquivo, não só mexer no menu.
2. **Os fólios são numeração posicional.** Cada seção traz `<p class="etiqueta">Fólio NN</p>`,
   e o número tem de bater com a posição no DOM. Reordenou, renumere tudo.
3. **O sumário é escrito à mão**, agrupado em Partes (`<p class="divisao">`). Ele não é
   gerado a partir do DOM — precisa ser reconstruído junto.

Reordenar seção envolve, portanto, três edições coordenadas. Referências cruzadas em prosa
(`"as questões do Fólio 04"`) também precisam ser caçadas — use `grep -n "Fólio 0"`.

A seção `aprovacao` fica fora do sumário de propósito: é a folha de aprovação de design,
alcançável só pelo "próximo" da última seção. Deve sair antes da publicação final.

### O que mais o JS faz

Tudo num único IIFE ao fim do `<body>`, sem dependências: preferências gravadas em
`localStorage` sob o prefixo `iacc.` (tema, escala de fonte, nível de leitura), gaveta do
sumário no celular, balão de glossário, e um injetor de favicon/título que roda no carregamento
e de novo aos 900 ms e 2,5 s — porque quando a página é servida dentro de outro site, o
hospedeiro sobrescreve tanto o `<link rel="icon">` quanto o `document.title`. Por isso
`MARCA` é constante no código, e não lida de `document.title`.

## Restrição que explica muita decisão: sem recurso externo

A pré-visualização publicada roda sob uma CSP que **bloqueia todo host externo** — fonte,
imagem, iframe, script. Não é contornável de dentro da página.

Daí decorre, e deve continuar valendo:

- **Sem webfont.** A tipografia usa pilhas de fontes do sistema: Palatino nos títulos
  (`--display`), sans do sistema no corpo (`--texto`), monoespaçada em fólios e dados
  (`--dado`), e uma pilha CJK com serifa (`--han`) para as marcas gráficas.
- **Favicon e bandeira da China desenhados em SVG embutido**, não referenciados.
- **Vídeo do YouTube não é incorporado** — a capa traz convite, instrução e link para nova aba.
  Já houve fachada com iframe e detecção de bloqueio; foi removida de propósito. Não volte a
  incorporar.
- **Miniaturas do YouTube** (`i.ytimg.com`) são a única exceção: aparecem em produção e
  degradam para um cartão desenhado via handler de `error`.

## Sistema de design "Processo"

Um dossiê: margem de protocolo à esquerda com fólios, coluna única de leitura, cantos retos
(2–4 px), fios de 1 px. Tokens em `:root`, com tema escuro em três estados
(`:root`, `prefers-color-scheme`, `[data-theme]`) — nunca defina cor só dentro de media query.

| Token | Uso — e a disciplina que o acompanha |
|---|---|
| `--carimbo` `#B3372A` | **só onde algo é selado**: fólio ativo, marco, selo de seção. Não é cor de destaque genérica. |
| `--jade` `#1E6153` | fonte verificada, confirmação |
| `--ocre` `#8C6A18` | anotação de margem, recado pessoal |
| `--china-vermelho` `#DE2910` | exclusivo da seção China. Alcança só 4,09:1 sobre o papel — **campo e traço apenas, nunca texto corrido**. |

**Nunca reintroduzir**: creme quente com serifada display e acento terracota, gradiente
roxo-azul, Inter ou Space Grotesk como display, emoji como marcador de seção, cartão
arredondado com barra de acento. A primeira proposta deste site foi descartada por cair nesse
agrupamento. Bandeiras em emoji são conteúdo (identificam país) e continuam permitidas.

### Componentes reutilizáveis

Antes de criar CSS novo, veja se um destes serve — vários já cobrem o caso:
`.def` + `.definicoes` (citação institucional com "o que essa definição decide"),
`.esqueleto-comum` (lista numerada de síntese), `.verbete` (tema de ética expandido),
`.fontes` (bloco de referências), `.escopo` (nota do que ainda falta), `.margem-nota`
(observação em ocre), `.recado` (voz da filha), `.leitura` (fonte primária com link),
`.criterio` (ressalva metodológica), `.org` + `.logo-org` (organização), `.livro`,
`.aula`, `.degrau`, `.card-d`, `.quadro` (tabela comparativa em `.rolagem-tabela`).

## Regras de conteúdo que mais pegam

Detalhe e razão em [DIRETRIZES-DE-CONTEUDO.md](DIRETRIZES-DE-CONTEUDO.md). O resumo operacional:

- **Não técnico, porém não simplista.** Remover jargão, preservar profundidade. "Iniciante em
  IA" descreve o vocabulário, não o repertório. Nunca escrever "é simples", "linguagem simples",
  "não se preocupe".
- **Tratamento: o senhor.** Rótulos de nível são "Essencial" e "Aprofundar", jamais
  "fácil"/"difícil".
- **Toda afirmação normativa ou factual leva fonte.** Definições legais e datas precisam ser
  **verificadas na web antes de escrever** — não de memória. Já foram conferidas assim as
  definições de IA da OCDE, UE, PL 2.338/2023 e UNESCO, e o Constitutional AI da Anthropic.
- **Nada em chinês no conteúdo.** Exceção declarada: as três marcas gráficas (人 no logotipo e
  nos títulos, 父亲节 no selo da dedicatória, 中 na marca-d'água da China).
- **Livros só com edição em português confirmada** (editora e tradutor). Quando a regra derrubar
  um título importante, dizer no texto o que se perdeu.
- **Logotipos só a partir de arquivo oficial** em `logos/`. Enquanto não existirem, o
  ladrilho `.logo-org` mostra monograma neutro com ponto ocre de pendência. **Não desenhar marca
  registrada de memória.**
- Quando faltar informação verificável, **deixar lacuna explícita** numa `.escopo` em vez de
  preencher com plausível.

## Publicar como Artifact

O arquivo local é um documento completo; o Artifact recebe conteúdo sem `<html>`/`<head>`/`<body>`.
Extraia `<title>` + `<style>` + interior do `<body>` para um arquivo no scratchpad e publique
esse. O `<link rel="icon">` do `<head>` fica de fora — por isso o injetor de favicon existe no JS.

```python
t=re.search(r'<title>.*?</title>',s,re.S).group(0); cs=re.search(r'<style>.*?</style>',s,re.S).group(0)
bd=s[s.index('>',s.index('<body'))+1:s.rindex('</body>')]
```

Republique sempre o **mesmo caminho de arquivo** para manter a URL do Artifact.

## Git

Remoto: `https://github.com/luyzatale/dadai`. O `gh` CLI não está instalado.

O Gerenciador de Credenciais do Windows devolve 403 neste repositório. Peça um token à usuária
e use-o de forma transitória — **nunca embutido no URL do remoto**, que o gravaria em texto puro
em `.git/config`:

```bash
AUTH=$(printf 'x-access-token:%s' "$TOKEN" | base64 | tr -d '\n')
git -c credential.helper= -c http.https://github.com/.extraheader="AUTHORIZATION: basic $AUTH" push
```

Identidade dos commits: `Luyza Alexandre <alexandre.t.luyza@gmail.com>`.

Ao escrever mensagem de commit no bash, cuidado com **crases** dentro de aspas duplas — o
markdown de `README.md` já foi corrompido por substituição de comando. Use aspas simples ou
heredoc com delimitador citado.
