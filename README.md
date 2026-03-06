# Tech Taste

Projeto desenvolvido para o estudo de Microsserviços.

## 🔨 Funcionalidades do projeto
Essa aplicação é capaz de efetuar o CRUD de um pedido, acompanhar o pagamento e notificar o usuário via e-mail, sobre andamento do pedido.

## Tecnologias e boas práticas

```bash
# Backend
Java 21
Spring Boot 3

# Banco
PostgreSQL
H2

# Boas práticas
Microsserviços de pedidos, pagamentos e usuários
Eureka Server (Serviço de descoberta)
API Gateway
Circuit Breaker e Fallback
Message Broker (RabbitMQ e Open Feign)
```

### Arquitetura

![image](https://github.com/user-attachments/assets/c292341a-4a9e-4568-8507-40ccb7cd226a)


## Considerações/ Detalhes

Para execução do projeto, é necessário criar dois databases:

```SQL
CREATE database "ms-pedidos-db";
CREATE database "ms-pagamentos-db";
```

Execute os serviços na seguinte ordem:

```bash
# 1º Serviço de configuração
config-server

# 2º Eureka Server
service-registry

# 3º Gateway
api-gateway;

# 4º Os microsserviços, independente da ordem
ms-pedidos
ms-pagamentos
ms-usuarios
```

As funcionalidades são divididas em 3 microsserviços: `criar pedidos`, `gerenciar pagamentos`, `notificar usuários`.

A comunicação de `pedidos` e `pagamentos`, é **síncrona**, feita pelo `Open Feign`; <br>
Já a parte de `noficar os usuários`, é feita de forma **assíncrona**, e usamos o `RabbitMQ` online para isso.

Temos a `api-gateway`, para direcionar/ redirecionar todas as requisições. Sua porta principal é 8082. <br>
O `service-registry (Eureka)` atua como serviço de descoberta — cada microsserviço se registra nele ao subir, informando seu endereço. O gateway consulta o registry para saber para onde encaminhar cada requisição, o que já deixa a aplicação preparada para escalar com um load balancer.

Além disso, exploramos mecanismos de resiliência, como circuit breaker e fallback, essenciais para manter a estabilidade dos serviços diante de falhas.


## Execução via terminal 
```
# fazer o build
mvn clean install

# executar o spring
mvn spring-boot:run
```