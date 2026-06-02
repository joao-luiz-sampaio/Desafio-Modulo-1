# Data Warehouse para Otimização de Preços no Airbnb Rio de Janeiro

## Sobre o Projeto

Este projeto foi desenvolvido como atividade prática do Módulo 1 do curso de Data Analytics, com foco na aplicação dos conceitos de Data Warehouse, Modelagem de Dados, SQL e Análise Exploratória de Dados.

Utilizando dados públicos do Airbnb referentes à cidade do Rio de Janeiro, foi construída uma solução analítica baseada em modelagem dimensional para apoiar análises de precificação e sazonalidade no mercado de hospedagem.

**Data de apresentação:** 07/04/2026

---

## Objetivo

Desenvolver uma estrutura de Data Warehouse capaz de armazenar e organizar dados de anúncios do Airbnb, permitindo análises relacionadas à influência da localização geográfica e da sazonalidade sobre os preços das diárias.

O projeto contempla:

* Modelagem conceitual e lógica dos dados;
* Implementação física do Data Warehouse em PostgreSQL;
* Processos de carga utilizando SQL;
* Consultas analíticas para suporte à tomada de decisão.

---

## Fonte dos Dados

Os dados utilizados foram obtidos através da plataforma Inside Airbnb.

Fonte:

https://insideairbnb.com/get-the-data/

Base utilizada:

* Rio de Janeiro – Brasil

---

## Problema de Negócio

### Otimização de Preço

**Pergunta de negócio:**

> Qual a variação média de preço por bairro e por temporada?

### Contexto

A localização geográfica e a sazonalidade são fatores determinantes para a definição dos preços das hospedagens.

O objetivo da análise é compreender como diferentes bairros e períodos do ano impactam os valores das diárias, permitindo a criação de estratégias de precificação dinâmica para anfitriões e plataformas de hospedagem.

---

## Arquitetura da Solução

Foi adotado o modelo dimensional Star Schema (Modelo Estrela), garantindo alta performance para consultas analíticas.

### Dimensão Localização (dim_localizacao)

Responsável por armazenar informações geográficas dos imóveis.

**Atributos:**

* Bairro
* Grupo de bairro
* Latitude
* Longitude

### Dimensão Host (dim_host)

Responsável por armazenar informações dos anfitriões.

**Atributos:**

* ID do Host
* Nome do Host

### Dimensão Imóvel (dim_imovel)

Responsável pelas características dos anúncios.

**Atributos:**

* ID do anúncio
* Nome do anúncio
* Tipo de acomodação
* Licença

### Fato Anúncios (fato_anuncios)

Tabela central contendo as métricas de negócio.

**Métricas armazenadas:**

* Preço da diária
* Quantidade de avaliações
* Data da última avaliação
* Temporada de atividade

---

## Modelo Estrela

```text
                dim_host
                    |
                    |
dim_localizacao ---- fato_anuncios ---- dim_imovel
```

---

## Regras de Negócio Aplicadas

A sazonalidade foi criada a partir do mês da última avaliação registrada no anúncio.

| Estação   | Meses                         |
| --------- | ----------------------------- |
| Verão     | Dezembro, Janeiro e Fevereiro |
| Outono    | Março, Abril e Maio           |
| Inverno   | Junho, Julho e Agosto         |
| Primavera | Setembro, Outubro e Novembro  |

Anúncios sem atividade registrada foram classificados como:

* Sem Atividade

---

## Consultas Analíticas Desenvolvidas

### Preço Médio por Bairro e Temporada

A consulta principal calcula:

* Preço médio por bairro;
* Estação do ano associada à atividade do anúncio;
* Quantidade de imóveis analisados.

### Ranking dos Bairros Mais Econômicos

Foi desenvolvida uma segunda consulta utilizando Window Functions para identificar:

* Os 3 bairros mais baratos de cada estação do ano;
* Ranking de preços por temporada;
* Comparação entre regiões da cidade.

---

## Resultados Obtidos

As análises permitiram identificar diferenças significativas entre bairros e períodos do ano.

Os resultados demonstraram que:

* A localização exerce forte influência sobre o valor das diárias;
* Bairros com maior atratividade turística mantêm preços elevados durante todo o ano;
* A sazonalidade afeta diretamente o comportamento dos preços;
* O verão apresentou os maiores valores médios de hospedagem entre as estações analisadas.

---

## Conclusões

### Impacto Geográfico

A localização não é apenas um endereço, mas um dos principais fatores de valorização dos imóveis anunciados.

Bairros com maior densidade turística apresentaram maior resiliência nos preços mesmo durante períodos de menor demanda.

### Sazonalidade

A métrica de Temporada de Atividade demonstrou que anúncios ativos durante o verão possuem preços médios significativamente superiores aos observados nas demais estações.

Esse comportamento reforça a importância da adoção de estratégias de precificação dinâmica ajustadas conforme a sazonalidade do mercado.

---

## Tecnologias Utilizadas

* PostgreSQL
* SQL
* pgAdmin
* Data Warehouse
* Modelagem Dimensional
* GitHub

---

## Autores

Projeto desenvolvido por:

* Helena Ferreira
* João Luiz Sampaio

Como atividade prática do Módulo 1 de Data Warehouse, Modelagem de Dados e SQL.
