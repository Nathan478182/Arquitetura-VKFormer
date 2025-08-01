# Arquitetura-VKFormer

Este repositório apresenta abordagens de atenção não quadrática, vetores alternativos aos embeddings tradicionais e uma nova arquitetura que tem potencial para superar modelos atuais em eficiência e capacidade de contextualização.

## Componentes principais

### 🔸 VKT-attention
Um mecanismo de atenção escalar, não quadrático, que elimina a necessidade de produtos de QK^T. Ele calcula a importância de cada token com base em um valor treinável (`V`), um vetor de contexto (`K`) e o vetor atual (`Q`). Essa atenção permite maior escalabilidade e foco dinâmico sem multiplicações cruzadas pesadas.

### 🔹 TCS-V (Token Contextual Scalar Vector)
Uma alternativa aos embeddings tradicionais, baseada em vetores de 14 dimensões. Cada vetor incorpora:
- Categoria gramatical (ex: substantivo, verbo, etc.)
- Identificadores de contexto (tokens ao redor)
- Posição do token
Esses vetores são gerados por uma rede leve baseada em operações ponderadas entre os IDs normalizados dos tokens.

---

## 📂 Arquivos incluídos

- `VKT-attention.md` – Explicação técnica do mecanismo de atenção
- `TCS-V.md` – Geração e estrutura dos vetores
- `VKFormer.md` – Arquitetura geral que utiliza ambos os métodos
- `PGV-3B5.md` – Exemplo de modelo com 3.5B de parâmetros e 128k tokens de contexto
- `LICENSE` – Licença MIT (uso livre com crédito ao autor)

---

## ⚙️ Licença

Distribuído sob a licença MIT. Uso comercial e modificações são permitidos, desde que o autor original seja creditado (com link para este repositório ou menção ao nome da conta do GitHub).

---

## ✨ Contribuições

Sugestões, críticas construtivas e melhorias são bem-vindas. Você pode abrir uma _issue_ ou enviar um _pull request_.
