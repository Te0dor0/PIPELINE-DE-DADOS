# Pipeline de Dados Automatizado de Vendas (ETL)

**Autor:** Diego Teodoro
**Tecnologias:** Python, Pandas, SQLAlchemy, Apache Airflow, SQLite, Parquet

---

## 🚀 Visão Geral do Projeto

Este repositório apresenta um **Pipeline ETL Automatizado** de nível de produção, projetado para processar grandes volumes de dados de vendas e clientes. O projeto implementa uma arquitetura robusta que abrange desde a extração e limpeza de dados até transformações de negócios complexas e orquestração automatizada.

O objetivo principal é transformar dados brutos e fragmentados em conjuntos de dados analíticos estruturados e de alta qualidade, permitindo a tomada de decisões baseada em dados por meio de um fluxo de trabalho automatizado e monitorado.

## 🏗️ Arquitetura e Design

O projeto segue uma arquitetura modular e desacoplada, garantindo que cada componente do processo ETL seja independente, testável e escalável.

| Componente | Responsabilidade | Tecnologia |
| :--- | :--- | :--- |
| **Extração** | Ingestão de dados de APIs REST, arquivos CSV, JSON e Parquet. | `Requests`, `Pandas` |
| **Transformação** | Limpeza de dados, padronização, aplicação de lógica de negócios e enriquecimento. | `Pandas`, `NumPy` |
| **Validação** | Garantia da integridade e qualidade dos dados por meio de verificações automatizadas. | Motor de Validação Customizado |
| **Carga** | Persistência de dados processados em bancos de dados relacionais e formatos de arquivo otimizados. | `SQLAlchemy`, `PyArrow` |
| **Orquestração** | Agendamento e monitoramento do fluxo de trabalho de ponta a ponta. | `Apache Airflow` |

### Principais Recursos de Engenharia

- **Extração Resiliente**: Lógica de backoff exponencial e retentativa implementada para chamadas de API usando `tenacity`.
- **Framework de Qualidade de Dados**: Camada de validação integrada que verifica a consistência do esquema, limites de nulos e intervalos de valores antes do carregamento.
- **Logging Estruturado**: Logs formatados em JSON para melhor observabilidade e integração com pilhas de monitoramento (ELK/Datadog).
- **Armazenamento Eficiente**: Utiliza Parquet para snapshots analíticos, reduzindo o espaço de armazenamento e melhorando o desempenho da consulta.
- **Operações Idempotentes**: Projetado para ser executado novamente com segurança, sem duplicar dados ou causar inconsistências.

## 📁 Estrutura do Projeto

```text
.
├── airflow/                   # Camada de Orquestração
│   └── dags/                  # Definições de DAGs do Airflow
├── data/                      # Simulação de Data Lake
│   ├── input/                 # Zona de Aterrissagem (Dados Brutos)
│   └── output/                # Zona Curada (Dados Processados)
├── src/                       # Lógica Central do ETL
│   ├── config/                # Configuração de Ambiente e Logging
│   ├── db_connection/         # Conectores de Banco de Dados
│   ├── extract/               # Módulos de Ingestão
│   ├── transform/             # Lógica de Processamento e Negócios
│   ├── quality/               # Motor de Qualidade de Dados
│   ├── load/                  # Módulos de Persistência
│   └── main.py                # Ponto de Entrada do Pipeline
├── tests/                     # Suíte de Testes Automatizados
├── .env.example               # Modelo de Configuração
└── requirements.txt           # Dependências do Projeto
```

## 🛠️ Primeiros Passos

### Pré-requisitos

- Python 3.11+
- [Apache Airflow](https://airflow.apache.org/) (para orquestração)

### Instalação

1. **Clone o repositório:**
   ```bash
   git clone https://github.com/diego-teodoro/automated-etl-pipeline.git
   cd automated-etl-pipeline
   ```

2. **Configure um ambiente virtual:**
   ```bash
   python -m venv venv
   source venv/bin/activate  # No Windows: venv\Scripts\activate
   ```

3. **Instale as dependências:**
   ```bash
   pip install -r requirements.txt
   ```

4. **Configure as variáveis de ambiente:**
   ```bash
   cp .env.example .env
   # Edite .env com suas configurações específicas
   ```

### Executando o Pipeline

**Execução Manual:**
```bash
python src/main.py
```

**Execução Automatizada (Airflow):**
Copie o conteúdo de `airflow/dags/` para a pasta de DAGs do seu Airflow e acione a DAG `etl_sales_pipeline` através da UI.

## 📈 Monitoramento e Qualidade

O pipeline gera relatórios de execução e logs detalhados. Em caso de falhas, o sistema oferece:
- Contexto de erro detalhado em `logs/error.log`.
- Relatórios de validação de dados destacando problemas específicos de integridade.
- Retentativas automáticas para falhas transitórias.

## 🤝 Contato

**Diego Teodoro**
- Linkedin: www.linkedin.com/in/diego-teodoro-ti
- GitHub: https://github.com/Te0dor0

---
*Este projeto foi desenvolvido para demonstrar habilidades avançadas em Engenharia de Dados usando o ecossistema Python.*
