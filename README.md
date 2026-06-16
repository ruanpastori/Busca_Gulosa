# Busca Gulosa - Mapa da Romênia

## 📚 Sobre o Projeto

Este projeto foi desenvolvido como atividade prática da disciplina de **Inteligência Artificial e Engenharia de Software** do curso de **Big Data Para Industria - FATEC SÃO CARLOS**.

O objetivo é implementar o algoritmo de **Busca Gulosa ** utilizando o clássico problema do **Mapa da Romênia**, apresentado no livro:

> Russell, Stuart; Norvig, Peter. Inteligência Artificial: Uma Abordagem Moderna.

O algoritmo utiliza uma função heurística para estimar a distância entre cada cidade e o objetivo (Bucharest), escolhendo sempre o nó aparentemente mais promissor.

---

# 🎯 Objetivos da Atividade

* Compreender os conceitos de Busca Informada.
* Implementar o algoritmo Busca Gulosa em Python.
* Utilizar heurísticas para guiar a busca.
* Comparar eficiência e qualidade da solução encontrada.
* Aplicar conceitos de Engenharia de Software na documentação e modelagem do sistema.

---

# 🧠 Conceitos Utilizados

## Busca Gulosa 

A Busca Gulosa seleciona sempre o nó com o menor valor da função heurística:

h(n)

Onde:

* h(n) representa a estimativa do custo restante até o objetivo.
* O algoritmo ignora o custo já percorrido.
* Prioriza o caminho que parece mais próximo da solução.

### Vantagens

✅ Simples implementação

✅ Baixo consumo de memória

✅ Encontra soluções rapidamente

### Desvantagens

❌ Não garante o caminho ótimo

❌ Pode encontrar soluções mais caras

---

# 📂 Estrutura do Projeto

```text
busca-gulosa-romenia/
│
├── README.md
├── busca_gulosa.py
├── imagens/
│   ├── diagrama-casos-uso.png
│   ├── diagrama-sequencia.png
│   └── diagrama-estados.png
│
└── docs/
```

---

# 🗺️ Mapa da Romênia

O problema consiste em encontrar um caminho da cidade de Arad até Bucharest.

Cada cidade é representada como um nó do grafo e cada estrada como uma aresta com custo associado.

<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/f5e81026-017a-4a3c-9e9c-7cf0f38e21cf" />

---

# 📌 Estrutura do Grafo

```python
mapa_romenia = {
    'Arad': [('Zerind', 75), ('Sibiu', 140), ('Timisoara', 118)],
    ...
}
```

### Explicação

O grafo é representado por um dicionário Python.

Exemplo:

```python
'Arad': [('Zerind', 75), ('Sibiu', 140)]
```

Significa:

* Arad → Zerind = 75 km
* Arad → Sibiu = 140 km

---

# 📍 Heurística

```python
heuristica_bucareste = {
    'Arad': 366,
    'Sibiu': 253,
    'Fagaras': 176,
    'Bucharest': 0
}
```

### Explicação

A heurística representa a distância em linha reta até Bucharest.

Quanto menor o valor:

* Mais próximo do objetivo.
* Maior a prioridade na busca.

---

# ⚙️ Função Principal

```python
def busca_gulosa(inicio, objetivo, grafo, heuristica):
```

### Parâmetros

| Parâmetro  | Descrição         |
| ---------- | ----------------- |
| inicio     | Cidade inicial    |
| objetivo   | Cidade destino    |
| grafo      | Estrutura do mapa |
| heuristica | Valores h(n)      |

---

# 📌 Fronteira

```python
fronteira = [(heuristica[inicio], inicio, [inicio])]
```

### Explicação

A fronteira armazena:

```python
(h(n), cidade, caminho)
```

Exemplo:

```python
(366, 'Arad', ['Arad'])
```

---

# 📌 Visitados

```python
visitados = set()
```

### Explicação

Evita que uma cidade seja expandida mais de uma vez.

Isso impede:

* Loops infinitos
* Processamento desnecessário

---

# 📌 Ordenação da Fronteira

```python
fronteira.sort(key=lambda x: x[0])
```

### Explicação

Ordena os elementos pelo valor da heurística.

Exemplo:

| Cidade    | h(n) |
| --------- | ---- |
| Sibiu     | 253  |
| Timisoara | 329  |
| Zerind    | 374  |

Sibiu será escolhida primeiro.

---

# 📌 Remoção do Melhor Nó

```python
h_atual, cidade_atual, caminho = fronteira.pop(0)
```

### Explicação

Remove o primeiro elemento da lista.

Como a lista já está ordenada:

* O nó removido sempre possui o menor h(n).

---

# 📌 Teste de Objetivo

```python
if cidade_atual == objetivo:
    return caminho
```

### Explicação

Verifica se o destino foi alcançado.

Se sim:

* Retorna o caminho encontrado.
* Finaliza a execução.

---

# 📌 Expansão dos Vizinhos

```python
for vizinho, _ in grafo.get(cidade_atual, []):
```

### Explicação

Percorre todas as cidades conectadas à cidade atual.

Exemplo:

```python
Sibiu
```

Possui:

* Arad
* Oradea
* Fagaras
* Rimnicu Vilcea

---

# 📌 Inclusão na Fronteira

```python
fronteira.append(
    (heuristica[vizinho], vizinho, novo_caminho)
)
```

### Explicação

Adiciona o vizinho à lista de cidades candidatas.

A prioridade é definida pelo valor de h(n).

---

# 🚀 Resultado da Execução

```text
Expandindo: Arad (h = 366)
Expandindo: Sibiu (h = 253)
Expandindo: Fagaras (h = 176)
Expandindo: Bucharest (h = 0)
```

