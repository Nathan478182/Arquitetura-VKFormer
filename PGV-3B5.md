Título: PGV-3B5: Um Modelo Generativo com Vetores Estruturais e Atenção Escalar para Contextos Estendidos

Resumo: Neste artigo, introduzimos o PGV-3B5 (Pre-trained Generative VKFormer com 3,5 bilhões de parâmetros), um modelo de linguagem generativo que combina uma nova representação vetorial estruturada (TCS-V) com um mecanismo de atenção escalar eficiente (VKT-Attention). O modelo utiliza um tamanho de contexto ampliado de 128.000 tokens e blocos modulares baseados em MLPs profundas, com foco em raciocínio interno, eficiência computacional e interpretação transparente.

1. Introdução Modelos de linguagem modernos geralmente dependem de embeddings de alta dimensionalidade e mecanismos de autoatenção quadráticos. O PGV-3B5 quebra esse paradigma ao empregar vetores de 14 dimensões estruturados (TCS-V) e uma atenção escalar personalizada (VKT-Attention), alcançando desempenho expressivo com 3,5B parâmetros e suporte a janelas contextuais muito superiores às de modelos convencionais.

2. Arquitetura Geral

Input: IDs de tokens

TCS-V: Converte IDs em vetores de 14 dimensões com informação sintática, contextual e posicional

VKT-Attention: Calcula a importância escalar de cada vetor

MLP 1: Camada de processação feedforward inicial

Blocos Empilhados: Cada bloco possui:

TCS-V para recalcular vetores com base em nova entrada

VKT-Attention para recalcular pesos escalares

MLP de 5 camadas com atenção embutida


Output: Logits para geração


3. Detalhes da TCS-V Cada vetor possui:

10 dimensões para categorias gramaticais

3 para contexto semântico

1 para posição do token


Os vetores são calculados por uma MLP que processa IDs normalizados dos tokens do contexto. Essa rede tem:

128.000 entradas (tamanho de contexto)

Camada oculta com 13 neurônios

Saída com 128.000 neurônios

Total de ~25 milhões de parâmetros


4. VKT-Attention Cada vetor possui:

Q: o vetor TCS-V do token

K: média ponderada das dimensões dos vetores do contexto

V: importância treinável do token


A atenção é calculada como:

A_i = Q · V / (K · T)
i = "atenção escalar"

Atenções muito pequenas reduzem a influência do vetor do token nos próximos cálculos. Atenções altas o preservam.

5. MLPs Profundas Cada bloco MLP possui 5 camadas:

Entrada: 1.664.000 dimensões

Camadas ocultas: 256 neurônios (3 camadas)

Saída: 1.664.000 dimensões

Parâmetros por MLP: ~852 milhões

Bias: ~3,3 milhões


6. Configuração PGV-3B5

1 camada inicial (TCS-V + VKT + MLP)

4 blocos empilhados

Total de 5 MLPs (5 camadas cada) = 25 camadas no total

3,5 bilhões de parâmetros totais (pesos + bias + TCS-V)


7. Comparativo

Transformers convencionais: ~2k tokens de contexto para 3B+ parâmetros

PGV-3B5: 128k tokens de contexto com eficiência atencional linear e vetores interpretáveis


8. Considerações Finais O PGV-3B5 representa um novo caminho em modelos generativos, focando em estrutura e interpretação vetorial em vez de representatividade densa. Sua arquitetura baseada em atenção escalar e vetores de baixa dimensão permite aumentar o contexto e raciocínio com eficiência computacional considerável.

