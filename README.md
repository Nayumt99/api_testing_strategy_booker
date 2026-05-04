# 🚀 API Automation Framework | Restful-Booker

Este projeto apresenta um framework de automação de testes para a API **Restful-Booker**, desenvolvido para validar fluxos de reserva de hotel. Como Arquiteto de Testes, foquei em criar uma estrutura escalável, utilizando variáveis de ambiente e relatórios dinâmicos.

## 🛠️ Tecnologias Utilizadas

*   **Runtime**: Node.js
*   **Engine de Testes**: Postman & Newman
*   **Relatórios**: Newman-Reporter-HtmlExtra
*   **Documentação**: Markdown

## 📋 Pré-requisitos

Antes de começar, você precisará ter instalado em sua máquina:
*   [Node.js](https://nodejs.org/en/) (Versão 18 ou superior)
*   [VS Code](https://code.visualstudio.com/) (ou sua IDE de preferência)

## 🚀 Instalação e Configuração

1.  **Clone o repositório:**
    ```bash
    git clone [https://github.com/seu-usuario/seu-repositorio.git](https://github.com/seu-usuario/seu-repositorio.git)
    cd seu-repositorio
    ```

2.  **Instale as dependências globais do Newman:**
    ```bash
    npm install -g newman
    npm install -g newman-reporter-htmlextra
    ```

## 🏃 Como Rodar os Testes

Para executar a suite de testes e gerar o relatório automaticamente, utilize o comando abaixo no terminal:

```bash
newman run "collections/restful_booker_strategy.json" \
  -e "environments/restful_booker_prod.json" \
  -r htmlextra \
  --reporter-htmlextra-export docs/evidence/report.html
````

![API Testing](https://github.com/Nayumt99/api_testing_strategy_booker/actions/workflows/main.yml/badge.svg)
