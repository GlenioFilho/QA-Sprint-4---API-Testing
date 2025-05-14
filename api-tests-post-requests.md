# Testes de API – Requisições POST

**Sprint:** 4  
**Projeto:** Urban Routes – API Testing  
**Endpoint testado:** `POST /api/v1/kits/:id/products`  
**Ambiente:** Postman (Chrome 800x600)

---

## 📋 Casos de Teste – Validação de ID e Corpo da Requisição

| ID | Título do Caso de Teste | Etapas | Corpo da Solicitação | Esperado | Real | Status | Bug |
|----|--------------------------|--------|------------------------|----------|------|--------|-----|
| 1 | Criar um kit | Enviar solicitação POST | `id: 7 + productsList válido` | 200 OK | 200 OK | Aprovado | — |
| 2 | Atualizar quantidade de produto | Enviar POST com `id=7` | `productsList com quantidade atualizada` | 200 OK | 200 OK | Aprovado | — |
| 3 | ID como string | Enviar POST com `id="abc"` | 400 BAD REQUEST | 500 INTERNAL | Reprovado | [KAN-37](https://gleniofilhoo.atlassian.net/browse/KAN-37) |
| 4 | ID vazio | Enviar POST com `id=` | 400 BAD REQUEST | 500 INTERNAL | Reprovado | [KAN-38](https://gleniofilhoo.atlassian.net/browse/KAN-38) |
| 5 | `productsList` vazio | Enviar POST com lista vazia | 400 BAD REQUEST | 500 INTERNAL | Reprovado | [KAN-39](https://gleniofilhoo.atlassian.net/browse/KAN-39) |
| 6 | Produto com ID inexistente | Produto inválido na lista | 400 BAD REQUEST | 500 INTERNAL | Reprovado | [KAN-40](https://gleniofilhoo.atlassian.net/browse/KAN-40) |
| 7 | ID deletado | `id` foi previamente removido | 400 BAD REQUEST | 200 OK | Reprovado | [KAN-41](https://gleniofilhoo.atlassian.net/browse/KAN-41) |
| 8 | ID nulo | `id: null` | 400 BAD REQUEST | 200 OK | Reprovado | [KAN-42](https://gleniofilhoo.atlassian.net/browse/KAN-42) |
| 9 | ID negativo | `id: -1` | 400 BAD REQUEST | 200 OK | Reprovado | [KAN-43](https://gleniofilhoo.atlassian.net/browse/KAN-43) |
| 10 | ID com string longa | `id: muito longo` | 400 BAD REQUEST | 500 INTERNAL | Reprovado | [KAN-44](https://gleniofilhoo.atlassian.net/browse/KAN-44) |
| 11 | ID duplicado | Mesmo ID usado 2x | 400 BAD REQUEST | 500 INTERNAL | Reprovado | [KAN-45](https://gleniofilhoo.atlassian.net/browse/KAN-45) |
| 12 | `productsList` ausente | Nenhum campo enviado | 400 BAD REQUEST | 200 OK | Reprovado | [KAN-46](https://gleniofilhoo.atlassian.net/browse/KAN-46) |
| 13 | `productsList` com 30 itens | Lista cheia e válida | 200 OK | 200 OK | Aprovado | — |
| 14 | `productsList` com 31 itens | Lista ultrapassa limite | 400 BAD REQUEST | 400 BAD REQUEST | Aprovado | — |
| 15 | Campo duplicado | Campos repetidos no JSON | 400 BAD REQUEST | 200 OK | Reprovado | [KAN-47](https://gleniofilhoo.atlassian.net/browse/KAN-47) |

---

## 🧪 Casos de Teste – ID com Formatos Inválidos

| ID | Caso de Teste | Entrada | Esperado | Real | Status | Bug |
|----|----------------|---------|----------|------|--------|-----|
| 24 | ID como número negativo | `-10` | 400 BAD | 200 OK | Reprovado | [KAN-48](https://gleniofilhoo.atlassian.net/browse/KAN-48) |
| 25 | ID com letras | `"abc"` | 400 BAD | 500 INTERNAL | Reprovado | [KAN-49](https://gleniofilhoo.atlassian.net/browse/KAN-49) |
| 26 | ID com alfanumérico | `"7a"` | 400 BAD | 500 INTERNAL | Reprovado | [KAN-50](https://gleniofilhoo.atlassian.net/browse/KAN-50) |
| 27 | ID com caractere especial | `"@!#"` | 400 BAD | 500 INTERNAL | Reprovado | [KAN-51](https://gleniofilhoo.atlassian.net/browse/KAN-51) |
| 28 | ID como nulo | `null` | 400 BAD | 200 OK | Reprovado | [KAN-52](https://gleniofilhoo.atlassian.net/browse/KAN-52) |

---

## 📦 Casos de Teste – Validação de Valores de Produto

| ID | Descrição | Entrada | Esperado | Real | Status | Bug |
|----|-----------|---------|----------|------|--------|-----|
| 29 | Campo "peso" inválido | peso: -1 | 400 BAD | 200 OK | Reprovado | [KAN-53](https://gleniofilhoo.atlassian.net/browse/KAN-53) |
| 30 | Campo "peso" válido | peso: 0.5 | 200 OK | 200 OK | Aprovado | — |
| 31 | Campo "nome" ausente | sem nome | 400 BAD | 500 INTERNAL | Reprovado | [KAN-54](https://gleniofilhoo.atlassian.net/browse/KAN-54) |
| 32 | Campo "quantidade" = 0 | quantidade: 0 | 400 BAD | 200 OK | Reprovado | [KAN-55](https://gleniofilhoo.atlassian.net/browse/KAN-55) |

---

## 📌 Observações Finais

- Vários testes retornaram `500 INTERNAL SERVER ERROR` onde o correto seria `400 BAD REQUEST`.
- Foram aplicadas técnicas de **partição de equivalência** e **valores de borda**.
- Todos os bugs foram documentados no Jira.

🔗 [Acessar relatórios de bug no Jira](https://gleniofilhoo.atlassian.net)

---

🧪 Criado por Glenio Filho – Sprint 4 – Urban Routes API Testing
