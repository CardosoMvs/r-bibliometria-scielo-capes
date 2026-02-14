# 📊 Framework de Análise Bibliométrica (Scielo & CAPES)

Este repositório contém rotinas automatizadas em **R (R Markdown)** para coleta, mineração e análise de dados acadêmicos. 

O objetivo destes scripts é fornecer um **template reprodutível** para pesquisadores que desejam realizar levantamentos bibliométricos ou revisões sistemáticas de forma programática, garantindo transparência e agilidade no processamento de grandes volumes de dados.

## 🚀 Funcionalidades

O projeto é dividido em dois módulos independentes que podem ser usados em conjunto:

### 1. Módulo Artigos (`Levantamento_Scielo.Rmd`)
Conecta-se ao pacote da Scielo para buscar artigos publicados.
- **Destaques:**
  - Busca automatizada via pacote `easyScieloPack`.
  - **Filtro Lógico Duplo:** Classifica resultados baseando-se na presença de termos no *Título* (maior relevância) ou apenas no *Resumo*.
  - Geração automática de Nuvem de Palavras (Wordcloud) para identificar subtemas.

### 2. Módulo Teses & Dissertações (`Levantamento_CAPES.Rmd`)
Processa a base de dados abertos da CAPES (1987-2022).
- **Destaques:**
  - busca automatizada via pacote `capesR`.
  - **Gestão de Memória:** O script baixa e processa os dados ano a ano, limpando a memória RAM (`gc()`) automaticamente, permitindo a análise de milhões de registros em computadores pessoais.
  - Padronização de nomes de Instituições e Orientadores via `stringi`.
  - Análises geográficas e temporais prontas.

---

## ⚙️ Como Adaptar para Seu Tema

Os scripts foram desenhados com variáveis de controle no início do código. Para pesquisar sobre outro assunto (ex: Inteligência Artificial, Dengue, Educação, etc.), basta alterar os vetores de parâmetros.

### No script Scielo:
Vá até o bloco **2. Parâmetros da Pesquisa** e edite:
```r
# Exemplo: Mudando de "Carbono" para "Inteligência Artificial"
termo_busca_api <- "artificial intelligence" 
tema_interesse <- c("neural networks", "machine learning", "deep learning")
contexto_estudo <- c("health", "medicine", "diagnosis")
```

### No script Capes:
Vá até o bloco **2. Parâmetros da Pesquisa** e edite:
```r
# O script gera automaticamente: "machine learning.*health", "neural networks.*diagnosis", etc.
tema_interesse <- c("machine learning", "deep learning")
contexto_estudo <- c("saúde", "diagnóstico", "hospitalar")
```
A lógica utiliza Regex Combinatória. O script cruza automaticamente todos os termos do tema com todos os termos do contexto.
