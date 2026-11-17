# icompras

Plataforma de compras online construída em arquitetura de microsserviços.
Cada domínio de negócio (pedidos, produtos, clientes, faturamento e logística) é um serviço independente.
A comunicação assíncrona entre os serviços é feita via Apache Kafka, com infraestrutura local orquestrada por Docker.

Projeto da **AMZTecnologIA** — autor: André Luiz da Câmara Muniz.

## Stack

- Java 25
- Spring Boot 4.1
- Maven
- Apache Kafka (+ Kafka UI)
- Docker / Docker Compose

## Estrutura do repositório

```
backend/
├── services/   # microsserviços Spring Boot (um projeto Maven por serviço)
├── infra/      # infraestrutura Docker (Kafka, bancos, etc.)
└── docs/       # documentação do projeto
```

## Serviços e portas

| Serviço      | Porta | Descrição                                  |
|--------------|-------|--------------------------------------------|
| pedidos      | 8080  | Criação e acompanhamento de pedidos        |
| produtos     | 8081  | Catálogo de produtos                       |
| clientes     | 8082  | Cadastro de clientes                       |
| faturamento  | 8083  | Emissão de faturas e cobrança              |
| logistica    | 8084  | Envio e rastreamento de entregas           |
| kafka-ui     | 8090  | Interface web para inspeção do Kafka       |

## Como rodar

> Em construção. Esta seção será preenchida com as instruções para subir a infraestrutura (`infra/`) e os serviços (`services/*`).

## Convenções

As convenções de código, arquitetura, commits e uso de IA no projeto estão descritas em [CLAUDE.md](CLAUDE.md).
