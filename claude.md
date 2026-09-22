# Projeto Morcegão Lanches — Instruções para Claude Code

## 1. Contexto do projeto

Este projeto é um sistema web de cardápio digital e criação de pedidos para o estabelecimento Morcegão Lanches.

O projeto é um MVP real, desenvolvido inicialmente para um único estabelecimento.

O objetivo é construir uma solução moderna, simples, organizada e adequada ao fluxo de atendimento definido no Documento Mestre.

O projeto não deve ser transformado em SaaS, sistema multiempresa ou plataforma genérica.

---

## 2. Fonte de verdade

O documento:

"Documento Mestre — Morcegão Lanches V1"

é a fonte de verdade do escopo funcional do projeto.

As decisões presentes nele devem ser respeitadas.

Não adicionar funcionalidades, alterar regras de negócio ou expandir o escopo por iniciativa própria.

Quando existir uma necessidade não definida no Documento Mestre, interromper a implementação dessa parte e solicitar uma decisão antes de prosseguir.

---

## 3. Regra principal de desenvolvimento

Implementar o projeto de forma incremental.

Não implementar várias funcionalidades de uma vez.

Cada etapa deve:

1. ter um objetivo claro;
2. alterar somente o necessário;
3. ser testável;
4. ser validada antes da próxima etapa.

Não criar funcionalidades "para o futuro" dentro da implementação atual.

---

## 4. Stack definida

### Frontend

- React
- TypeScript

### Backend

- Python
- FastAPI

### Banco de dados

- PostgreSQL

### Arquitetura

Frontend
→ REST API
→ FastAPI
→ PostgreSQL

Frontend e backend são responsabilidades separadas.

---

## 5. Estrutura conceitual

O projeto terá:

- frontend;
- backend;
- banco de dados;
- documentação.

A organização deve manter separação clara de responsabilidades.

Não misturar regras de negócio, acesso ao banco, rotas HTTP e componentes de interface sem necessidade.

---

## 6. Escopo V1

O MVP contempla:

- cardápio digital;
- categorias;
- busca de produtos;
- produtos;
- preços;
- promoções;
- disponibilidade de produtos;
- carrinho;
- checkout;
- criação de pedidos;
- retirada;
- delivery;
- atendimento na mesa;
- formas de pagamento;
- painel administrativo;
- gerenciamento de produtos;
- gerenciamento de categorias;
- gerenciamento de bairros e taxas;
- gerenciamento de pedidos;
- autenticação do proprietário;
- alteração de status dos pedidos;
- geração de link do WhatsApp com mensagem preenchida.

---

## 7. Funcionalidades que NÃO fazem parte da V1

Não implementar:

- login do cliente;
- cadastro público de clientes;
- gateway de pagamento;
- integração oficial com WhatsApp;
- automação de envio de WhatsApp;
- estoque;
- controle financeiro;
- programa de fidelidade;
- cupons;
- inteligência artificial;
- sistema multiempresa;
- integração com SuperCardápio;
- integração bancária;
- sistema complexo de funcionários;
- extras ou adicionais de produtos.

Esses itens não devem ser adicionados sem decisão explícita.

---

## 8. Produtos

Os produtos devem possuir, conforme definido no projeto:

- nome;
- descrição;
- imagem;
- preço;
- preço anterior, quando aplicável;
- categoria;
- ativo/inativo;
- disponível/indisponível.

A V1 não possui sistema de adicionais ou personalização de produtos.

---

## 9. Pedidos

Um pedido deve preservar os dados relevantes no momento da compra.

Os itens do pedido devem armazenar:

- produto;
- nome do produto no momento da compra;
- quantidade;
- preço unitário no momento da compra;
- subtotal.

Alterações futuras no preço do produto não devem alterar pedidos históricos.

---

## 10. Checkout

O checkout deve coletar:

- nome;
- telefone;
- tipo de atendimento;
- forma de pagamento.

### Retirada

Não exige endereço de entrega.

### Delivery

Deve permitir:

- seleção do bairro;
- rua;
- número;
- complemento;
- taxa de entrega correspondente.

### Atendimento na mesa

Deve permitir identificação da mesa conforme definido no projeto.

### Dinheiro

Quando pagamento em dinheiro for selecionado, solicitar o valor para o qual o cliente precisa de troco.

### Pix

Na V1 não existe gateway de pagamento.

---

## 11. Painel administrativo

O painel é destinado ao proprietário do estabelecimento.

O proprietário poderá:

- visualizar pedidos;
- aceitar pedidos;
- rejeitar pedidos;
- alterar status;
- gerenciar produtos;
- alterar preços;
- controlar promoções;
- controlar disponibilidade;
- gerenciar categorias;
- gerenciar bairros;
- alterar taxas de entrega.

Não criar sistema de múltiplos funcionários na V1.

---

