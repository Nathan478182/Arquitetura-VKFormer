Título: TCS-V: Uma Representação Vetorial Compacta e Estrutural para Modelos com Raciocínio Explícito

Resumo: Neste trabalho, propomos o TCS-V (Token Contextual Structure Vector), um novo método de geração de vetores de entrada para modelos generativos. O TCS-V busca representar cada token de forma mais rica e interpretável, incorporando elementos estruturais da língua, informações contextuais simplificadas e identificação posicional. O vetor resultante possui 14 dimensões e pode ser utilizado diretamente em redes MLP e mecanismos como VKT-Attention.

1. Introdução Embeddings densos e de alta dimensionalidade têm sido o padrão em modelos de linguagem. No entanto, eles são opacos e pouco interpretáveis. O TCS-V propõe uma abordagem alternativa: criar vetores com semântica fixa, dimensões estruturadas e construção baseada em operações aritméticas e neurônios simples.

2. Estrutura do Vetor TCS-V Cada vetor TCS-V possui 14 dimensões:

10 dimensões representam categorias gramaticais (substantivo, verbo, adjetivo etc.)

3 dimensões representam tokens de contexto que indicam o significado local

1 dimensão representa a posição do token na sequência


3. Construção do Vetor A geração do vetor é feita por uma MLP compacta que recebe como entrada os IDs normalizados dos tokens do contexto. A rede possui:

Camada de entrada com n neurônios (n = tamanho do contexto)

Camada oculta com 13 neurônios (relativos às 13 primeiras dimensões)

Camada de saída com n neurônios, para reatribuir informação por token


As bias são treináveis. Funções de ativação recomendadas incluem GELU ou ReLU.

4. Objetivo e Vantagens O TCS-V busca codificar diferenças estruturais entre tokens e seu significado local em um vetor pequeno e eficiente, possibilitando:

Redução de dimensionalidade

Explicabilidade

Integração direta com mecanismos de atenção escalares

Compatibilidade com MLPs profundas


5. Integração com VKT-Attention O vetor TCS-V pode ser usado como vetor Q no cálculo de atenção VKT. A importância V é treinável por token, e o contexto K é derivado das médias ponderadas dos vetores de todos os outros tokens.

6. Considerações Finais TCS-V oferece uma alternativa à representação vetorial tradicional, com maior eficiência e compreensibilidade. Sua simplicidade estrutural o torna ideal para modelos que priorizam raciocínio simbólico, eficiência computacional e transparência nas decisões.

