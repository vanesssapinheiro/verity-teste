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
- **GitHub Actions**: Para automação da execução dos testes e geração de releases
- **Cucumber**: Para descrever os testes em BDD.
- **Confluence**: Para gerar a documentação.
- **Docker (*opcional*)**: Para executar os testes em um container Docker.

## Configuração do ambiente
```sh
# instalando dependencias do Node
npm install 

# baixar imagem do serverest 
docker pull paulogoncalvesbh/serverest:latest
```


### Executar os Testes Localmente

Para gerar os relatórios localmente, execute o seguinte comando:

```bash
npm run newman
# resultado vai ser gerado no console
npm run newman:reports
# devem ser gerados os arquivos ./reports/report.json e ./reports/report.html
```

Para executar os testes com Docker multiplas interações, execute o seguinte comando:

```bash
npm run newman:docker
# resultado vai ser gerado no console
npm run newman:docker:report
# devem ser gerados os arquivos ./reports/report.json e ./reports/report.html
```
Para executar os testes com Docker, execute o seguinte comando:

```bash
npm run newman:docker:multiple
# resultado vai ser executado no docker e gerado no console com 120 interações
npm run newman:docker:multiple:report
# resultado vai ser executado no docker e gerado no console com 120 interações e gerado arquivos ./reports/report.json e ./reports/report.html
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

# Testes implementados
Estão descritos na documentação armazenados em ./docs/Documentacao_Desafio.pdf

# Resultado dos Testes
Estão descritos na documentação armazenados em ./docs/Resultado_ Desafio .pdf

# Testes BDD
Estão descritos na documentação armazenados em ./cenarios/bdd.testcase


