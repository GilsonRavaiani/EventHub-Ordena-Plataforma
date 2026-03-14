# 🌐 LAB AZ-204 — Projeto Completo: "EventHub Ordena Plataforma"


## 🎯 Objetivo do projeto

### Criar uma solução moderna no Azure que:

* Recebe pedidos via API (Azure App Service)

* Processa eventos (Grade de Eventos + Funções)

* Armazena dados (Cosmos DB + Blob Storage)

* Expõe APIs gerenciadas (API Management)

* Contêineres dos EUA (ACR + Apps de Contêineres)

* Implementa segurança (Managed Identity + Key Vault)

* Monitora tudo (Application Insights)

## 🧩 Módulo 1 — Criar e publicar uma imagem de contêiner

### Habilidades treinadas:

* Criar e gerenciar imagens

* Publicar no Azure Container Registry

* Executar no Azure Container Apps

### 🔧 Passos:

1. Crie um app simples em Node.js ou .NET que expõe /health e /orders.

2. Crie hum Dockerfile.

3. Crie um ACR:

Bash: 

az acr create -n meuacr204 -g rg-az204 --sku Basic

4. Faça push da imagem:

Bash:  
az acr login -n meuacr204
docker build -t meuacr204.azurecr.io/orders-api:v1 .
docker push meuacr204.azurecr.io/orders-api:v1

5. Crie um Container App usando essa imagem.


# 🧩 Módulo 2 — Criar um Azure App Service Web App

## Habilidades treinadas:

* Criar Web App

* Configurar TLS, configurações, logs

* Implantar contínuo

🔧 Passos:

1. Crie um Web App:

Bash:

az webapp create -g rg-az204 -p plan-az204 -n orders-webapp

2. Registros ativos:

Bash:

az webapp log config -n orders-webapp -g rg-az204 --application-logging filesystem

3. Configure strings de conexão para Cosmos DB e Storage.

4. Crie um slot de staging e faça swap.


# 🧩 Módulo 3 — Criar Azure Functions com triggers

## Habilidades treinadas:

* Gatilhos (HTTP, Temporizador, Blob, Grade de Eventos)

* Bindings de entrada e saída

🔧 Passos:

1. Crie uma Function App com runtime .NET ou Node.

2. Adicione:

* Uma função HTTP para validar pedidos

* Uma função Event Grid para processar eventos de novos pedidos

* Uma função Timer para limpeza diária


# 🧩 Módulo 4 — Trabalhar com Azure Storage

## Habilidades treinadas:

* Armazenamento de Blob

* Metadados e propriedades

* Gestão do ciclo de vida

🔧 Passos:

1. Crie, hum, contêineres, pedidos-arquivos.

2. Faça upload de um arquivo via SDK.

3. Adicione metadados:

csharp:

blobClient.SetMetadata(new Dictionary<string,string>{{"orderId","123"}});

4. Configure política de lifecycle para mover blobs antigos para Cool/Archive.


# 🧩 Módulo 5 — Trabalhar com Azure Cosmos DB

## Habilidades treinadas:

* CRUD via SDK

* Níveis de consistência

* Mudança de Feed

🔧 Passos:

1. Crie um banco ordersdb e container orders.

2. Insira itens via SDK.

3. Leia itens com diferentes níveis de consistência.

4. Crie uma Função com trigger de Change Feed para processar novos pedidos.


# 🧩 Módulo 6 — Implementar Segurança

## Habilidades treinadas:

* Identidade Gerenciada

* Cofre da Chave

* SAS Tokens

* Plataforma de Identidade Microsoft

🔧 Passos:

1. Habilite Managed Identity sem Web App.

2. Armazene a connection string do Cosmos no Key Vault.

3. Configure o Web App para buscar o segredo via Identidade Gerenciada.

4. Gere um SAS Token para acesso temporário ao Blob Storage.

# 🧩 Módulo 7 — Monitoramento e Diagnóstico

## Habilidades treinadas:

* Insights sobre Aplicação

* Logs, métricas, traces

* Alertas

🔧 Passos:

1. Habilite Application Insights sem Web App e Functions.

2. Adicione telemetria customizada:

Csharp:

telemetry.TrackEvent("OrderReceived");

3. Grie alertas para:

* Erros 500

* Latência alta

* Falhas em Funções


# 🧩 Módulo 8 — API Management

## Habilidades treinadas:

* Criar instância

* APIs de importação

* Criar políticas

🔧 Passos:

1. Crie uma instância de API Management.

2. Importe a API do Web App.

3. Adicione políticas:

* Limite de taxa

* Cache

* Validar o JWT


# 🧩 Módulo 9 — Event Grid, Event Hubs e Service Bus

## Habilidades treinadas:

* Soluções baseadas em eventos

* Soluções baseadas em mensagens

🔧 Passos:

1. Crie um Event Grid Topic para novos pedidos.

2. Publique events via API.

3. Crie um Event Hub para telemetria.

4. Crie uma fila Service Bus orders-queue.

5. Crie uma Function com trigger Service Bus.


# 🧩 Módulo 10 — Integração Final

## Monte o fluxo completo:

1. Web App recebe pedido

2. Grid: Publica evento no Event

3. Função de dispara de grade de eventos

4. Function grava no Cosmos DB

5. Change Feed dispara outra Function

6. Function envia mensagem para Service Bus

7. Worker em Container App processa a fila

8. Logs e métricas vão para Application Insights

9. API exposta via API Management

