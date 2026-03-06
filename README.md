# Tech Taste

Projeto desenvolvido para o estudo de Microsserviços.

## 🔨 Funcionalidades do projeto
Essa aplicação é capaz de efetuar o CRUD de um pedido, acompanhar o pagamento e notificar o usuário via e-mail, sobre andamento do pedido.

## Tecnologias e boas práticas
- Java 21 e Spring Boot
- Eureka Server (Serviço de descoberta)
- Open Feign
- API Gateway
- Microsserviços de pedidos, pagamentos e usuários
- Circuit Breaker e Fallback
- Postgre e H2
- RabbitMQ

### Arquitetura
<!-- 
```

           Cliente (Postman / Frontend)
                     │
                     ▼
            API Gateway (:8082)
            /          \
     consulta            roteia requisição
          │                      │
          ▼                      ▼
 Service Registry (:8081)   ms-pedidos (:8080)
  "ms-pedidos → :8080"      ms-pagamentos (:8083)
  "ms-pagamentos → :8083"   ms-usuarios (:8084)
  "ms-usuarios → :8084"
  
  
  ms-pedidos ──── OpenFeign (síncrono) ────► ms-pagamentos
  ms-pedidos ──── RabbitMQ (assíncrono) ───► ms-usuarios

``` -->

![image](https://github.com/user-attachments/assets/c292341a-4a9e-4568-8507-40ccb7cd226a)


## Considerações/ Detalhes

Para execução do projeto, é necessário criar dois databases:

```SQL
CREATE database "ms-pedidos-db";
CREATE database "ms-pagamentos-db";
```

Execute os serviços na seguinte ordem:

```bash
# 1º Sempre o Eureka Server
service-registry

# 2º Gateway
api-gateway;

# 3º Os microsserviços, independente da ordem
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