Caminho encontrado:

```text
Arad -> Sibiu -> Fagaras -> Bucharest
```

---

# 📊 Comparação dos Caminhos

| Caminho                                             | Custo  |
| --------------------------------------------------- | ------ |
| Arad → Sibiu → Fagaras → Bucharest                  | 450 km |
| Arad → Sibiu → Rimnicu Vilcea → Pitesti → Bucharest | 418 km |

### Observação

A Busca Gulosa encontrou rapidamente uma solução, porém não a melhor possível.

Isso acontece porque ela considera apenas a heurística.

---
---

💻 Código Fonte
Implementação Completa da Busca Gulosa
# Grafo representando o mapa da Romênia
mapa_romenia = {
    'Arad': [('Zerind', 75), ('Sibiu', 140), ('Timisoara', 118)],
    'Zerind': [('Arad', 75), ('Oradea', 71)],
    'Oradea': [('Zerind', 71), ('Sibiu', 151)],
    'Sibiu': [('Arad', 140), ('Oradea', 151), ('Fagaras', 99), ('Rimnicu Vilcea', 80)],
    'Timisoara': [('Arad', 118), ('Lugoj', 111)],
    'Lugoj': [('Timisoara', 111), ('Mehadia', 70)],
    'Mehadia': [('Lugoj', 70), ('Drobeta', 75)],
    'Drobeta': [('Mehadia', 75), ('Craiova', 120)],
    'Craiova': [('Drobeta', 120), ('Rimnicu Vilcea', 146), ('Pitesti', 138)],
    'Rimnicu Vilcea': [('Sibiu', 80), ('Craiova', 146), ('Pitesti', 97)],
    'Fagaras': [('Sibiu', 99), ('Bucharest', 211)],
    'Pitesti': [('Rimnicu Vilcea', 97), ('Craiova', 138), ('Bucharest', 101)],
    'Bucharest': [('Fagaras', 211), ('Pitesti', 101), ('Giurgiu', 90), ('Urziceni', 85)],
    'Giurgiu': [('Bucharest', 90)],
    'Urziceni': [('Bucharest', 85), ('Vaslui', 142), ('Hirsova', 98)],
    'Hirsova': [('Urziceni', 98), ('Eforie', 86)],
    'Eforie': [('Hirsova', 86)],
    'Vaslui': [('Urziceni', 142), ('Iasi', 92)],
    'Iasi': [('Vaslui', 92), ('Neamt', 87)],
    'Neamt': [('Iasi', 87)]
}

# Heurística (distância em linha reta até Bucareste)
heuristica_bucareste = {
    'Arad': 366,
    'Bucharest': 0,
    'Craiova': 160,
    'Drobeta': 242,
    'Eforie': 161,
    'Fagaras': 176,
    'Giurgiu': 77,
    'Hirsova': 151,
    'Iasi': 226,
    'Lugoj': 244,
    'Mehadia': 241,
    'Neamt': 234,
    'Oradea': 380,
    'Pitesti': 100,
    'Rimnicu Vilcea': 193,
    'Sibiu': 253,
    'Timisoara': 329,
    'Urziceni': 80,
    'Vaslui': 199,
    'Zerind': 374
}

def busca_gulosa(inicio, objetivo, grafo, heuristica):

    fronteira = [(heuristica[inicio], inicio, [inicio])]
    visitados = set()

    print(f"--- Iniciando Busca Gulosa de {inicio} para {objetivo} ---")

    while fronteira:

        fronteira.sort(key=lambda x: x[0])

        h_atual, cidade_atual, caminho = fronteira.pop(0)

        print(f"Expandindo: {cidade_atual} (h = {h_atual})")

        if cidade_atual == objetivo:
            return caminho

        if cidade_atual not in visitados:

            visitados.add(cidade_atual)

            for vizinho, _ in grafo.get(cidade_atual, []):

                if vizinho not in visitados:

                    novo_caminho = caminho + [vizinho]

                    fronteira.append(
                        (heuristica[vizinho], vizinho, novo_caminho)
                    )

    return None


caminho_final = busca_gulosa(
    'Arad',
    'Bucharest',
    mapa_romenia,
    heuristica_bucareste
)

print("\n--- Resultado ---")

if caminho_final:
    print("Caminho encontrado:",
          " -> ".join(caminho_final))
else:
    print("Não foi possível encontrar um caminho.")
---

# 📐 Diagramas UML

## Diagrama de Casos de Uso

![Diagrama de Casos de Uso](imagens/diagrama-casos-uso.png)

### Casos de Uso

* Informar cidade de origem
* Informar cidade destino
* Executar busca
* Visualizar caminho encontrado

---

## Diagrama de Sequência

![Diagrama de Sequência](imagens/diagrama-sequencia.png)

Fluxo:

1. Usuário inicia busca
2. Sistema cria fronteira
3. Sistema ordena nós pela heurística
4. Sistema expande nós
5. Sistema encontra objetivo
6. Sistema retorna caminho

---

## Diagrama de Estados

![Diagrama de Estados](imagens/diagrama-estados.png)

Estados:

```text
Início
 ↓
Criar Fronteira
 ↓
Expandir Nó
 ↓
Objetivo Encontrado?
 ↓
Sim → Finalizar
Não → Expandir Próximo Nó
```

---

# 🛠️ Tecnologias Utilizadas

* Python 3
* Algoritmos de Busca
* Estruturas de Dados
* UML
* Git
* GitHub

---

# 📖 Referências

RUSSELL, Stuart; NORVIG, Peter.

Artificial Intelligence: A Modern Approach.

Pearson Education.
