# Projeto: Análise de Dados - Coleta de Dados I

Este projeto faz parte do módulo "Análise de Dados: Coleta de Dados I" do curso da EBAC. O objetivo deste exercício é aprender a coletar e manipular dados de diferentes fontes (como arquivos Excel, CSV e Texto) utilizando a linguagem Python.

## Descrição do Projeto

O projeto utiliza um conjunto de dados referente a informações financeiras de clientes, especificamente sobre seu comportamento em relação a pagamentos de dívidas (adimplentes ou inadimplentes). O arquivo de dados original é um arquivo Excel, contendo informações como idade, salário anual, estado civil, entre outros atributos.

O exercício aborda as seguintes etapas:

1. **Preparação do Ambiente**:
   - Utilizar o pacote `requests` para baixar o arquivo Excel contendo os dados de crédito.

2. **Manipulação de Dados com Python**:
   - Utilização das bibliotecas `openpyxl` para ler dados de arquivos Excel e `pandas` para manipulação de dados.
   - Extração das colunas relevantes para clientes inadimplentes e solteiros.
   - Salvar os dados extraídos no formato CSV, com separação por ponto e vírgula.

## Tópicos Abordados

- **Arquivos CSV**
- **Arquivos Texto**
- **Arquivos Excel**

## Passos do Projeto

### 1. Preparação do Ambiente

Primeiro, você precisa configurar seu ambiente de trabalho, instalando as bibliotecas necessárias:

```bash
pip install requests
pip install openpyxl
pip install pandas
```

Depois, baixe o arquivo de dados `credito.xlsx` utilizando o código abaixo:

```python
import requests

url = 'https://raw.githubusercontent.com/andre-marcos-perez/ebac-course-utils/main/dataset/credito.xlsx'
response = requests.get(url)

# Escreve o conteúdo baixado em um arquivo
with open('banco.xlsx', 'wb') as file:
    file.write(response.content)

print('Download completo.')
```

### 2. Extração de Dados com openpyxl e pandas

Agora, com o arquivo baixado, vamos usar o `openpyxl` para carregar o arquivo Excel e o `pandas` para manipulação dos dados.

```python
from openpyxl import load_workbook
import pandas as pd

# Carrega o arquivo Excel
planilhas = load_workbook(filename='credito.xlsx')
planilha = planilhas.active

# Carrega os dados na tabela
dados = pd.DataFrame(planilha.values)

# Filtra os clientes inadimplentes (default = 1) e solteiros (estado_civil = 'solteiro')
clientes_inadimplentes = dados[(dados['default'] == 1) & (dados['estado_civil'] == 'solteiro')]

# Seleciona apenas as colunas id, sexo e idade
dados_extraidos = clientes_inadimplentes[['id', 'sexo', 'idade']]

# Salva os dados extraídos em um arquivo CSV
dados_extraidos.to_csv('credito.csv', sep=';', index=False)
```

### 3. Salvar os Dados em Formato CSV

O código acima filtra os dados de clientes inadimplentes e solteiros e salva as colunas `id`, `sexo` e `idade` em um arquivo CSV chamado `credito.csv`.

### 4. Resultado Esperado

O arquivo CSV gerado terá a seguinte estrutura de exemplo:

```csv
id;sexo;idade
1;M;34
2;F;28
3;M;41
```

## Conclusão

Neste exercício, aprendemos a trabalhar com arquivos Excel e CSV em Python utilizando as bibliotecas `openpyxl` e `pandas`, além de realizar filtragem e extração de dados específicos para análise.

## Requisitos

- Python 3.x
- Bibliotecas: `requests`, `openpyxl`, `pandas`

## Contato

Se você tiver dúvidas ou sugestões, entre em contato com o professor André Perez ou com o aluno Jailson Carvalho.

