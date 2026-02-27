![Programação-Arquitetura de microsserviços com Java e Spring](https://github.com/user-attachments/assets/1e496c6c-bcd6-49c4-84f3-bce6fb11074d)

![](https://img.shields.io/github/license/alura-cursos/android-com-kotlin-personalizando-ui)

# Tech Taste

App de simulação de uma empresa de delivery para o curso de Arquitetura de microsserviços com Java e Spring. O projeto nos dá a possibilidade de implementar aplicações autônomas e independentes, trabalhando conceitos primordiais para esse tipo de arquitetura.

## 🔨 Funcionalidades do projeto

Para praticar o design e projeto de uma arquitetura de microsserviços, vamos implementar os seguintes componentes:

- `Serviço de registro e descoberta`: uso do Eureka Server, utilizado amplamente no ecossistema Spring Cloud.
- `API Gateway`: componente que vai atuar como ponto de entrada único para todas as requisições feitas pelos clientes (como frontend, mobile ou terceiros)
- `Microsserviços de pedidos, pagamentos e usuários`: todas essas aplicações serão independentes, com seu próprio banco de dados, e irão comunicar-se entre si.
- `Config Server`: um serviço do Spring Cloud que permite centralizar e gerenciar configurações de múltiplos microsserviços.

Utilizaemos estratégias de comunicação, tanto síncrona quanto assíncrona, utilizando message brokers para garantir eficiência e escalabilidade.

Além disso, exploramos mecanismos de resiliência, como circuit breaker e fallback, essenciais para manter a estabilidade dos serviços diante de falhas.

![image](https://github.com/user-attachments/assets/c292341a-4a9e-4568-8507-40ccb7cd226a)

## 📚 Mais informações do curso

Gostou do projeto e quer conhecer mais? Você pode acessar o site do curso que desenvolve o projeto desde o começo!
