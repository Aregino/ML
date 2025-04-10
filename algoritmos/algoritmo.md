
## **Árvore de Decisão**


É como separa os dados em conjunto homogeneo, os nós, tendo como maior ganho para que seja ideal. Separar em "Baldes" aquele conjunto mais homogeneo, porem como foi falado nao deve ficar muito personalizado para modelo de machine learning que ai tb nao vai funcionar adequadamente 

Claro, Andre! Vamos falar de forma **bem didática** sobre o algoritmo de **Árvore de Decisão**, que é um dos mais simples e intuitivos em **machine learning**.

---

## 🌳 O que é uma Árvore de Decisão?

Uma **Árvore de Decisão** é um modelo que **simula decisões humanas**, como se fosse um fluxograma. Ela serve para **classificar** ou **prever** valores com base em perguntas **simples** e **binárias** (sim/não, maior/menor, etc.).

---

### 🔍 Como funciona?

Ela divide os dados em **ramificações**, fazendo perguntas sobre os atributos dos dados, até chegar a uma **decisão final** (folha da árvore).

---

## 🎯 Exemplo simples: "Vamos sair para passear?"

Imagina que queremos decidir **se devemos sair para passear** ou não, com base em 3 fatores:

- ☁️ Está chovendo?
- 📈 Temperatura está acima de 20°C?
- 📅 É fim de semana?

---

### 🌳 Árvore de decisão (simples):

```text
                 Está chovendo?
                    /     \
                 Sim       Não
                /           \
           Não saímos     Temperatura > 20?
                            /         \
                         Sim         Não
                        /              \
                É fim de semana?     Não saímos
                    /     \
                 Sim       Não
               Saímos     Não saímos
```

---

### ✅ Testando com um exemplo:

- Está chovendo? ❌ (não)
- Temperatura > 20°C? ✅ (sim)
- É fim de semana? ✅ (sim)

➡️ Resultado final: **Saímos!**

---

## 🧠 Como o algoritmo monta essa árvore?

Ele escolhe **as melhores perguntas (atributos)** para dividir os dados usando critérios como:

- **Ganho de Informação (Information Gain)**
- **Índice de Gini**

Esses critérios medem **quão bem uma pergunta separa os dados** em grupos homogêneos.

---

## 🛠 Aplicações na prática

- Diagnóstico médico 🏥
- Análise de crédito 💳
- Detecção de fraudes 🔍
- Previsão de vendas 📊

---

## ⚖️ Vantagens

- Fácil de entender e visualizar.
- Funciona com dados categóricos e numéricos.
- Pouco pré-processamento.

---

## ⚠️ Desvantagens

- Pode se tornar muito complexa (overfitting).
- Sensível a pequenas mudanças nos dados.

---

Se quiser, posso te mostrar um exemplo em **Python com sklearn**, usando dados reais como o famoso dataset de **Iris** ou de **Titanic**. Quer ver um desses exemplos?


Show! Vamos usar o dataset do **Titanic** 🛳️, que é clássico para aprendizado de modelos de classificação.

---

## 🎯 Objetivo:
Prever se uma pessoa **sobreviveu** ou **não**, com base em algumas características (idade, sexo, classe do navio, etc).

Vamos usar o modelo de **Árvore de Decisão** do `scikit-learn`.

---

## 📦 Instale se precisar:
```bash
pip install pandas scikit-learn seaborn matplotlib
```

---

## 💻 Código em Python:

```python
import pandas as pd
from sklearn.tree import DecisionTreeClassifier, plot_tree
from sklearn.model_selection import train_test_split
from sklearn.metrics import accuracy_score
import seaborn as sns
import matplotlib.pyplot as plt

# Carregando o dataset do Titanic
df = sns.load_dataset("titanic")

# Selecionando colunas importantes e removendo linhas com valores ausentes
df = df[["survived", "pclass", "sex", "age"]].dropna()

# Convertendo variável categórica 'sex' para numérica
df["sex"] = df["sex"].map({"male": 0, "female": 1})

# Separando X (atributos) e y (alvo)
X = df[["pclass", "sex", "age"]]
y = df["survived"]

# Dividindo em treino e teste
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# Criando o modelo de Árvore de Decisão
modelo = DecisionTreeClassifier(max_depth=3, random_state=42)
modelo.fit(X_train, y_train)

# Fazendo previsões
y_pred = modelo.predict(X_test)

# Avaliando o modelo
print(f"Acurácia: {accuracy_score(y_test, y_pred):.2f}")

# Plotando a árvore
plt.figure(figsize=(12, 6))
plot_tree(modelo, feature_names=X.columns, class_names=["Não Sobreviveu", "Sobreviveu"], filled=True)
plt.title("Árvore de Decisão - Titanic")
plt.show()
```

---

### 🧠 Interpretação da Árvore

- O modelo decide, por exemplo:
  - Se o passageiro for mulher (`sex=1`) e tiver menos de certa idade, há maior chance de sobreviver.
  - Passageiros da **primeira classe** tinham maior chance de sobrevivência.
  - Homens da **terceira classe** tinham menor chance.

---
