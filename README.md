## Desafio de Projeto: Modelagem de Dados em Estrela no Power BI com DAX

Este projeto demonstra a criação de um modelo de dados em estrela para um conjunto de dados de vendas, utilizando o Power BI e a linguagem DAX. O objetivo é transformar uma tabela única em um modelo dimensional, otimizado para análises eficientes e intuitivas.

Este é mais um desafio Power BI proposto pela [DIO](https://www.linkedin.com/school/dio-makethechange/) em parceria com a [NTT DATA](https://www.nttdata.com/global/en/), 

**Fonte de Dados:**

O conjunto de dados utilizado é o "Financial Sample" disponível no Power BI Desktop. A tabela original (Financial_origem) contém informações sobre vendas, produtos, descontos, segmentos de mercado e países.

**Modelo de Dados em Estrela:**

O modelo em estrela é composto por uma tabela fato (**F_Vendas**) e seis tabelas de dimensão:

**Dimensão:**
* **D_Produtos:**  Contém informações detalhadas sobre cada produto, como nome, preço de venda e custo de fabricação,  além de métricas agregadas calculadas a partir da tabela fato (média de unidades vendidas, médias e mediana do valor de vendas, valor máximo e mínimo de venda).
* **D_Produtos_Detalhes:** Complementa a tabela D_Produtos, armazenando informações adicionais como faixa de desconto e quantidade de unidades vendidas para cada produto.
* **D_Categoria:** Representa os segmentos de mercado e países, combinados para formar categorias únicas.
* **D_Descontos:** Armazena informações sobre as faixas de desconto e seus respectivos valores.
* **D_Calendario:**  Tabela de calendário criada com a função DAX `CALENDAR()`, contendo informações sobre datas, meses e anos.
* **D_Vendas:**  Tabela auxiliar criada para armazenar a chave artificial (SK_ID) e outras informações relevantes para cada venda.

**Fato:**
* **F_Vendas:**  Contém informações sobre cada venda, incluindo a chave estrangeira que referencia as tabelas de dimensão (ID_Produto, ID_Categoria, ID_Data, ID_Descontos), além de métricas como unidades vendidas, preço de venda, vendas brutas, descontos, vendas líquidas, custo das mercadorias vendidas e lucro.

**Relacionamentos:**

* A tabela F_Vendas se conecta com as tabelas de dimensão através de chaves estrangeiras. 
* D_Produtos_Detalhes está conectada a D_Produtos através do ID_Produto.

**Etapas de Modelagem:**

1. **Criação das Tabelas Dimensão:**
    * As tabelas de dimensão foram criadas a partir da tabela original "Financial_origem", selecionando e renomeando as colunas relevantes.
    * Foi utilizada a funcionalidade "Duplicar" para criar cópias da tabela original e evitar modificações na fonte de dados.
    * Para gerar IDs únicos nas tabelas D_Produtos e D_Categoria, foram utilizadas colunas condicionais, combinando as informações de outras colunas.
    * A tabela D_Calendario foi criada usando a função DAX `CALENDAR()`.
2. **Criação da Tabela Fato:**
    * A tabela F_Vendas foi criada selecionando as colunas relevantes da tabela original, incluindo as chaves estrangeiras para conectar com as tabelas de dimensão.
3. **Criação dos Relacionamentos:**
    * Na aba "Modelagem", foram criados os relacionamentos entre a tabela F_Vendas e as tabelas de dimensão, utilizando as chaves correspondentes.
    * Os relacionamentos existentes entre as tabelas "Detalhes" e as demais tabelas foram removidos para adequar a modelagem ao star schema.
    * Foi utilizado o recurso "Assumir Relacionamento" do Power BI para detectar e criar automaticamente alguns relacionamentos.

**Funcionalidades e Funções DAX:**

* **`CALENDAR()`**: Função DAX para criar a tabela de calendário.
* **Colunas Condicionais:**  Utilizadas para gerar IDs únicos nas tabelas D_Produtos e D_Categoria, combinando informações de outras colunas.
* **`RELATED()`:** Função DAX para trazer colunas de tabelas relacionadas, utilizando os relacionamentos criados no modelo.

**Considerações:**

* O modelo em estrela facilita a análise dos dados de vendas, permitindo explorar diferentes dimensões e métricas de forma rápida e eficiente.
* A escolha de manter a tabela D_Produtos_Detalhes separada da tabela D_Produtos cria uma estrutura "Snowflake", que pode ser útil para armazenar informações adicionais sobre os produtos.
* O modelo pode ser expandido no futuro, adicionando novas tabelas de dimensão e métricas para atender a novas necessidades de análise.

**Conclusão:**

Este projeto demonstra a importância da modelagem de dados para análises eficientes no Power BI. Através da criação de um modelo em estrela, os dados de vendas se tornam mais organizados, intuitivos e fáceis de analisar. A linguagem DAX e as funcionalidades do Power BI Desktop são ferramentas poderosas para transformar dados brutos em informações valiosas para a tomada de decisão.