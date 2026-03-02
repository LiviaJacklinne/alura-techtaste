# Api Gateway

## Anotações / Explicações
### 1 - spring.cloud.gateway.discovery.locator.enabled=true

Essa propriedade habilita o Discovery Locator no Spring Cloud Gateway.

Quando ativada:

O Gateway automaticamente cria rotas dinâmicas para os serviços registrados no Eureka Server (não precisa definir manualmente).

Exemplo de funcionamento:

Se o Eureka Server tem os seguintes serviços registrados:

`ms-pedidos (executando em http://localhost:5050)` <br>
`ms-pagamentos (executando em http://localhost:5051)`

O Gateway cria rotas dinâmicas para acessar esses serviços, como:

http://localhost:8082/ms-pedidos/ → Encaminha as requisições para o serviço ms-pedidos.
http://localhost:8082/ms-pagamentos/ → Encaminha as requisições para o serviço ms-pagamentos.

### 2 - spring.cloud.gateway.discovery.locator.lower-case-service-id=true

Essa propriedade converte o ID dos serviços registrados no Eureka para letras minúsculas ao criar rotas dinâmicas.

Por padrão, os IDs dos serviços no Eureka podem conter letras maiúsculas e minúsculas. Contudo, algumas ferramentas ou convenções preferem trabalhar com IDs em minúsculas para evitar problemas de case sensitivity.