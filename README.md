# Teste para Vaga de QA

Este repositório contém um projeto para realização de testes de API utilizando Postman, Newman e GitHub Actions.

## Objetivo

- Utilizar o Postman e Newman para realizar testes na API [Serverest](https://serverest.dev) e obter 100% de cobertura de testes nos seguintes endpoints:
  - **[POST] /login**
  - **[GET] /usuarios**
  - **[GET] /usuarios/:id**
  - **[POST] /usuarios**
  - **[PUT] /usuarios/:id**
  - **[DELETE] /usuarios/:id**
- Gerar relatórios dos testes nos formatos **JSON** e **HTML**.
- Configurar um workflow no GitHub Actions para executar os testes automaticamente e gerar uma release contendo os relatórios.

## Ferramentas Utilizadas

- **Postman**: Para criar e executar os testes de API.
- **Newman**: Para execução dos testes em linha de comando.
- **GitHub Actions**: Para automação da execução dos testes e geração de releases.

### Executar os Testes Localmente

Para gerar os relatórios localmente, execute o seguinte comando:

```bash
npm run newman:reports
```

Devem ser gerados dois arquivos na pasta `reports/`:

- `report.json`
- `report.html`

### Executar o Workflow

1. Toda alteração na branch `main` do repositório.
2. O workflow será acionado automaticamente, executando os testes e gerando os relatórios.
3. A release será criada com os relatórios anexados, a versão da release será utilizada do `package.json`.

## Resultados Esperados

- 100% de cobertura de testes nos endpoints especificados.
- Relatórios detalhados dos testes em formatos **JSON** e **HTML**.
- Pipeline automatizada com GitHub Actions para execução dos testes e criação de releases.



# ServeRest API Documentação

ServeRest é uma API REST gratuita que simula uma loja virtual, projetada para fins de aprendizado e testes de API.

URL Base: `https://serverest.dev`


## 1. Login

### a) Login
- **Descrição:** Endpoint para logar e obter um token de autenticação.
- **Método:** POST
- **URL:** `/login`
- **Headers:**
  - `Content-Type`: `application/json`
  - `Accept`: `application/json`
- **Corpo da Requisição:**
```json
{
  "email": "{{currentEmail}}",
  "password": "{{currentPassword}}"
}
```
- **Responses:**
  - **200 OK:**
    ```json
    {
      "message": "Login realizado com sucesso",
      "authorization": "Bearer <token>"
    }
    ```
  - **401 Unauthorized:**
    - Invalid email or password:
      ```json
      {
        "message": "Email e/ou senha inválidos"
      }
      ```
  - **400 Bad Request:**
    - Campos obrigatórios:
      ```json
      {
        "email": "email é obrigatório",
        "password": "password é obrigatório"
      }
      ```

---

## 2. Usuarios

### a) Registrar Usuário
- **Descrição:** Endpoint para registrar um novo usuário.
- **Método:** POST
- **URL:** `/usuarios`
- **Headers:**
  - `Content-Type`: `application/json`
  - `Accept`: `application/json`
- **Corpo da Requisição:**
```json
{
  "nome": "{{currentName}}",
  "email": "{{currentEmail}}",
  "password": "{{currentPassword}}",
  "administrador": "{{currentAdministrador}}"
}
```
- **Responses:**
  - **201 Created:**
    ```json
    {
      "message": "Cadastro realizado com sucesso",
      "_id": "<generated_id>"
    }
    ```
  - **400 Bad Request:**
    - Email already in use:
      ```json
      {
        "message": "Este email já está sendo usado"
      }
      ```
    - Campos obrigatórios:
      ```json
      {
        "nome": "nome é obrigatório",
        "email": "email é obrigatório",
        "password": "password é obrigatório",
        "administrador": "administrador é obrigatório"
      }
      ```

### b) Lista de Usuarios
- **Descrição:** Endpoint para listar todos os usuários registrados.
- **Método:** GET
- **URL:** `/usuarios`
- **Headers:**
  - `Authorization`: `Bearer {{currentBearerToken}}`
  - `Accept`: `application/json`
- **Query Parameters (optional):**
  - `_id`: Filter by ID
  - `nome`: Filter by name
  - `email`: Filter by email
  - `administrador`: Filter by admin status (`true`/`false`)
- **Responses:**
  - **200 OK:**
    ```json
    {
      "quantidade": 1,
      "usuarios": [
        {
          "nome": "Example Name",
          "email": "example@email.com",
          "password": "123456",
          "administrador": "true",
          "_id": "<generated_id>"
        }
      ]
    }
    ```
  - **400 Bad Request:**
    - Campos inválidos:
      ```json
      {
        "email": "email deve ser um email válido",
        "administrador": "administrador deve ser 'true' ou 'false'"
      }
      ```

### c) Busca de Usuário por ID
- **Descrição:** Endpoint para obter os detalhes de um usuário por ID.
- **Método:** GET
- **URL:** `/usuarios/:_id`
- **Headers:**
  - `Authorization`: `Bearer {{currentBearerToken}}`
  - `Accept`: `application/json`
- **Responses:**
  - **200 OK:**
    ```json
    {
      "nome": "Example Name",
      "email": "example@email.com",
      "password": "123456",
      "administrador": "true",
      "_id": "<generated_id>"
    }
    ```
  - **400 Bad Request:**
    - Usuario não encontrado:
      ```json
      {
        "message": "Usuário não encontrado"
      }
      ```

### d) Editação de Usuário
- **Descrição:** Endpoint para atualizar o usuário por ID.
- **Método:** PUT
- **URL:** `/usuarios/:_id`
- **Headers:**
  - `Authorization`: `Bearer {{currentBearerToken}}`
  - `Content-Type`: `application/json`
  - `Accept`: `application/json`
- **Request Body:**
```json
{
  "nome": "{{currentName}}",
  "email": "{{currentEmail}}",
  "password": "{{currentPassword}}",
  "administrador": "{{currentAdministrador}}"
}
```
- **Responses:**
  - **200 OK:**
    ```json
    {
      "message": "Registro alterado com sucesso"
    }
    ```
  - **400 Bad Request:**
    - Campos obrigatórios:
      ```json
      {
        "nome": "nome é obrigatório",
        "email": "email é obrigatório",
        "password": "password é obrigatório",
        "administrador": "administrador é obrigatório"
      }
      ```

### e) Deletar Usuário por ID
- **Description:** Endpoint para excluir o usuário por ID.
- **Method:** DELETE
- **URL:** `/usuarios/:_id`
- **Headers:**
  - `Authorization`: `Bearer {{currentBearerToken}}`
  - `Accept`: `application/json`
- **Responses:**
  - **200 OK:**
    ```json
    {
      "message": "Registro excluído com sucesso"
    }
    ```
  - **400 Bad Request:**
    - Usuario não encontrado:
      ```json
      {
        "message": "Nenhum registro excluído"
      }
      ```

---

## Notes
- **Autenticação:** Alguns endpoints requerem autenticação.
