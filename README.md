# Dad AI · O Homem que Revisa a IA

Um guia de inteligência artificial em português, escrito para **Julio César Alexandre** —
servidor público, leitor culto, iniciante absoluto no assunto. Presente de Dia dos Pais, 2026.

O site não ensina a operar ferramentas. Ele acompanha o leitor enquanto ele forma a própria
opinião: de onde essa técnica veio, por quais mãos passa, o que já vem decidindo em nome do
Estado e em que ponto a decisão precisa voltar a ser de alguém que responde por ela.

---

## Estado atual

**MVP de design aprovado em revisão.** A estrutura, o sistema visual e a experiência estão
definidos; o conteúdo integral de cada seção ainda será escrito.

| | |
|---|---|
| Protótipo navegável | [`mvp/index.html`](mvp/index.html) — arquivo único, sem dependências |
| Regra de conteúdo | [`DIRETRIZES-DE-CONTEUDO.md`](DIRETRIZES-DE-CONTEUDO.md) |

Para ver: abra `mvp/index.html` em qualquer navegador. Não requer servidor nem build.

---

## Estrutura

Doze seções em quatro partes, ordenadas por importância para o leitor. Cada uma é uma
**página independente** — não há rolagem contínua entre seções.

**Parte I · A questão**
`01` Início · `02` Conceitos e Cronologia · `03` Quem constrói a IA · `04` Ética e sociedade · `05` Regulamentação da IA · `06` IA no serviço público

**Parte II · A prática**
`07` O método 4D · `08` Ferramentas do dia a dia · `09` Engenharia de prompt · `10` SocialTech

**Parte III · Um país à parte**
`11` China em foco

**Parte IV · Aulas**
`12` Recomendação de trilha

---

## A regra de conteúdo

> **Os tópicos devem ser não técnicos, porém não simplistas.**
> O leitor é uma pessoa culta e existencial.

"Iniciante em IA" descreve o vocabulário sobre um assunto novo, não o repertório intelectual.
Remove-se o jargão; preserva-se a profundidade. Detalhes em
[`DIRETRIZES-DE-CONTEUDO.md`](DIRETRIZES-DE-CONTEUDO.md).

Todo tema de ética e toda afirmação normativa carregam **referências explícitas e
verificáveis** — o leitor vai querer conferir e, eventualmente, citar.

---

## Direção visual — "Processo"

O site se apresenta como um dossiê: margem de protocolo à esquerda com fólios, coluna única
de leitura, cantos retos, fios de 1px.

| Token | Valor | Uso |
|---|---|---|
| Papel ofício | `#EDEFE9` | fundo, cinza-celadon frio |
| Tinta | `#131E19` | texto, verde-preto de caneta |
| Carimbo | `#B3372A` | apenas onde algo é selado |
| Jade | `#1E6153` | fontes verificadas, confirmações |
| Ocre | `#8C6A18` | anotação de margem, recados pessoais |
| Vermelho oficial | `#DE2910` | exclusivo da seção China: campo e bandeira, nunca texto |

**Tipografia** — Palatino nos títulos (registro de certidão, não de revista); sans do sistema
no corpo; monoespaçada com `tabular-nums` em fólios, datas e quadros.

**Logo** — 人 (*rén*), "humano", em selo 白文: caractere reservado em branco sobre campo
vermelho. Em chinês, inteligência artificial escreve-se 人工智能 — e o primeiro caractere da
palavra é *humano*.

### O que foi deliberadamente evitado

Creme quente com serifada display e acento terracota; gradiente roxo-azul; Inter ou Space
Grotesk como face de display; emoji como marcador de seção; cartão arredondado com barra de
acento. É o agrupamento visual que denuncia página gerada automaticamente, e a primeira
proposta foi descartada por cair nele.

---

## Acessibilidade

O leitor tem mais de 60 anos. Isso é premissa de projeto, não um extra.

- Controle **A A A** de tamanho de texto, aplicado ao site inteiro e memorizado entre visitas
- Piso de 16px no celular em qualquer escala
- Modo claro e escuro, respeitando também a preferência do sistema
- Dois níveis no mesmo texto — **Essencial** e **Aprofundar**, nunca "fácil" e "difícil"
- Termos difíceis abrem explicação em um toque
- Navegação por teclado (setas ← → percorrem as seções), foco visível, `prefers-reduced-motion`
- Contraste conferido: nenhum par de cor abaixo de 4,5:1 em texto corrido

---

## Próximos passos

1. Escrever o conteúdo integral das dez seções sob a regra acima
2. Datar e reconferir todo o quadro de regulamentação — legislação de IA muda de mês para mês
3. Confirmar quais títulos da estante têm edição brasileira
4. Reconferir a nomenclatura do método 4D contra o material original da Anthropic
5. Separar o protótipo em arquivos por seção e publicar