## 12. Autenticação

O sistema possui autenticação para o proprietário.

Regras:

- acesso por email e senha;
- não existe cadastro público;
- não existe login do cliente;
- senha nunca deve ser armazenada em texto puro;
- operações administrativas devem ser protegidas no backend.

A segurança deve ser adequada ao MVP sem criar infraestrutura desnecessariamente complexa.

---

## 13. WhatsApp

A V1 não utiliza a API oficial do WhatsApp.

O sistema deverá gerar um link para abrir uma conversa no WhatsApp do cliente com uma mensagem previamente preenchida contendo os dados relevantes do pedido.

O proprietário será responsável por clicar em enviar.

Não implementar automação de envio.

---

## 14. API

A API será RESTful utilizando FastAPI.

Endpoints previstos incluem:

### Públicos

GET /categories

GET /products

GET /products?category_id={id}

GET /neighborhoods

POST /orders

### Administração

POST /auth/login

POST /products

PUT /products/{id}

PATCH /products/{id}/availability

POST /categories

PUT /categories/{id}

POST /neighborhoods

PUT /neighborhoods/{id}

GET /orders

GET /orders/{id}

PATCH /orders/{id}/status

Os endpoints podem ser ajustados tecnicamente quando necessário, mas não devem alterar as regras funcionais do MVP.

---

## 15. Validação

Validações importantes devem existir no backend.

Nunca confiar somente na validação do frontend.

Validar, conforme aplicável:

- campos obrigatórios;
- telefone;
- tipo de atendimento;
- endereço para delivery;
- bairro válido;
- forma de pagamento;
- produtos existentes;
- produtos disponíveis;
- quantidade;
- valores do pedido.

---

## 16. Banco de dados

As entidades definidas para a V1 são:

- users
- categories
- products
- neighborhoods
- customers
- orders
- order_items

Relacionamentos e campos devem seguir o Documento Mestre.

Não criar tabelas adicionais sem necessidade funcional ou decisão explícita.

---

## 17. Arquitetura e qualidade

Priorizar:

- separação de responsabilidades;
- código legível;
- baixo acoplamento;
- validação no backend;
- segurança básica adequada;
- tratamento correto de erros;
- nomes claros;
- organização profissional;
- facilidade de manutenção.

Evitar:

- abstrações desnecessárias;
- padrões complexos sem necessidade;
- dependências desnecessárias;
- funcionalidades especulativas;
- código duplicado;
- soluções excessivamente complexas para o tamanho do MVP.

---

## 18. Processo de implementação

O Claude Code deve implementar somente a tarefa solicitada.

Antes de executar uma mudança significativa:

- explicar o que será alterado;
- identificar arquivos envolvidos;
- apontar eventuais decisões técnicas necessárias.

Depois da implementação:

- informar quais arquivos foram criados ou alterados;
- explicar brevemente o que foi feito;
- informar como testar;
- informar eventuais problemas encontrados.

Não avançar automaticamente para a próxima funcionalidade.

---

## 19. Decisões

O Claude Code não deve tomar decisões de produto ou alterar o escopo por conta própria.

Quando houver conflito ou informação ausente:

1. identificar o problema;
2. explicar a decisão necessária;
3. aguardar definição.

Decisões arquiteturais importantes devem ser discutidas antes da implementação.

---

## 20. Regra contra escopo creep

Se uma ideia nova aparecer durante o desenvolvimento e não estiver definida no MVP:

NÃO implementar automaticamente.

Registrar como possível item futuro e aguardar decisão.

O objetivo é entregar o MVP definido, não construir funcionalidades adicionais.

---

## 21. Ambiente e configuração

Informações sensíveis nunca devem ser armazenadas diretamente no código.

Não colocar:

- senhas;
- tokens;
- chaves secretas;
- credenciais de banco;

em arquivos versionados.

Utilizar variáveis de ambiente e arquivos apropriados de configuração.

---

## 22. Git

As alterações devem ser pequenas e coerentes.

Evitar commits gigantes contendo várias funcionalidades independentes.

Cada conjunto de alterações deve representar uma mudança compreensível no projeto.

---

## 23. Papel do Claude Code

O Claude Code é responsável pela implementação técnica e pelo trabalho de código/versionamento.

Ele não é a autoridade sobre o escopo do produto.

As decisões do projeto devem seguir:

1. Documento Mestre aprovado;
2. decisões posteriores explicitamente aprovadas;
3. orientação técnica definida durante o desenvolvimento.

Quando houver dúvida, perguntar antes de implementar.

---

## 24. Objetivo final

Construir o MVP definido no Documento Mestre do Morcegão Lanches de forma:

- funcional;
- organizada;
- simples;
- sustentável;
- segura dentro do nível necessário ao projeto;
- fácil de testar;
- fácil de manter;
- sem funcionalidades fora do escopo.
