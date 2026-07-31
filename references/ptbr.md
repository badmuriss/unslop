# Camada pt-br: slop de IA em português brasileiro

Carregue este arquivo sempre que o texto estiver em português brasileiro, em
qualquer modo (escrever, editar, detectar, avaliar). A lista em inglês do
SKILL.md não cobre o que denuncia um texto de IA em pt-br. Metade dos padrões
daqui não tem equivalente em inglês, e o número 1 da lista (travessão) é
exatamente o oposto do que a norma culta brasileira faz na prática.

## Escala de severidade

| Nível | Significado | O que fazer |
|-------|-------------|-------------|
| **crítica** | sozinho já entrega o texto como IA | corrigir sempre, sem exceção; falha no `eval.md` |
| **alta** | denuncia em conjunto com qualquer outro | corrigir sempre, salvo citação literal |
| **média** | passa em um texto, vira padrão em três | corrigir salvo justificativa explícita |
| **baixa** | questão de gosto e consistência | julgar pelo contexto |

Citação literal de outra pessoa é intocável em qualquer nível. Se a fonte
escreveu "estarei enviando", a citação mantém "estarei enviando".

---

## 1. Pontuação e formatação

### 1.1 Travessão (—, –) usado como pausa retórica
**Severidade: crítica.** É o tell número 1 em pt-br. Brasileiro escrevendo no
teclado quase nunca produz um travessão: dá trabalho, não está no teclado ABNT2
e o costume é usar vírgula, ponto, dois-pontos ou parênteses. Quando aparece uma
oração intercalada entre travessões, ou pior, no formato inglês colado
(`palavra—palavra`), a origem é um modelo de linguagem.

> Ruim: A entrega — que já estava atrasada — chegou sem a nota fiscal.
> Bom: A entrega, que já estava atrasada, chegou sem a nota fiscal.

> Ruim: O plano custa 697 — sem mensalidade.
> Bom: O plano custa 697, sem mensalidade.

> Ruim: Ele tinha uma única saída—e não usou.
> Bom: Ele tinha uma única saída. Não usou.

Substituições, em ordem de preferência: vírgula (aposto curto), ponto (duas
ideias que aguentam ficar sozinhas), dois-pontos (a segunda parte explica a
primeira), parênteses (informação lateral de verdade).

Exceções legítimas, não corrija:
- diálogo em ficção e roteiro, onde o travessão marca a fala ("— Vem cá.");
- meia-risca em intervalos numéricos ("páginas 10–15", "2024–2026");
- citação literal de um texto que já usava travessão.

### 1.2 Title Case Em Título
**Severidade: alta.** Não existe em português. Só a primeira palavra e os nomes
próprios levam maiúscula. Title case em heading é tradução mecânica de padrão
editorial em inglês.

> Ruim: Como Aumentar Suas Vendas No Instagram
> Bom: Como aumentar suas vendas no Instagram

### 1.3 Emoji decorando heading ou bullet
**Severidade: alta.** 🚀 no título, ✅ em todo item de lista, 💡 antes da dica.
Em caption de Instagram um emoji dentro da frase pode ser natural. Emoji como
marcador de lista é layout de IA.

> Ruim: ## 🚀 Resultados
> Bom: ## Resultados

### 1.4 Bullet com cabeçalho em negrito
**Severidade: média.** O padrão `- **Coisa:** frase explicativa` repetido em
todo item transforma texto em ficha técnica. Vira prosa, ou vira tabela de
verdade, ou fica só o bullet sem o negrito.

> Ruim:
> - **Velocidade:** entrega em 7 dias.
> - **Preço:** valor fechado.
> Bom: Entrega em 7 dias, com valor fechado antes de começar.

### 1.5 Negrito mecânico no meio do parágrafo
**Severidade: média.** Negrito em três expressões por parágrafo não destaca
nada, só sinaliza que o modelo achou tudo importante. Um destaque por seção, ou
nenhum.

### 1.6 Aspas curvas misturadas com retas
**Severidade: baixa.** Escolha um padrão e mantenha no documento inteiro. Aspas
curvas coladas de outro lugar dentro de um texto com aspas retas denunciam
copiar e colar de saída de chat.

---

## 2. Aberturas cerimoniais

**Severidade: alta** para todas. O modelo aquece antes de dizer qualquer coisa.
Corte a primeira frase inteira e comece no fato. Quase sempre o texto melhora e
não perde nada.

Lista de banidas: "no cenário atual", "nos dias de hoje", "no mundo de hoje",
"em um mundo cada vez mais [conectado/digital/competitivo]", "vale destacar
que", "é importante ressaltar que", "cabe salientar que", "não é novidade que",
"com o avanço da tecnologia", "você já parou para pensar", "em um mercado cada
vez mais competitivo", "atualmente, muitas empresas".

