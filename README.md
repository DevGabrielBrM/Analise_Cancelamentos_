# Análise de Dados de Cancelamento de Clientes

Este projeto foi realizado durante uma aula gratuita da **Jornada Python** e tem como objetivo analisar os dados de cancelamento de clientes de uma empresa com mais de 800 mil usuários. O intuito é entender os principais motivos pelos quais os clientes cancelam seus serviços e propor ações que possam ajudar a reduzir essa taxa de cancelamento.

## Objetivo do Projeto

A empresa identificou que a maioria de sua base de clientes está inativa, ou seja, cancelou o serviço. Para melhorar os resultados, a empresa deseja:
- Compreender os principais motivos para os cancelamentos.
- Identificar ações eficazes para reduzir o número de cancelamentos.

## Conjunto de Dados

Os dados utilizados neste projeto estão disponíveis no seguinte link: [Base de Dados de Cancelamento](https://drive.google.com/drive/folders/1uDesZePdkhiraJmiyeZ-w5tfc8XsNYFZ?usp=drive_link).

O arquivo `cancelamentos.csv` contém as seguintes colunas:

- `CustomerID`: Identificador único do cliente
- `idade`: Idade do cliente
- `sexo`: Sexo do cliente
- `tempo_como_cliente`: Tempo que o cliente está com a empresa (em meses)
- `frequencia_uso`: Frequência de uso do serviço
- `ligacoes_callcenter`: Número de ligações feitas ao call center
- `dias_atraso`: Dias em atraso com pagamentos
- `assinatura`: Tipo de plano do cliente
- `duracao_contrato`: Duração do contrato (Mensal, Anual, etc.)
- `total_gasto`: Total gasto pelo cliente
- `meses_ultima_interacao`: Meses desde a última interação com o cliente
- `cancelou`: Indicador de cancelamento (1 para cancelado, 0 para ativo)

### Observações sobre o Código e o Banco de Dados

O código está fornecido no formato `.py`, mas é recomendável executá-lo no formato `.ipynb` (Jupyter Notebook) para uma melhor visualização e interatividade. O arquivo `.ipynb` não está incluído no repositório, pois gera um arquivo com mais de 25 MB.

O banco de dados CSV também foi reduzido para atender ao limite de 25 MB, mas ainda contém informações relevantes para a análise.
* função display() é executada só no .ipynb

## Passo a Passo da Análise

### 1. Importar a Base de Dados
```python
import pandas as pd

tabela = pd.read_csv('cancelamentos.csv')
```

## Visualizar a Base de Dados
- Analisar as informações contidas na base e identificar colunas desnecessárias.
- Remover a coluna CustomerID.
  ```python
  tabela = tabela.drop(columns='CustomerID')
  display(tabela)
  ```

## Tratamento de Dados
- Corrigir dados em formatos errados e lidar com valores ausentes.
- Neste projeto, as linhas com valores vazios foram removidas
  ```python
  tabela = tabela.dropna()
  display(tabela.info())
  ```
## Análise Inicial dos Cancelamentos
- Contar o número de cancelamentos e clientes ativos.
- Calcular o percentual de cancelamentos.
  ```python
  display(tabela['cancelou'].value_counts(normalize=True).map('{:.2%}'.format))
  ```

## Análise de Causas do Cancelamento
- Criar gráficos para analisar a relação entre variáveis e o cancelamento.
  ```python
  import plotly.express as px
  
  for coluna in tabela.columns:
      grafico = px.histogram(tabela, x=coluna, color='cancelou')
      grafico.show()
  ```
## Filtragem dos Dados
- Filtrar dados para entender o impacto das ligações ao call center, atrasos e tipos de contrato nos cancelamentos.
  ```
  filtro = tabela['ligacoes_callcenter'] <= 4
  tabela = tabela[filtro]
  filtro = tabela['dias_atraso'] <= 20
  tabela = tabela[filtro]
  filtro = tabela['duracao_contrato'] != 'Monthly'
  tabela = tabela[filtro]
  ```

## Resultados Esperados
A partir da análise, espera-se identificar:

- Padrões que levam ao cancelamento de clientes.
- Recomendações para melhorar a retenção de clientes, como melhorias no atendimento ao cliente e ajustes nas ofertas de contrato.

## Contribuições
Contribuições são bem-vindas! Sinta-se à vontade para abrir uma issue ou enviar um pull request.

## Licença
Este projeto é para fins educacionais e não possui uma licença específica. Todos os direitos reservados à Jornada Python.
