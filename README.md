
# 🧱 Arquitetura do Projeto — Camisetas Incendiários

Este projeto é uma aplicação web simples e interativa para gerenciamento de camisetas do grupo **Incendiários**, permitindo cadastro e edição de dados com integração à AWS.

---

## 🔧 Tecnologias Utilizadas

- **Frontend (HTML/CSS/JS)**: páginas web estáticas simples.
- **AWS Amplify Hosting**: para hospedar as páginas HTML de forma rápida.
- **API Gateway (API REST)**: responsável por receber requisições HTTP e repassá-las para uma função Lambda.
- **AWS Lambda (Python)**: backend sem servidor que lida com lógica de cadastro, edição e validação de dados.
- **DynamoDB**: banco de dados NoSQL que armazena os dados dos jogadores.

---

## 📁 Estrutura de Arquivos

| Arquivo              | Função                                                                 |
|----------------------|------------------------------------------------------------------------|
| `index.html`         | Página inicial que pergunta se o usuário já tem número e camiseta.     |
| `home.html`          | Formulário de **cadastro** de novo jogador.                            |
| `editar.html`        | Formulário de **edição** dos dados de um jogador já cadastrado.        |
| `style.css`          | Arquivo de estilos CSS (opcional).                                     |
| `lambda_function.py` | Função Lambda escrita em Python que trata GET e POST na API.           |

---

## 🔁 Fluxo de Funcionamento

### 1. **Página inicial** (`index.html`)
- Usuário responde à pergunta:
  - **Sim** → Redirecionado para `editar.html`
  - **Não** → Redirecionado para `home.html`

### 2. **Cadastro** (`home.html`)
- A API (`GET`) consulta todos os números já usados.
- O frontend mostra apenas os números disponíveis.
- Após preenchimento, envia um `POST` com os dados para a API.

### 3. **Edição** (`editar.html`)
- O usuário escolhe seu número (que já está em uso).
- Os dados são carregados automaticamente nos campos.
- Usuário edita **apenas nome da camiseta e tamanho**.
- Envio via `POST` atualiza o registro no DynamoDB, desde que o nome coincida.

### 4. **API Gateway + Lambda**
- A API possui dois métodos:
  - `GET`: retorna todos os jogadores cadastrados.
  - `POST`: cadastra ou atualiza um jogador (se o número estiver livre ou o nome for igual ao cadastrado).
- A Lambda faz a verificação de número já utilizado e valida o nome.

### 5. **Banco de Dados** — DynamoDB
- Tabela: `incendiariosvolei`
- Armazena: `nome`, `nome_camiseta`, `tamanho`, `numero`
- Estrutura flexível (NoSQL) e rápida para buscas por atributos.

---

## 🔒 Segurança e Restrições

- Os campos `nome` e `numero` **não são editáveis** na tela de edição.
- A função Lambda garante que:
  - Um número não pode ser usado por outra pessoa.
  - Atualização só é permitida se o nome coincidir com o já cadastrado.

---

## 📱 Responsividade

- Todos os arquivos HTML possuem estilos e media queries para telas pequenas.
- Campos e botões são adaptados para melhor usabilidade em celulares.

---

## 🚀 Como Publicar

1. Subir os arquivos HTML, CSS e imagens para o **AWS Amplify Hosting**.
2. Garantir que a API está configurada no **API Gateway** com endpoint público.
3. Verificar permissões da Lambda para acessar o DynamoDB.
4. Testar as páginas em desktop e mobile.

--
