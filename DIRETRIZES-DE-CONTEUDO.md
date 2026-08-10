# Diretrizes de conteúdo — Dad AI

Regra geral que vale para **todas as seções**, sem exceção.

---

## A regra

> **Os tópicos devem ser não técnicos, porém não simplistas.**
> O leitor é uma pessoa culta e existencial.

Julio César Alexandre é iniciante absoluto em inteligência artificial. Isso descreve o
vocabulário dele sobre um assunto novo — **não** o repertório intelectual dele.

O que se remove é o jargão. O que se preserva é a profundidade.

---

## O que isso significa na prática

| Remover | Preservar |
|---|---|
| Sigla sem tradução, nome de arquitetura, número de parâmetro | A tensão moral do tema |
| Analogia infantilizante ("é como uma receita de bolo") | A ambiguidade real, quando ela existe |
| Tom de folheto de repartição | A consequência prática para quem decide |
| "Não se preocupe, é simples" | A pergunta que o tema não resolve |

**Frase de teste.** Se o parágrafo soar como cartilha explicativa de órgão público, está
errado. Se soar como um bom ensaio de jornal sério — sem uma única palavra técnica não
explicada —, está certo.

---

## Como cada tópico deve abrir

Ancorar em uma **pergunta humana**, não no funcionamento interno da tecnologia.

- ❌ "Redes neurais são compostas por camadas de nós interconectados que…"
- ✅ "Uma decisão que ninguém consegue explicar ainda é uma decisão legítima?"

Perguntas que servem de eixo recorrente ao longo do site: o que isso faz com o **trabalho**,
com o **julgamento**, com a **autoridade**, com o **tempo**, com a **memória**, com a **morte**.

---

## Registro de linguagem

- Tratamento: **o senhor**. Formal, nunca solene.
- Citar **pensadores e fontes reais** — epígrafes, autores, legislação — em vez de metáforas
  fáceis. Uma epígrafe bem escolhida educa mais que três parágrafos de simplificação.
- Palavra técnica inevitável: usar, e explicar no mesmo instante pelo balão de glossário.
  Ele não precisa ser poupado da palavra — precisa recebê-la com a definição junto.
- Frases curtas por clareza, nunca por desconfiança da capacidade do leitor.
- Onde há divergência genuína entre especialistas, dizer que há. Não fechar artificialmente.

---

## Rótulos de interface

Os controles do site obedecem à mesma regra.

- Níveis de leitura: **"Essencial" / "Aprofundar"** — nunca "Bem simples" / "Difícil".
- Nada no site deve sugerir que existe uma versão para quem não entende.

---

## Ética e sociedade (Fólio 04) — nota específica

É a seção onde a regra mais importa. Os 16 temas são filosóficos por natureza: colonialismo
de dados, identidade digital, a morte na era digital, economia cognitiva.

Tratá-los como "curiosidades sobre tecnologia" seria a pior traição possível ao leitor.
Cada verbete termina com suas **referências completas e verificáveis** — porque ele vai
querer conferir, e talvez citar.

---

## Logotipos de empresas

> **Sempre que uma empresa for referenciada, exibir o logotipo dela.**

Vale para as fichas de organizações, as pastilhas de ferramentas e qualquer menção nominal
a uma companhia ao longo do site.

### Regras de uso

1. **Somente arquivo oficial.** O logotipo vem da página de marca da própria empresa (ou do
   repositório oficial dela). Nunca desenhado de memória, nunca redesenhado "parecido".
   Marca aproximada é marca errada.
2. **Sem recolorir, sem distorcer.** Proporção original preservada; nada de forçar a marca
   na paleta do site.
3. **Fundo neutro.** Cada logotipo assenta sobre um ladrilho claro próprio, para não brigar
   com o papel ofício nem com o modo escuro.
4. **SVG embutido no arquivo**, não referência a CDN — o site precisa funcionar offline e
   sem depender de servidor de terceiros.
5. **Texto alternativo** com o nome da empresa, sempre.
6. **Enquanto o arquivo oficial não existir**, exibir o monograma neutro. É uma ausência
   honesta; um logotipo inventado não é.

### Onde colocar os arquivos

`logos/<empresa>.svg` — o nome do arquivo em minúsculas, sem acento
(`deepseek.svg`, `alibaba.svg`, `baidu.svg`, `openai.svg`, `anthropic.svg`).

---

## Nada em chinês no conteúdo

> **Não usar palavras em chinês no texto.**

O leitor não lê chinês. Caractere sem tradução no meio da frase é ruído, não erudição —
e contraria a regra maior deste site, que é remover barreira sem remover profundidade.

**Vale para:** nomes de empresa (`DeepSeek`, não `DeepSeek · 深度求索`), títulos de livro,
legendas, glossários e qualquer prosa. Se um termo chinês for indispensável ao argumento,
escrevê-lo em português, ou transliterado e explicado na mesma frase.

**Não vale para as três marcas gráficas do projeto**, que são identidade visual e não texto:

| Marca | Onde | Por quê |
|---|---|---|
| 人 | logotipo, favicon, selo antes de cada título | encomendado como símbolo do site; explicado no atributo `title` |
| 父亲节 | selo da dedicatória | é o presente; descrito para leitor de tela |
| 中 | marca-d'água da seção China | textura a 9% de opacidade, `aria-hidden` |

Se essas três também tiverem de sair, é decisão consciente a tomar — não descuido.

---

## Livros: só com edição em português

> **Recomendar apenas títulos com edição brasileira ou portuguesa confirmada.**

Indicar livro que o leitor não consegue ler é recomendação vazia. Antes de entrar na estante,
confirmar **editora e tradutor** — não basta o título existir.

Quando a regra derrubar um livro importante, **dizer o que se perdeu**. A estante da seção
China declara, no próprio texto, que o principal contraponto crítico sobre vigilância ficou
de fora por falta de tradução. Uma estante honesta recomenda o que se pode ler e admite o
que não se pode.
