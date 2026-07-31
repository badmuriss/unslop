# eval: 20 checagens binárias sobre o próprio output

Rode este arquivo **depois** de escrever ou editar, **antes** de entregar,
sempre sobre o texto que você acabou de produzir. Não é revisão subjetiva. Cada
linha passa ou falha, e a evidência é um trecho citado ou uma contagem.

## Protocolo

1. Rode as **universais** (U1 a U8) em todo texto.
2. Rode as **pt-br** (P1 a P8) se o texto for português brasileiro. P6, P7 e P8
   só valem no contexto Outis, marque `n/a` fora dele.
3. Rode as de **modo escrever** (E1 a E4) só no modo ESCREVER.
4. Alguma falhou? Revise **uma vez**, mirando só o que falhou. Rode de novo
   apenas as checagens que falharam.
5. Se ainda falhar depois dessa revisão, entregue assim mesmo e diga qual
   checagem falhou e por que você deixou. Uma rodada de revisão, nunca duas.
6. Nunca marque passa sem olhar. Checagem sem evidência conta como falha.

---

## Universais

**U1. Zero artefato de conversa de chat.**
Procure: "Claro!", "Com certeza!", "Ótima pergunta", "Espero que ajude", "Aqui
está", "Posso ajudar com mais alguma coisa", "Of course", "Would you like me
to", "As of my last update".
Passa se: zero ocorrências.

**U2. Nenhum fato novo em relação à fonte.**
Liste todo nome próprio, número, data, valor e citação do seu output. Para cada
item, aponte onde ele aparece no texto original (modo EDITAR) ou no brief (modo
ESCREVER).
Passa se: todo item tem origem apontada, ou está marcado `[VERIFICAR: ...]`.
Falha se: sobrou um item sem origem, mesmo que seja verdade.

**U3. Toda afirmação de terceiro e todo número têm fonte.**
Liste as frases que atribuem informação a alguém ("especialistas", "estudos",
"pesquisa", "segundo") e todos os números do texto.
Passa se: cada uma nomeia a fonte no próprio texto ou carrega `[VERIFICAR]`.

