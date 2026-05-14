# 🛒 Análise de Dados de Varejo & Regras de Associação com FP-Growth

Este projeto consiste em uma análise exploratória de dados (EDA) e na implementação de um modelo de Machine Learning para recomendação de produtos em um cenário de varejo multissetorial.

## 📌 Objetivo do Projeto
O desafio foi dividido em duas etapas principais:
1. **Análise de Negócio:** Responder a perguntas estratégicas para auxiliar gestores na tomada de decisão e identificação de gargalos.
2. **Modelo Preditivo:** Implementar um sistema de recomendação baseado em associações de itens, focando no setor de **Department Store**.

---

## 📊 1. Análise Exploratória (Geral)
Nesta etapa, foram respondidas questões fundamentais para a saúde do negócio:
- **Volume de Vendas:** Total de itens vendidos e faturamento global.
- **Eficiência por Unidade:** Desempenho e representatividade de cada `Store_type`.
- **Comportamento do Consumidor:** Métodos de pagamento preferenciais e análise de ticket médio.
- **Logística Temporal:** Identificação de picos de vendas por hora e dia da semana em cada cidade.

---

## 🏬 2. Foco no Setor: Department Store
Após a visão geral, a análise foi aprofundada no setor de **Lojas de Departamento**, onde foram realizados recortes para entender:
- Itens de maior e menor frequência.
- Preferências de compra por perfil de cliente.

---

## 🤖 3. Modelo: FP-Growth
Para a recomendação de itens, utilizei o algoritmo **FP-Growth (Frequent Pattern Growth)**.

### Por que FP-Growth?
Diferente do algoritmo Apriori, o FP-Growth não gera candidatos de forma exaustiva. Ele armazena o dataset em uma estrutura de árvore (FP-Tree), o que o torna **significativamente mais rápido e eficiente em memória**, especialmente em datasets grandes.

### Métricas Utilizadas:
- **Support:** Frequência com que o conjunto de itens aparece.
- **Confidence:** Probabilidade de compra do item B dado que o item A foi comprado.
- **Lift:** Força da associação. Um lift > 1 indica que os itens são comprados juntos mais vezes do que o esperado se fossem independentes.

---

## 📉 Análise dos Resultados e Tuning
Durante o desenvolvimento, foi realizado o **tuning dos hiperparâmetros**, ajustando os níveis de suporte mínimo e confiança. 

> [!IMPORTANT]
> **Nota sobre os dados:** Observou-se que as métricas de suporte e confiança apresentaram valores baixos. Após investigação e testes, concluiu-se que isso ocorre devido à natureza do dataset (dados fictícios), que apresenta uma distribuição de produtos com alta repetição aleatória entre os setores, o que dilui a força das associações estatísticas reais.

---

## 💡 Conclusões
Apesar das limitações dos dados, o modelo identificou **300 regras** com associação real (`lift > 1`). Abaixo, as principais associações bidirecionais agrupadas por perfil:

### 🛍️ Perfis Identificados
1. **Cross-sell Direto** (Complementaridade imediata):
   - `Esponjas ↔ Sabão` (Lift: 1.06)
   - `Creme de Barbear ↔ Lâminas` (Lift: 1.06)
   - `Mangueira ↔ Água` (Lift: 1.09)

2. **Perfil Culinário** (Uso em preparo de refeições):
   - `Queijo ↔ Mostarda` (Lift: 1.11)
   - `Vinagre ↔ Atum` (Lift: 1.08)
   - `Tomate ↔ Panos de Limpeza` (Lift: 1.12)

3. **Compra Semanal** (Itens domésticos e perecíveis):
   - `Laranja ↔ Leite` / `Frango ↔ Banana` (Reposição de frescos).
   - `Fraldas ↔ Purificador de Ar` (Perfil de pais com bebês).
   - `Cereal ↔ Pá de Lixo` (Padrão de compra mensal de suprimentos).


  ### 📈 Exemplos de Perfis Identificados (Department Store)
Note que, embora a **Confiança** seja numericamente baixa (característica do dataset disperso), o **Lift** consistentemente acima de 1 confirma a existência de um padrão de associação entre os itens:


Antecedente ↔ ConsequenteSuporteConfiançaLiftSponges ↔ Soap0.0013923.81%1.0594Shaving Cream ↔ Razors0.0013443.76%1.0593Garden Hose ↔ Water0.0014644.02%1.0938Cheese ↔ Mustard0.0014644.05%1.1094Tuna ↔ Vinegar0.0013623.85%1.0799Tomatoes ↔ Cleaning Rags0.0014584.01%1.1185Orange ↔ Milk0.0013923.85%1.0724Banana ↔ Chicken0.0013743.81%1.0720Diapers ↔ Air Freshener0.0014043.91%1.0781Dustpan ↔ Cereal0.0013983.93%1.0986
Antecedente ↔ Consequente	Suporte	Confiança	Lift

Sponges ↔ Soap	0.001392	3.81%	1.0594
Shaving Cream ↔ Razors	0.001344	3.76%	1.0593
Garden Hose ↔ Water	0.001464	4.02%	1.0938

Cheese ↔ Mustard	0.001464	4.05%	1.1094
Tuna ↔ Vinegar	0.001362	3.85%	1.0799
Tomatoes ↔ Cleaning Rags	0.001458	4.01%	1.1185

Orange ↔ Milk	0.001392	3.85%	1.0724
Banana ↔ Chicken	0.001374	3.81%	1.0720
Diapers ↔ Air Freshener	0.001404	3.91%	1.0781
Dustpan ↔ Cereal	0.001398	3.93%	1.0986


<img width="834" height="552" alt="gráfico" src="https://github.com/user-attachments/assets/76efd8ed-4c94-450f-a772-a237d649dd82" />


---

## 🛠️ Tecnologias Utilizadas
- **Python** (Pandas, Numpy)
- **Machine Learning:** MLxtend (FP-Growth)
- **Visualização:** Matplotlib / Seaborn
- **Ambiente:** VS Code / Jupyter Notebook

---