> Ruim: No cenário atual, é importante ressaltar que a automação de atendimento se tornou fundamental para empresas de todos os portes.
> Bom: Um restaurante que responde em 4 horas perde a reserva para quem responde em 4 minutos.

> Ruim: Você já parou para pensar em quanto tempo sua equipe gasta com tarefas repetitivas?
> Bom: A equipe do Trigale gastava 6 horas por semana copiando pedido de WhatsApp para planilha.

### 2.1 Definição de dicionário como primeira frase
**Severidade: alta.** "Marketing digital é o conjunto de estratégias..." O
leitor que chegou no texto já sabe o que é. Comece pelo caso, pelo número ou
pela afirmação contestável.

---

## 3. Fechamentos

### 3.1 Fecho genérico positivo
**Severidade: alta.** "E assim, vemos que", "Em suma", "Portanto, fica claro
que", "O futuro é promissor", "As possibilidades são infinitas", "Agora é com
você". Termine na informação mais concreta que você tem e pare.

> Ruim: E assim, vemos que investir em automação é fundamental para quem quer crescer. O futuro pertence a quem se adapta.
> Bom: O tempo de resposta caiu de 4 horas para 3 minutos. O custo mensal ficou em 100 reais.

### 3.2 Recapitulação do que o texto acabou de dizer
**Severidade: média.** Parágrafo final que resume os tópicos anteriores em
ordem. O leitor leu. Corte.

### 3.3 Pergunta retórica que o próprio texto responde
**Severidade: alta.** "Então vale a pena? Sim, vale." A pergunta não é pergunta,
é enfeite. Afirme direto.

> Ruim: Isso significa que toda empresa precisa de IA? Não necessariamente.
> Bom: Empresa com menos de 50 conversas por dia não precisa disso.

---

## 4. Vocabulário-muleta

**Severidade: média** por ocorrência isolada, **alta** quando aparecem duas ou
mais na mesma seção. Estas palavras coocorrem: onde tem "robusto" costuma ter
"panorama" e "impulsionar" a três linhas de distância.

| Palavra | Troca |
|---------|-------|
| robusto | específico ("aguenta 300 pedidos por hora"), ou corte |
| panorama | o assunto em si ("o mercado de X", "os três concorrentes") |
| fundamental, crucial, essencial, imprescindível | corte, ou diga a consequência de não ter |
| pivotal | não existe em pt-br fora de tradução ruim; corte |
| impulsionar, alavancar, potencializar, turbinar | aumentar, dobrar, acelerar, ou o número real |
| mergulhar, mergulho profundo (delve) | ver, analisar, ou o verbo específico |
| tapeçaria, mosaico, teia | corte a metáfora |
| cenário (abstrato) | situação concreta, ou corte |
| desvendar, desmistificar, revelar os segredos | explicar, mostrar, ou o fato direto |
| explorar (como verbo de artigo) | o verbo real: comparar, testar, medir |
| abordar, endereçar (address) | tratar, resolver, responder |
| jornada (do cliente, de transformação) | as etapas com nome |
| ecossistema, sinergia, holístico | corte |
| solução completa, solução ideal | o que a coisa faz |
| empoderar, revolucionar, transformador, inovador | corte, ou mostre o antes e o depois |
| otimizar, maximizar, elevar a outro patamar | o ganho medido |
| significativo, considerável, expressivo | o número |
| dinâmico, versátil, poderoso, incrível | corte |
| aprofundar-se em | o verbo específico |

Regra prática: no máximo uma palavra desta tabela a cada 300 palavras.

### 4.1 Tradução literal do inglês corporativo
**Severidade: média.** "entregar valor", "no final do dia", "mover a agulha",
"dobrar a aposta", "dar um passo atrás", "estamos falando de", "isso é um
divisor de águas", "seja você um X ou um Y". Soam a texto passado no tradutor.

> Ruim: Seja você um pequeno empreendedor ou um gestor de uma grande empresa, essa ferramenta entrega valor.
> Bom: Funciona igual para quem tem 1 loja e para quem tem 40.

---

## 5. Construções

### 5.1 Gerúndio de call center
**Severidade: crítica.** "Estarei enviando", "vamos estar acompanhando", "vou
estar verificando", "estaremos entrando em contato". Futuro perifrástico com
gerúndio, marca registrada de script de telemarketing e de LLM treinado em
texto corporativo brasileiro.

> Ruim: Estarei enviando a proposta ainda hoje e vamos estar acompanhando o retorno.
> Bom: Envio a proposta hoje e acompanho o retorno.