**U4. Nenhuma tríade obrigatória.**
Conte os itens de cada lista e procure séries de três adjetivos ou três
substantivos coordenados.
Falha se: o texto tem duas ou mais listas e **todas** têm exatamente 3 itens, ou
se existe qualquer série de três adjetivos coordenados ("rápida, segura e
escalável").

**U5. Formatação limpa.**
Verifique os headings e os marcadores de lista.
Passa se: nenhum heading em Title Case, nenhum emoji em heading ou em marcador,
e no máximo 2 itens no padrão `- **Coisa:** frase` no documento inteiro.

**U6. Ritmo variado.**
Conte as palavras de cada frase, parágrafo a parágrafo.
Falha se: existem 3 frases seguidas com menos de 9 palavras cada, ou 4 frases
seguidas cujo comprimento cabe numa faixa de 3 palavras.

**U7. Zero paralelismo negativo.**
Procure: "não é só", "não é apenas", "não se trata de", "mais do que X, é Y",
"não apenas ... mas também", "not only ... but also", "it's not just".
Passa se: zero ocorrências.

**U8. Uma entidade, um nome.**
Escolha a entidade principal do texto. Liste todos os termos usados para
apontar para ela.
Passa se: um único termo, salvo a primeira menção com nome completo e as
seguintes com nome curto.
Falha se: o mesmo referente vira agente, assistente, ferramenta e solução ao
longo do texto.

---

## pt-br

**P1. Zero travessão.**
Procure os caracteres `—` e `–` no corpo.
Passa se: zero ocorrências, ou as únicas ocorrências são fala de ficção
(travessão no início da linha) ou intervalo numérico ("2024–2026").

**P2. Zero gerúndio de call center.**
Procure: `estarei`, `estaremos`, `estará`, `vou estar`, `vamos estar`, `vai
estar`, cada um seguido de verbo em gerúndio.
Passa se: zero ocorrências fora de citação literal.

**P3. Abertura sem cerimônia.**
Leia as duas primeiras frases.
Falha se: contêm "no cenário atual", "nos dias de hoje", "no mundo de hoje",
"em um mundo cada vez mais", "vale destacar", "é importante ressaltar", "cabe
salientar", "não é novidade que", "com o avanço da tecnologia", ou se a primeira
frase é a definição de dicionário do assunto.

**P4. Fecho concreto.**
Leia a última frase.
Passa se: ela contém um fato, um número, um nome próprio ou uma decisão.
Falha se: é "e assim, vemos que", "em suma", "fica claro que", "o futuro é
promissor", "agora é com você", pergunta retórica, ou resumo do que o texto já
disse.

**P5. Vocabulário-muleta dentro do limite.**
Conte as ocorrências da tabela da seção 4 de `references/ptbr.md` (robusto,
panorama, crucial, pivotal, impulsionar, alavancar, potencializar, mergulhar,
tapeçaria, cenário abstrato, desvendar, explorar, abordar, ecossistema,
sinergia, holístico, empoderar, transformador, otimizar).
Passa se: no máximo 1 ocorrência a cada 300 palavras.

**P6. Regras da casa: zero "pra", "pro", "pros".** *(só contexto Outis)*
Procure com fronteira de palavra: `\bpra\b`, `\bpro\b`, `\bpros\b`, sem
diferenciar maiúscula.
Passa se: zero ocorrências fora de citação literal de terceiro.
Verifique também que a correção não quebrou nenhuma palavra: procure "parato",
"parazo", "parática", "paraduto", "paraspecta" e qualquer outra deformação.

**P7. Regras da casa: zero hashtag e zero preço em criativo.** *(só contexto Outis)*
Procure `#` em caption e `R$`, "a partir de", "por apenas" em peça de criativo.
Passa se: nenhuma hashtag em nenhum texto de rede social, e nenhum valor em
peça de criativo. Preço em proposta e em página de vendas continua permitido.

**P8. Regras da casa: sem frase-efeito vazia e sem voz self-serve.** *(só contexto Outis)*
Procure: "quem não integra, perde", "o futuro é agora", "saia na frente", "não
fique para trás", "o mercado não espera", "quem não se adapta", "seus
concorrentes já estão", "basta", "é só", "em poucos cliques", "sem código",
"comece grátis", "teste gratuito".
Passa se: zero ocorrências, e o texto descreve a Outis fazendo o trabalho, não o
cliente configurando a ferramenta.

---

## Modo escrever

**E1. Rubrica acima do corte.**
Passa se: total 35 ou mais em `references/rubrica.md` e nenhuma dimensão em 3 ou
menos.

**E2. Abertura com peso.**
Leia a primeira e a segunda frase.
Passa se: pelo menos uma delas traz um fato, um número, uma cena concreta ou uma
afirmação com a qual dá para discordar.
Falha se: as duas são contexto, definição ou promessa do que vem depois.

**E3. Brief cumprido.**
Compare com o brief: formato pedido, tamanho, público, canal, chamada para ação.
Passa se: o formato bate, o tamanho está dentro de 15% do pedido e a chamada
para ação pedida está lá.

**E4. Amostra de voz respeitada.**
Só quando o usuário forneceu amostra ou arquivo de voz. Caso contrário, `n/a`.
Compare com a amostra: pessoa gramatical, faixa de comprimento de frase, nível
de gíria e formalidade, hábito de pontuação.
Passa se: os quatro batem. Falha se: o texto está visivelmente mais formal ou
mais coloquial que a amostra.

---

## Formato de saída do eval

```
U1 passa   U2 passa   U3 FALHA   U4 passa   U5 passa   U6 FALHA   U7 passa   U8 passa
P1 passa   P2 passa   P3 passa   P4 passa   P5 passa   P6 n/a     P7 n/a     P8 n/a
E1 passa   E2 passa   E3 passa   E4 n/a

U3 falhou: "70% dos consumidores" sem fonte no parágrafo 2.
U6 falhou: 3 frases seguidas de 6, 7 e 5 palavras no fecho.
Revisão 1 aplicada. U3 passa (número trocado pelo dado da Trigale), U6 passa.
```

Entregue o texto com essa linha de resultado. Se você não rodou o eval, você não
terminou.
