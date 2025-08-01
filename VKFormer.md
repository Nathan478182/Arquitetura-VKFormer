Paper: Arquitetura VKFormer — Uma Estrutura Modular para Modelos com Contexto Extendido e Atenção Escalar


---

Resumo
VKFormer é uma arquitetura de rede neural projetada para permitir raciocínio iterativo, representação contextual rica e eficiência computacional em tarefas de modelagem de linguagem. Ela é composta por dois componentes principais: os vetores TCS-V (Token Contextual Summary Vector) e o mecanismo de atenção VKT-Attention (Value-Key-Token Attention). A arquitetura se organiza em blocos modulares com camadas MLP, podendo ser configurada para diferentes tamanhos de contexto e capacidade de modelo.


---

1. Introdução
Enquanto arquiteturas baseadas em Transformer atingiram grande sucesso, seu custo de atenção quadrático em relação ao tamanho do contexto limita sua escalabilidade. VKFormer busca resolver isso com uma atenção mais enxuta e vetores de representação ricos e compactos. A arquitetura é especialmente adaptada para contextos muito longos (centenas de milhares de tokens), mantendo o custo computacional controlado.


---

2. Componentes Centrais

2.1 TCS-V (Token Contextual Summary Vector)
TCS-V gera vetores de 14 dimensões para cada token, baseando-se em informações morfossintáticas, IDs de tokens vizinhos e sua posição na sequência. Essa representação é produzida por uma rede densa com pesos compartilhados que processa os IDs normalizados dos tokens de entrada. O vetor é compacto, mas informativo o suficiente para carregar diferenças semânticas relevantes.

2.2 VKT-Attention
Ao invés da atenção tradicional baseada em multiplicação de matrizes QK^T, a VKT-Attention usa apenas três elementos:

V: uma importância treinável para cada token

K: um vetor global contextual derivado da média ponderada de todos os vetores

Q (opcional): o vetor do token atual


A atenção escalar resultante modula a contribuição de cada vetor nas camadas seguintes, reduzindo o cálculo de atenção a operações aritméticas simples com custo linear.


---

3. Estrutura da Arquitetura
A arquitetura é formada por blocos que seguem a estrutura:

1. Geração dos vetores TCS-V a partir dos IDs


2. Cálculo da atenção VKT-Attention sobre os vetores


3. Passagem por uma MLP feedforward


4. Encadeamento para o próximo bloco



Cada bloco realiza um ciclo de contextualização e transformação vetorial, permitindo que a rede desenvolva raciocínio de forma iterativa.


---

4. Flexibilidade e Escalabilidade

VKFormer é uma arquitetura, não um modelo específico. Assim, ela pode ser configurada com:

Diferentes tamanhos de contexto (ex: 4k a 128k tokens)

Tamanhos variáveis de vetores TCS-V (ex: 14D, 32D, etc.)

Diferentes profundidades (número de blocos)

Tamanhos distintos de MLPs


Essa flexibilidade permite a criação de modelos otimizados para diferentes tarefas ou orçamentos computacionais.


---

5. Exemplo de Modelo: PGV-3B5
Um exemplo concreto é o modelo PGV-3B5, um VKFormer com:

3.5 bilhões de parâmetros

128.000 tokens de contexto

Vetores TCS-V de 14 dimensões

4 blocos de MLPs (5 camadas cada)


Esse modelo demonstra a escalabilidade da arquitetura, atingindo contextos raramente acessíveis por modelos Transformer com esse nível de parâmetros.


---

6. Considerações Finais
VKFormer abre caminho para modelos com maior capacidade de raciocínio sequencial e escalabilidade contextual, mantendo a interpretabilidade e modularidade. Sua atenção escalar e vetores contextuais oferecem uma alternativa leve, mas expressiva, ao Transformer clássico.

Trabalhos futuros podem explorar variantes com compressão de embeddings, fúsão de vetores simbólicos, e adaptação a tarefas multimodais.


---

