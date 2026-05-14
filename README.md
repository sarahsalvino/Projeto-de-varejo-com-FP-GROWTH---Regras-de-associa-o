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

---

## 🛠️ Tecnologias Utilizadas
- **Python** (Pandas, Numpy)
- **Machine Learning:** MLxtend (FP-Growth)
- **Visualização:** Matplotlib / Seaborn
- **Ambiente:** VS Code / Jupyter Notebook

---
**Desenvolvido por Sarah Cavalcante Salvino** 🚀
