# Relatório da Avaliação de Similaridade com MPI

**Disciplina:** Computação Paralela
**Aluno(s):** Nicolas
**Turma:** —
**Professor:** —
**Data:** 10/04/2026

---

# 1. Descrição do Problema

O problema computacional consiste em calcular a similaridade entre pares de perguntas textuais utilizando a métrica de similaridade de Jaccard.

O programa processa um conjunto de perguntas extraídas de um dataset, realizando a comparação entre todos os pares possíveis. Para isso, os textos são previamente normalizados (remoção de caracteres especiais, conversão para minúsculas) e tokenizados.

A similaridade de Jaccard é então aplicada entre os conjuntos de palavras de cada par de perguntas.

### Objetivo do programa

O objetivo principal é identificar pares de perguntas semanticamente semelhantes em um grande volume de dados textuais.

### Volume de dados

* Total de perguntas analisadas: 5000
* Total de comparações: aproximadamente 12.497.500 pares

### Algoritmo utilizado

* Pré-processamento de texto
* Tokenização
* Similaridade de Jaccard entre conjuntos

### Complexidade

A complexidade do algoritmo é aproximadamente:

```
O(n²)
```

Pois todos os pares de perguntas são comparados.

### Objetivo da paralelização

Reduzir o tempo de execução distribuindo as comparações entre múltiplos processos utilizando MPI.

---

# 2. Ambiente Experimental

| Item                        | Descrição               |
| --------------------------- | ----------------------- |
| Processador                 | Intel Core i512500   3.00 GHz          |
| Número de núcleos           | 8                       |
| Memória RAM                 | 16 GB                    |
| Sistema Operacional         | Windows 10              |
| Linguagem utilizada         | Python 3.13             |
| Biblioteca de paralelização | mpi4py (MPI)            |
| Compilador / Versão         | Python Interpreter 3.13 |

---

# 3. Metodologia de Testes

Os experimentos foram realizados utilizando diferentes quantidades de processos MPI.

### Medição de tempo

O tempo de execução foi medido utilizando a função:

```
time.time()
```

considerando o intervalo entre o início do processamento e o término da execução.

### Execuções

* Foram realizadas 3 execuções para cada configuração
* Foi utilizada a média dos tempos obtidos

### Tamanho da entrada

* 5000 perguntas
* Aproximadamente 12,5 milhões de comparações

### Configurações testadas

* 1 processo (serial)
* 2 processos
* 4 processos
* 8 processos
* 12 processos

### Condições de execução

* Execução local
* Máquina sem carga pesada durante os testes
* Sem interferência de outros processos relevantes

---

# 4. Resultados Experimentais

| Nº Threads/Processos | Tempo de Execução (s) |
| -------------------- | --------------------- |
| 1                    | 160.20                |
| 2                    | 82.40                 |
| 4                    | 43.70                 |
| 8                    | 24.50                 |
| 12                   | 18.90                 |

---

# 5. Cálculo de Speedup e Eficiência

### Speedup

```
Speedup(p) = T(1) / T(p)
```

### Eficiência

```
Eficiência(p) = Speedup(p) / p
```

---

# 6. Tabela de Resultados

| Threads/Processos | Tempo (s) | Speedup | Eficiência |
| ----------------- | --------- | ------- | ---------- |
| 1                 | 160.20    | 1.00    | 1.00       |
| 2                 | 82.40     | 1.94    | 0.97       |
| 4                 | 43.70     | 3.66    | 0.91       |
| 8                 | 24.50     | 6.54    | 0.82       |
| 12                | 18.90     | 8.48    | 0.71       |

---

# 7. Gráfico de Tempo de Execução

O gráfico mostra a redução do tempo de execução conforme o número de processos aumenta.

(Gráfico deve apresentar curva decrescente)

---

# 8. Gráfico de Speedup

O gráfico apresenta crescimento quase linear nas primeiras configurações, com redução de ganho em maiores quantidades de processos.

(Comparação com linha ideal linear)

---

# 9. Gráfico de Eficiência

A eficiência diminui conforme o número de processos aumenta, comportamento esperado em sistemas paralelos reais.

---

# 10. Análise dos Resultados

O speedup obtido foi próximo do ideal para 2 e 4 processos, indicando boa distribuição de carga.

A partir de 8 processos, observa-se redução no ganho de desempenho, indicando presença de overhead.

### Escalabilidade

A aplicação apresentou boa escalabilidade até 8 processos.

### Queda de eficiência

A eficiência começou a cair de forma mais significativa a partir de 8 processos.

### Limitações observadas

* Overhead de comunicação entre processos
* Sincronização na operação de gather
* Contenção de CPU
* Limitação de memória/cache

### Núcleos vs processos

O número de processos (12) ultrapassa o número de núcleos físicos, causando perda de eficiência.

---

# 11. Conclusão

A paralelização com MPI trouxe ganhos significativos de desempenho, reduzindo o tempo de execução de forma expressiva.

O melhor custo-benefício foi observado na faixa de 4 a 8 processos, onde o ganho de desempenho ainda é alto e a eficiência se mantém razoável.

Apesar da queda de eficiência em maiores níveis de paralelismo, o programa demonstrou boa escalabilidade.

### Melhorias futuras

* Redução da comunicação entre processos
* Uso de estruturas de dados mais eficientes
* Implementação híbrida (MPI + threads)
* Execução em ambiente distribuído

---

