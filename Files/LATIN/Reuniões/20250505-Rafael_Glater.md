# Apresentação do Rafael Glater - 05/05/2025

- Question Answering Extrativo: Ele mostra onde no texto está a resposta, ao invés de gerar a resposta.
- Não tava conseguindo bater o estado da arte, e agora tá tentando entender quais os viéses que o modelo tem.

## BERT

- Na imagem do modelo de transformer, tem 4 camadas
  - Self Attention
    - Q=Query, K=Key, V=Value; Onde os valores são os pesos aprendidos.
  - Provavelmente o viés está no Self Output (?)

### Answer Position

- Answer Position $\leq 125$ VS Answer Position $> 250$

Dúvida: Por que no final ele usou apenas os dados de $> 250$?

- No F1 Scores ele analisa as respostas aproximadas.

Ele então foi analisar principalmente o módulo de Attention dentro da camada de Self Attention do Transformer.

- O Attention é composto por 12 matrizes.
  - Cada linha é um token da entrada
  - "Essa palavra do índice X dá atenção a quais outras palavras?"
  - A soma de uma linha dá 1
  - A tendência é que as últimas 12 matrizes sejam as que mais apresentem viéses.

**Dúvida:** as imagens das matrizes representam quais dos casos de treino?

**Resposta:** a primeira imagem mostra a média das 12 matrizes finais para os 100 primeiros casos de treino no início; Depois ele mostra a média das 12 matrizes finais para os 100 últimos casos de treino.

Dúvida do Rafael: Se com uma matriz de input, multiplicada por uma matriz Q e somada a um bias gera uma matriz enviesada; então todas as linhas finais terão o mesmo viés. Então de onde surge esse viés?

**Dúvida:** Ele chegou a analisar as variações entre as camadas de atenção?
**Resposta:** Não, mas vai dar uma olhada.

---

#### Answer Position - Embeddings

- **Verde:** Pergunta; **Azul:** Resposta; **Rosa:** início; **Roxo:** início

- **Rodrygo:** Chamar o Mário Sérgio pra falar sobre Teoria da Informação. E a dúvida é: considerando que o modelo tem um viés e ele é observável, você o está observando da forma mais objetiva possível?
  - Com embeddings novos de LLM como Rope, como que ele se comporta? Quais rotas alternativas seriam possíveis?

### Distance and direction to nearest common token

É muito comum que no texto use palavras que estão na pergunta e isso sirva de âncora para encontrar a resposta.

Ele agora vai comparar casos em que os tokens estão próximos à esquerda da resposta e quando eles estão próximos à direita da resposta.

Ele colocou linhas tracejadas amarelas e vermelhas para ilustrar o início e fim da influência de resposta.

Uma possibilidade sugerida é a de usar um dicionário de sinônimos para poder remover essa âncora de palavras que estão presentes no texto.

### Common tokens distance

Agora ele tá comparando a distância das respostas aos tokens, porém mudando a distância: de 1 a 5 vs > 10

### Common tokens directions

Agora ele tá comparando entre respostas à esquerda de tokens presentes na pergunta vs respostas à direita de tokens presentes na pergunta.

**Rodrygo:** Pensando aqui no que é novo... Essa abordagem já foi feita antes?

<!-- [O que é um dataset full?] -->

Uma possibilidade seria criar um dataset não enviesado como Ground-Truth, e depois comparar com o dataset enviesado.

### Input Lenght: Pequenos textos vs Longos textos

### Vieses combinados

- Small input lenght answer at the beginning with tokens at right
- Large input lenght answer at the ending with tokens at left

## Llama

Um problema é que o Llama é generativo e não extrativo.

### Position Bias

## Conclusões

Rodrygo: É importante confirmar que não estamos reinventando a roda. Seria complicado chegar numa conclusão de que o que estamos fazendo.
