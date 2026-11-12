# Prática 2 — Comunicação e sincronização em sistemas distribuídos

Atividade de Plataformas e Sistemas de Alto Desempenho da UVA. O desafio foi incluir o quinto nó na simulação em Python. Nos relógios lógicos, ele é identificado pela letra **E**.

## Como executar no VS Code

Abra a pasta do projeto no VS Code e execute no terminal com Python 3.9 ou superior:

```bash
python pratica2_comunicacao_sincronizacao.py
```

No Windows, também é possível usar `py` no lugar de `python`. O projeto usa a biblioteca padrão. A calculadora e o registro de nomes se comunicam em `127.0.0.1`.

## Como verificar a inclusão do quinto nó

```bash
python pratica2_comunicacao_sincronizacao.py --modo relogios
```

A instrução `e = Relogio("E", 4)` associa E à quinta posição do vetor. Depois de um evento local, a saída é:

```text
Evento independente E: L=1, V=[0, 0, 0, 0, 1]
```

## Demonstrações

| Modo | Resultado da execução |
| --- | --- |
| `rpc` | A calculadora retorna 10 para 6 + 4 e 24 para 6 × 4. A barreira original retorna TIMEOUT para os clientes 1 e 6. |
| `relogios` | A e B registram eventos independentes. No envio de A para B, o relógio de Lamport passa de 2 no envio para 3 no recebimento. C, D e E também registram eventos locais. |
| `eleicao` | Com o nó 5 indisponível, o nó 4 vence a eleição Bully simulada. |
| `maioria` | Na votação independente da eleição, o participante 5 vota pela recusa. A proposta recebe três votos favoráveis entre cinco e é aprovada. |

## Resultado da barreira no código entregue

A condição de liberação exige cinco clientes distintos. O laço `for i in (1, 6)` cria somente dois, embora a mensagem de tela mencione três. Ambos aguardam até o limite de oito segundos. Para reproduzir o ensaio de controle descrito no relatório, troque o laço por `for i in range(1, 6)` em uma cópia e execute o modo `rpc`. Os cinco clientes recebem `LIBERADO`.
