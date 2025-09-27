# 🏙️ Análise Airbnb em Nova York - Dashboard Power BI

## 📋 Visão Geral

Este projeto apresenta uma análise completa dos dados do Airbnb em Nova York, desenvolvido em Power BI utilizando o formato PBIP para melhor controle de versão e colaboração. O dashboard oferece insights sobre preços, disponibilidade, localização e classificação das propriedades na cidade de Nova York.

**🎯 Objetivo:** Fornecer uma visão analítica dos dados do Airbnb em NYC para auxiliar na tomada de decisões de investidores, hosts e viajantes.

**👥 Público-alvo:** Analistas de dados, investidores imobiliários, hosts do Airbnb e pesquisadores do mercado de acomodações.

**📅 Última atualização:** Setembro 2025

---

## 🎓 Objetivos de Aprendizado

Este projeto foi desenvolvido com caráter educacional e visa consolidar conhecimentos em análise de dados e Business Intelligence. Os principais objetivos de aprendizado incluem:

### **📊 Power BI & Visualização de Dados**
- Construção de **dashboards interativos** e profissionais
- Implementação de **mapas geográficos** com coordenadas latitude/longitude
- Criação de **temas personalizados** e identidade visual
- Uso de **filtros dinâmicos** e interatividade entre visuais

### **🔧 Modelagem de Dados**
- Aplicação de **transformações no Power Query** (linguagem M)
- Criação de **colunas calculadas** com fórmulas DAX
- Implementação de **classificações automáticas** baseadas em regras de negócio
- Organização de **relacionamentos** entre tabelas

### **⚙️ Controle de Versão & Colaboração**
- Utilização do formato **PBIP** para versionamento em Git
- Estruturação de projetos Power BI para **trabalho em equipe**
- Aplicação de **boas práticas** de documentação técnica
- Integração entre **Power BI Desktop** e repositórios GitHub

### **📈 Análise Exploratória de Dados**
- **Limpeza e tratamento** de datasets reais
- Identificação de **padrões e insights** em dados de hospedagem
- Criação de **métricas de performance** e KPIs
- Análise **geoespacial** de propriedades urbanas

### **🏗️ Engenharia de Dados**
- Configuração de **fontes de dados** externas
- Implementação de **pipelines de transformação**
- Otimização de **performance** em modelos de dados
- Aplicação de **time intelligence** e calendários customizados

---

## 🎨 Recursos do Dashboard

### 📊 **Principais Visualizações**
- **Mapa Interativo**: Distribuição geográfica das propriedades com latitude/longitude
- **Análise de Preços**: Visualização por bairros e tipos de acomodação
- **Classificação por Padrão**: Categorização automática (Baixo, Médio, Alto, Altíssimo)
- **Métricas de Performance**: Reviews, disponibilidade e listagens por host

### 🏷️ **Tema Personalizado**
- Interface customizada com tema próprio (`tema_matheus`)
- Imagem de capa personalizada (`capa_menu_pbi`)
- Design otimizado para apresentações profissionais

---

## 📂 Estrutura do Projeto

```
AirBnB-in-NY/
├── 📄 README.md
├── 🎯 air_bnb_ny.pbip                    # Arquivo principal do projeto
├── 📊 air_bnb_ny.Report/                 # Configurações do relatório
│   ├── definition/
│   │   ├── pages/                        # 3 páginas de análise
│   │   ├── report.json                   # Configurações globais
│   │   └── version.json                  # Controle de versão
│   └── StaticResources/                  # Temas e recursos visuais
└── 🗃️ air_bnb_ny.SemanticModel/         # Modelo de dados
    ├── definition/
    │   ├── tables/                       # Tabelas e colunas
    │   └── model.tmdl                    # Definição do modelo
    └── diagramLayout.json                # Layout das relações
```

---

## 📊 Modelo de Dados

### **🗂️ Tabelas Principais**

#### **`dados` (Tabela Principal)**
- **ID**: Identificador único da propriedade
- **Informações do Host**: `host_id`, `host_name`, `calculated_host_listings_count`
- **Localização**: `neighbourhood_group`, `neighbourhood`, `latitude`, `longitude`
- **Propriedade**: `name`, `room_type`, `price`, `minimum_nights`
- **Reviews**: `number_of_reviews`, `last_review`, `reviews_per_month`
- **Disponibilidade**: `availability_365`

#### **`1 - Calendário`**
- Tabela de dimensão temporal para análises de time intelligence

