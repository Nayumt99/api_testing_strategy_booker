# 🎯 Estratégia de Testes: API Restful-Booker

Este documento detalha a abordagem estratégica para a automação de testes da API **Restful-Booker**, focando em garantir a integridade do contrato e das regras de negócio do sistema de reservas.

---

## 1. Escopo e Objetivos
* **Objetivo Principal**: Validar o ciclo de vida completo de uma reserva (CRUD) e as regras de negócio associadas.
* **Nível de Teste**: Testes de API (Integração e Contrato).
* **Ferramentas Utilizadas**: 
    * **Postman**: Desenvolvimento de coleções e scripts de pré-requisito/teste.
    * **Newman**: Executor de linha de comando (CLI) para automação e CI/CD.
    * **htmlextra**: Reporter para geração de evidências detalhadas em HTML.

---

## 2. Arquitetura da Automação
A arquitetura foi projetada para ser modular e independente de dados fixos (hardcoded):

*   **Desacoplamento de Ambiente**: Uso de arquivos de ambiente (`.json`) para separar variáveis como `base_url`.
*   **Persistência Dinâmica de Dados**: Implementação de scripts em JavaScript (Post-response) para capturar o `bookingid` no `POST` e injetá-lo automaticamente no `GET` e demais métodos.
*   **Hierarquia de Execução**: As requisições são organizadas logicamente para garantir que a criação ocorra antes da consulta/atualização.

---

## 3. Plano de Testes (Cenários)

### 3.1 Caminho Feliz (Happy Path)
| Cenário | Método | Descrição |
| :--- | :--- | :--- |
| Criar Reserva | `POST` | Valida a criação de uma reserva com payload válido e status 200/201. |
| Consultar Reserva | `GET` | Valida se a reserva criada anteriormente é retornada corretamente usando o ID dinâmico. |
| Autenticação | `POST` | Gera o token de acesso necessário para operações de escrita (PUT/DELETE). |

### 3.2 Testes de Negócio (Negativos)
*   **Busca Inexistente**: Validar retorno `404 Not Found` ao consultar um ID que não existe.
*   **Autenticação Inválida**: Garantir que alterações sem token válido retornem `403 Forbidden`.
*   **Payload Inválido**: Enviar dados malformados para validar o tratamento de erro da API.

---

## 4. Critérios de Aceite
* **Status Code**: Cada endpoint deve retornar o código HTTP definido no contrato da API.
* **Tempo de Resposta**: O tempo de latência não deve ultrapassar **800ms** em condições normais.
* **Integridade do JSON**: O corpo da resposta deve conter as propriedades obrigatórias (ex: `firstname`, `lastname`, `bookingid`).

---

## 5. Execução e Relatórios
A execução é padronizada via terminal para permitir integração futura com pipelines de **CI/CD (GitHub Actions)**:
```bash
newman run "collections/restful_booker_strategy.json" \
  -e "environments/restful_booker_prod.json" \
  -r htmlextra \
  --reporter-htmlextra-export docs/evidence/report.html