Busca mecânica: `estarei|estaremos|vou estar|vamos estar|vai estar|estará` seguido de gerúndio.

### 5.2 "Não é só X, é Y" e "não apenas... mas também"
**Severidade: alta.** Paralelismo negativo. Diz a coisa uma vez.

> Ruim: Não é só um site, é uma máquina de vendas.
> Bom: O site fecha orçamento sozinho, sem você responder nada.

> Ruim: A ferramenta não apenas organiza os pedidos, mas também gera o relatório.
> Bom: A ferramenta organiza os pedidos e gera o relatório.

Variantes da mesma família: "mais do que X, é Y", "isso não é sobre X, é sobre
Y", "não se trata de X, e sim de Y".

### 5.3 Regra de três e tríades rítmicas
**Severidade: média.** Três adjetivos, três benefícios, três itens em toda
lista, três frases curtas em sequência. O modelo fecha tudo em três porque soa
completo. Use dois, ou quatro, ou um.

> Ruim: Uma solução rápida, segura e escalável.
> Bom: Roda em 7 dias e aguenta pico de Black Friday.

Cuidado especial com a cadeia de frases curtas: "Simples. Direto. Funciona."
Isso é slogan, não texto.

### 5.4 Rotação de sinônimos
**Severidade: alta.** O mesmo referente vira agente, depois assistente, depois
ferramenta, depois solução, depois plataforma, tudo no mesmo parágrafo. Humano
repete o substantivo. A rotação confunde o leitor, que fica procurando a
diferença entre as quatro coisas.

> Ruim: O agente responde no WhatsApp. O assistente identifica a intenção e a ferramenta registra no CRM.
> Bom: O agente responde no WhatsApp, identifica a intenção e registra no CRM.

Escolha um nome por entidade e mantenha do começo ao fim do documento.

### 5.5 Dois-pontos de revelação em excesso
**Severidade: média.** "A melhor parte: ...", "O resultado? ...", "E tem mais:
...", "O detalhe: ...". Uma vez por texto é ritmo. Três vezes é tique.

> Ruim: O resultado? 40% mais conversas. E o melhor: sem contratar ninguém.
> Bom: Deu 40% mais conversas sem contratar ninguém.

### 5.6 Atribuição vaga
**Severidade: alta.** "Especialistas apontam", "estudos mostram", "pesquisas
indicam", "dados do mercado revelam", "segundo especialistas", "é sabido que".
Ou nomeia a fonte, ou corta a frase. Nunca invente a fonte para preencher.

> Ruim: Estudos mostram que 70% dos consumidores preferem atendimento por WhatsApp.
> Bom: Na Trigale, 8 de cada 10 pedidos do mês passado entraram por WhatsApp.
> Alternativa: [VERIFICAR: origem do dado de 70%] e, se não achar, corte.

### 5.7 Hedging empilhado
**Severidade: média.** "Pode-se dizer que talvez seja possível que em alguns
casos". Uma ressalva por afirmação, no máximo. Se você não tem certeza, diga o
que sabe e o que não sabe, com essas palavras.

> Ruim: Pode-se dizer que, de certa forma, essa abordagem talvez traga resultados.
> Bom: Funcionou nos dois clientes onde testamos. Não sei se escala para 50.

### 5.8 Voz passiva burocrática e sujeito indeterminado
**Severidade: média.** "Foi identificado que", "acredita-se que", "é possível
afirmar que", "faz-se necessário". Diga quem fez.

> Ruim: Foi identificado um gargalo no processo de aprovação.
> Bom: O gargalo está na aprovação: cada orçamento espera 2 dias pela assinatura.

### 5.9 Explicação redundante do óbvio
**Severidade: média.** "Ou seja", "isso significa que", "em outras palavras",
usados logo depois de uma frase que já estava clara. Equivalente pt-br do sinal
N1 do SKILL.md (over-explaining). Se precisou explicar, a frase anterior estava
ruim: conserte ela e apague a explicação.

### 5.10 Paralelismo perfeito demais
**Severidade: baixa.** Todos os bullets com o mesmo comprimento, todos
começando com verbo no infinitivo, todos os parágrafos com quatro linhas. Texto
humano é irregular. Deixe um item curto e um longo.

---

## 6. Calibração de registro em pt-br

"Mais humano" não quer dizer mais gíria. O erro de correção excessiva em
português é jogar um texto institucional para o registro de conversa de
WhatsApp.

