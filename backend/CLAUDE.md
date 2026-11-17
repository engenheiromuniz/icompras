# iCompras — convenções para a IA (AMZTecnologIA)
Autor e responsável técnico: André Luiz da Câmara Muniz (decide arquitetura; a IA implementa).
## Stack
Java 25, Spring Boot 4.1.x, Maven (use ./mvnw), PostgreSQL 17 + Flyway, Spring for Apache Kafka
(Kafka 4 KRaft),
HTTP Interface (@HttpExchange) para chamadas entre serviços — NUNCA OpenFeign/Spring Cloud.
springdoc-openapi 3.x (Swagger), JUnit 5 + AssertJ + Mockito + Testcontainers, MapStruct (pedidos).
## Estrutura
Monorepo: services/<nome>-service, infra/, docs/adr, docs/demandas.
Pacote: br.com.amztecnologia.icompras.<servico>. Subpacotes: api, api.dto, service, repository,
domain,
infra (http, kafka, s3, outbox), config, exception.
## Regras obrigatórias
- DTOs são records (XxxRequest, XxxResponse, XxxEvent). Entidade JPA nunca sai do service.
- Entidades: @Getter/@Setter/@NoArgsConstructor; NUNCA @Data. Dinheiro: BigDecimal (escala 2).
- Erros em ProblemDetail via GlobalExceptionHandler. 201+Location em criação; exclusão lógica.
- Banco só via Flyway (nunca editar migration aplicada); ddl-auto=validate.
- Escritas @Transactional; leituras @Transactional(readOnly=true); nenhuma chamada HTTP dentro de
  transação.
- Eventos: JSON como String (StringSerializer), chave = id do agregado, records próprios por
  serviço.
- Publicar eventos de domínio SEMPRE via outbox no pedidos-service.
- Nunca logar dados pessoais (CPF, e-mail) nem de pagamento. Segredos só por variável de ambiente.
- Testes: nomes deve_<resultado>_quando_<condicao>; integração com Testcontainers.
- Commits: Conventional Commits em português, minúsculas, imperativo.
## Como responder
Antes de codar, apresente o plano (arquivos e responsabilidades). Entregue arquivo por arquivo com
caminho
completo. Termine listando pontos de atenção para revisão.