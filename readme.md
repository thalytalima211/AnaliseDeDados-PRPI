# Análise de Dados PRPI
Repositório destinado à extração, ao tratamento e à análise dos dados relacionados aos projetos de pesquisa e pesquisadores da Pró-Reitoria de Pesquisa, Pós-Graduação e Inovação (PRPI) do IFCE, utilizando Python e Pandas.

## Tecnologias Utilizadas
- Python 3
- Pandas e NumPy para tratamento e análise de dados
- SQLAlchemy e o driver correspondente ao banco de dados PostgreSQL, para conexão com a base institucional
- Gspread e Google Auth para acesso às planilhas do Google Sheets
- Jupyter Notebook para execução interativa das análises

## Pré-Requisitos
Antes de executar a análise, é necessário ter:
- Python 3.10 ou superior, conforme a compatibilidade das dependências do projeto
- Git
- Acesso autorizado ao banco de dados da PRPI
- Acesso às planilhas do Google Sheets utilizadas na análise
- Credenciais de autenticação para o Google Sheets

## Como executar

### 1. Clonar o repositório
```git
git clone git@github.com:thalytalima211/AnaliseDeDados-PRPI.git
cd AnaliseDeDados-PRPI
```

### 2. Configurar ambiente Pyhton
Recomenda-se criar um ambiente virtual para isolar as dependências do projeto.

#### Windows
```
python -m venv .venv
.venv\Scripts\activate
```

#### Linux ou MacOS
```
python3 -m venv .venv
source .venv/bin/activate
```

Em seguida, instale a dependências do projeto:
```
pip install -r requirements.txt
```

### 3. Configurar as credenciais do Google Sheets
O acesso às planilhas é realizado por meio da API do Google Sheets, utilizando uma conta de serviço do Google Cloud. Para configurar o acesso, siga os seguintes passos:

#### Criar e configurar a conta de serviço
1. Acesse o [Google Cloud Console](https://console.cloud.google.com).
2. Crie ou selecione um projeto.
3. Ative a [API do Google Sheets](https://console.cloud.google.com/apis/library/sheets.googleapis.com).
4. Crie uma [conta de serviço](https://console.cloud.google.com/iam-admin/serviceaccounts).
5. Abra a conta criada, entre na aba Chaves (Keys), clique em Adicionar chave → Criar nova chave → JSON.
6. Baixe o arquivo de credenciais.
7. Renomeie o arquivo baixado para `credenciais.json`
8. Adicione o arquivo à raiz do projeto

#### Conceder acesso às planilhas
Copie o endereço de e-mail da conta de serviço, identificado pelo campo `client_email` do JSON.

Em cada planilha privada necessária à análise:
- Clique em Compartilhar.
- Adicione o e-mail da conta de serviço.
- Conceda a permissão de leitura.

A conta de serviço precisa ter acesso a todas as planilhas utilizadas. A criação das credenciais, por si só, não concede acesso automático a elas.

### 4. Configure as variáveis de ambiente
O projeto utiliza variáveis de ambiente para armazenar os parâmetros de acesso ao banco de dados e identificar as planilhas utilizadas na análise.

| Variável | Finalidade |
| -------- | ---------- |
| PRPI_DATABASE_URL |URL de conexão com o banco de dados da PRPI, conforme o formato `postgresql+psycopg://USUARIO:SENHA@HOST:PORTA/NOME_DO_BANCO`. |
| PRPI_PLANILHA_NL_ID | Identificador da planilha do Google Sheets que contém os dados da plataforma NL. |
|PRPI_PLANILHA_PESQUISADORES_NL_ID |Identificador da planilha do Google Sheets que contém os dados de pesquisadores da plataforma NL. |

O identificador de uma planilha pode ser obtido a partir de sua URL. Em um endereço no formato `https://docs.google.com/spreadsheets/d/ID_DA_PLANILHA/edit`, ele corresponde ao trecho entre /d/ e /edit.

Para definir as variáveis de ambiente, crie o arquivo `.env` na raiz do projeto e insira as variáveis, substituindo pelos respectivos acessos:
```env
PRPI_DATABASE_URL="URL_DE_CONEXAO_DO_BANCO"
PRPI_PLANILHA_NL_ID="ID_DA_PLANILHA_NL"
PRPI_PLANILHA_PESQUISADORES_NL_ID="ID_DA_PLANILHA_PESQUISADORES"
```

### 5. Executar a análise
Após configurar o ambiente, as credenciais e as variáveis de ambiente:
1. Abra o projeto no VS Code ou em outra IDE de sua preferência.
2. Ative o ambiente virtual.
3. Inicie o Jupyter Notebook.
4. Abra o notebook principal de análise.
5. Execute as células na ordem apresentada, verificando a conexão com as fontes de dados e a execução das etapas de tratamento.