#### **`2 - Medidas`**
- Medidas DAX calculadas para KPIs e métricas personalizadas

#### **`host_id_summerized`**
- Dados agregados por host para análises de performance

### **🧮 Colunas Calculadas Principais**

```dax
// Preço Total Estimado
total_price = dados[price] * dados[minimum_nights]

// Classificação Automática por Padrão
classification = 
SWITCH(
    TRUE(),
    dados[total_price] <= 1000, "Baixo Padrão",
    dados[total_price] > 1000 && dados[total_price] <= 10000, "Médio Padrão", 
    dados[total_price] > 10000 && dados[total_price] <= 100000, "Alto Padrão",
    "Altíssimo Padrão"
)

// Índice para Ordenação
classification_index = 
SWITCH(
    TRUE(),
    dados[total_price] <= 1000, 1,
    dados[total_price] > 1000 && dados[total_price] <= 10000, 2,
    dados[total_price] > 10000 && dados[total_price] <= 100000, 3,
    4
)
```

---

## 🚀 Como Utilizar

### **📋 Pré-requisitos**
- Power BI Desktop (versão atual recomendada)
- Dataset CSV: `train.csv` (localizado em `https://www.kaggle.com/datasets/thedevastator/airbnbs-nyc-overview/data`)

### **⚙️ Configuração**

1. **Clone o repositório:**
   ```bash
   git clone https://github.com/mm-borges/AirBnB-in-NY.git
   cd AirBnB-in-NY
   ```

2. **Abra o arquivo PBIP:**
   - Abra o Power BI Desktop
   - Navegue até `Arquivo > Abrir`
   - Selecione `air_bnb_ny.pbip`

3. **Configure a fonte de dados:**
   - Atualize o caminho do arquivo CSV se necessário
   - Vá em `Transformar dados > Configurações da fonte de dados`
   - Ajuste o caminho para o local do seu dataset

4. **Atualize os dados:**
   - Clique em `Atualizar` na faixa de opções
   - Aguarde o carregamento completo dos dados

---

## 🔍 Páginas do Dashboard

### **📍 Página 1: Visão Geral**
- KPIs principais (total de propriedades, preço médio, etc.)
- Distribuição por borough
- Gráficos de tendência temporal

### **🗺️ Página 2: Análise Geográfica** 
- Mapa interativo com densidade de propriedades
- Análise por neighborhood_group
- Filtros por tipo de quarto e faixa de preço

### **💰 Página 3: Análise Financeira**
- Classificação por padrão de preço
- Análise de hosts mais ativos
- Métricas de reviews e disponibilidade

---

## 🛠️ Configurações Técnicas

### **🌐 Configurações Regionais**
- **Cultura**: Português (Brasil) - `pt-BR`
- **Moeda**: Dólar americano (USD)
- **Formato de Data**: Formato curto

### **📊 Configurações do Power BI**
- **Time Intelligence**: Habilitado
- **Modo Desenvolvedor**: Ativo
- **Versão do Relatório**: 2.0.0
- **Auto Recovery**: Habilitado

---

## 📈 Funcionalidades Avançadas

### **🔄 Transformações de Dados (Power Query)**
- Promoção automática de cabeçalhos
- Transformação de tipos de dados com localização
- Remoção de linhas com erros e valores nulos
- Tratamento especializado para dados monetários e geográficos

### **🎨 Recursos Visuais**
- Tema customizado aplicado globalmente
- Imagens personalizadas integradas
- Layout responsivo otimizado
- Tooltips aprimorados habilitados

---

## 🤝 Contribuição

Contribuições são bem-vindas! Para contribuir:

1. Fork o projeto
2. Crie uma branch para sua feature (`git checkout -b feature/AmazingFeature`)
3. Commit suas mudanças (`git commit -m 'Add some AmazingFeature'`)
4. Push para a branch (`git push origin feature/AmazingFeature`)
5. Abra um Pull Request

---

## 👨‍💻 Autor

**Matheus Melo Borges**
- 🌍 [LinkedIn](https://www.linkedin.com/in/matheus-melo-borges/)
- 📧 [Email](matheusmeloborges@gmail.com)
- 😺 [GitHub](https://github.com/mm-borges)

---

### ⭐ Este projeto foi desenvolvido para fins educacionais e de demonstração, através de exercício proposto durante curso de Análise de Dados em [Comunidade DS](https://comunidadeds.com/)