Não faça em texto institucional, proposta, landing page ou documentação:
- gíria e enchimento oral: "tipo assim", "meio que", "sei lá", "né", "mano", "bagulho", "papo reto";
- diminutivo afetivo: "uma ajudinha", "rapidinho", "projetinho";
- interjeição de rede social: "gente", "olha só", "spoiler";
- perda de precisão técnica em nome do tom: "número oficial da Meta" não é a mesma coisa que "número Twilio na WhatsApp Business API da Meta";
- inversão do nome do produto ou do fornecedor, que precisa ficar exato.

Pode fazer, em qualquer registro:
- frase curta;
- primeira pessoa quando o autor de fato assina;
- contração natural da fala escrita ("tá" só em fala citada, "está" no corpo);
- opinião assumida, inclusive negativa.

Teste: essa frase caberia numa proposta comercial assinada? Se só cabe num
story, você passou do ponto.

---

## 7. Regras da casa (contexto Outis / Murilo)

Aplique esta seção quando o texto for da Outis, de qualquer marca da casa
(Outis, Ecos, Entrelinhas, Redatio) ou quando o usuário for o Murilo. Fora
desse contexto, é preferência de outro autor, não regra.

### 7.1 Nunca "pra", "pro", "pros"
**Severidade: crítica.** Sempre "para", "para o", "para os", "para a", "para
as". Vale inclusive em caption e story.

> Ruim: Feito pra quem não tem tempo pro operacional.
> Bom: Feito para quem não tem tempo para o operacional.

Cuidado na busca e substituição: use fronteira de palavra (`\bpra\b`,
`\bpro\b`, `\bpros\b`, sem diferenciar maiúscula). Não corrompa **produto,
prazo, prática, praticamente, prata, praia, aprovar, próximo, propósito,
prospect, Prospecta**, nem o nome de plano **Pro** (Starter, Pro, Business), nem
**pró-labore**. Citação literal de cliente que falou "pra" fica como está.

### 7.2 Zero hashtag em caption
**Severidade: crítica.** Nenhuma hashtag, em nenhuma rede, em nenhum formato.
Se o texto termina com um bloco de #, apague o bloco inteiro.

### 7.3 Frase-efeito vazia banida
**Severidade: crítica.** Lista: "quem não integra, perde", "o futuro é agora",
"saia na frente", "não fique para trás", "o mercado não espera", "a revolução já
começou", "quem não se adapta, morre", "seus concorrentes já estão fazendo".

Substitua por substância concreta, uma destas quatro: um dado com origem, um
exemplo nomeado, um antes e depois, ou o mecanismo (como a coisa funciona por
dentro).

> Ruim: Quem não integra IA no atendimento, perde. O futuro é agora.
> Bom: A pizzaria respondia em 40 minutos no pico de sexta. Com o agente, responde em 30 segundos e o pedido não vaza para o concorrente.

### 7.4 Zero preço em criativo
**Severidade: crítica.** Nenhum valor, nenhum "a partir de", nenhum "R$" em
peça de criativo. Preço vive na conversa e na proposta.

### 7.5 Voz Outis: agência que faz pelo cliente
**Severidade: alta.** A Outis não é ferramenta self-serve nem dev-tool. Nunca
escreva como se o cliente fosse configurar, integrar, instalar ou manter
qualquer coisa.

> Ruim: Configure seu agente em minutos. Basta conectar sua conta do WhatsApp e definir os fluxos.
> Bom: A gente monta o agente com o seu cardápio, conecta no seu WhatsApp e entrega funcionando.

Banidas nessa voz: "basta", "é só", "em poucos cliques", "sem código", "faça
você mesmo", "comece grátis", "teste gratuito", "self-service", "dashboard
intuitivo".

### 7.6 Sem travessão, reforço
**Severidade: crítica.** A regra 1.1 vale em dobro nas marcas da casa. Nenhum
travessão em copy, caption, proposta, landing ou e-mail.

---

## 8. Varredura mecânica

Antes de entregar, procure literalmente por estes padrões. São busca de texto,
não julgamento.

```
—  –
estarei |estaremos |vou estar |vamos estar |vai estar
\bpra\b  \bpro\b  \bpros\b
no cenário atual|nos dias de hoje|no mundo de hoje|em um mundo cada vez mais
vale destacar|é importante ressaltar|cabe salientar|não é novidade que
e assim, vemos|em suma|fica claro que|o futuro é
especialistas apontam|estudos mostram|pesquisas indicam|segundo especialistas
não é só|não apenas|mas também|mais do que
pode-se dizer|acredita-se que|faz-se necessário|foi identificado
robusto|panorama|crucial|pivotal|impulsionar|alavancar|potencializar|mergulh
tapeçaria|desvendar|ecossistema|sinergia|holístic|empoderar
#
R\$
```

O resultado da varredura alimenta o `eval.md`. Nenhuma ocorrência de padrão
crítico pode sobreviver à entrega.
