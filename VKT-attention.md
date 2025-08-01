Título: VKT-Attention: Um Mecanismo Escalar de Atenção para Modelos com Contexto Extenso

Resumo: Apresentamos o VKT-Attention, um novo mecanismo de atenção que substitui a tradicional self-attention vetorial por uma atenção escalar eficiente. O VKT-Attention é projetado para cenários com contextos extremamente longos, onde a escalabilidade e a interpretabilidade são cruciais. A abordagem redefine os papéis dos vetores Q, K e V, reduzindo a complexidade computacional e facilitando a integração com camadas MLP padronizadas.

1. Introdução Mecanismos de atenção têm sido fundamentais em arquiteturas modernas, especialmente Transformers. Entretanto, seu custo quadrático em relação ao tamanho do contexto limita a eficiência em tarefas que demandam janelas muito extensas. O VKT-Attention surge como uma alternativa que reformula o conceito de atenção, oferecendo um cálculo escalar simplificado, compatível com representações vetoriais padronizadas.

2. Definição Formal Seja um token com vetor de representação Q e uma importância treinável associada V. Definimos o contexto global K como a média ponderada das representações dos demais tokens.

Adicionalmente, definimos T como o vetor médio dos n tokens antes e depois do token atual, adicionando uma noção local de contexto.

O cálculo da importância escalar do token é dado por:

a = (Q • V) / (K • T)

Onde • denota o produto interno. O valor resultante a é convertido diretamente em uma atenção escalar por adição de uma vírgula decimal (i.e., normalização implícita).

3. Integração com MLPs Ao contrário da atenção convencional que repondera vetores de forma direta, o VKT-Attention atua como um fator de escalonamento. Cada vetor de entrada Q é multiplicado pela sua atenção escalar a, antes de ser processado por camadas MLP subsequentes.

Essa operação resulta em vetores comprimidos ou preservados proporcionalmente à sua relevância contextual, fornecendo um filtro eficaz antes do aprendizado não linear.

4. Complexidade Computacional Com um custo linear em relação ao número de tokens (O(n)), o VKT-Attention possibilita operações em janelas contextuais de tamanho massivo, sem comprometer a escalabilidade.

5. Propriedades e Benefícios

Escalabilidade Extrema: Adequado para contextos >100k tokens.

Baixo custo computacional: Requer apenas produtos escalares e médias.

Simplicidade estrutural: Pode ser embutido diretamente em neurônios MLP.

Interpretabilidade: O escore escalar facilita visualizações de importância entre tokens.


6. Considerações Finais O VKT-Attention representa um caminho promissor para mecanismos de atenção em arquiteturas voltadas para raciocínio simbólico, compressão contextual e escalabilidade. Seus benefícios computacionais e estruturais o tornam especialmente valioso em domínios com limites de memória ou requisitos de interpretabilidade.

