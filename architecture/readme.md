# Architecture

Let's describe the architectural philosophies that OSF follows and supports.

## Microservices

OSF is designed to be used to build microservices. A microservice is a small, independent, and loosely coupled service that can be deployed and scaled independently.

## Best Practices

> External References:
>
> - [Chris Richardson: Microservice Architecture](https://microservices.io/patterns/microservices.html)
> - [7 Microservices Best Practices for Developers - by Michael Bogan](https://dzone.com/articles/7-microservices-best-practices-for-developers)
> - [KongHQ: Microservices Architectures](https://konghq.com/learning-center/microservices/microservices-architectures)
> - [Single Responsibility Principle](https://en.wikipedia.org/wiki/Single-responsibility_principle)

### Single Responsibility Principle

  Adopting a microservices strategy requires embracing the [single responsibility principle](https://en.wikipedia.org/wiki/Single-responsibility_principle). By limiting the scope of responsibility for any single service, we limit the negative impact of that service failing. If a single microservice is responsible for too much, its failure or unavailability will have a domino effect on the rest of the system.

  A microservice should be just that: micro. Keep the app domain of your microservices small, dedicated to one logical functionality. This will reduce the impact that a given microservice has if any issues arise. In addition, smaller services are simpler to maintain. The result is easier updating and faster development.

### Separation of Data Stores

  Multiple microservices connecting to the same database are still, in essence, a monolithic architecture. The monolith is just at the database layer instead of the application layer, making it just as fragile. Each microservice should have, as much as possible, its own data persistence layer. This not only ensures isolation from other microservices but also minimizes the blast radius if that particular data set were to become unavailable.

### Communication Channels

  There are two types of communication between microservices: synchronous and asynchronous. Synchronous communication is when one microservice calls another microservice and waits for a response. Asynchronous communication is when one microservice calls another microservice and does not wait for a response. Synchronous communication is more efficient, but it can lead to a bottleneck if the called microservice is slow or unavailable. Asynchronous communication is less efficient, but it is more resilient to failure.

### Compatibility

  As much as possible, maintain backward compatibility, so your consumers don’t encounter broken APIs. The popular way to do this is by following path level compatibility guarantees like `/api/v1` or `/api/v2`. Any backward-incompatible changes go to a new path like `/api/v3`.

  However, despite our best efforts as software engineers, sometimes we need to deprecate APIs, so we’re not stuck running them forever. Use [Deprecation Header](https://datatracker.ietf.org/doc/html/draft-ietf-httpapi-deprecation-header), [Deprecation Link](https://tools.ietf.org/html/draft-dalal-deprecation-link) & [Sunset Header](https://datatracker.ietf.org/doc/html/draft-ietf-httpapi-deprecation-header) to notify your consumers that an API is deprecated.

### Orchestrating Microservices

  Orchestration of your microservices is a key factor of success in both process and tooling. Technically, you could use something like systemd and Docker or podman to run containers on a virtual machine, but that doesn’t provide the same level of resiliency as a container orchestration platform. This negatively affects the uptime and availability benefits that come with adopting a microservices architecture. For effective microservice orchestration, you’ll want to rely on a battle-tested container orchestration platform; and the clear leader in that field is Kubernetes.

### Microservices Security

  As your application comprises more and more microservices, ensuring proper security can become a complicated beast. A centralized system for enforcing security policies is vital to protecting your overall application from malicious users, invasive bots, and faulty code. API Gateway ought to be the start of your security story with microservices, whether you’re running on VMs or in Kubernetes. They support middlewares (plugins) for security which makes it easy to address some of the most common needs for microservices, including authentication, authorization, traffic control, and rate limiting.

### Observability (o11y)

  An architecture built on microservices can lead to massive scaling of hundreds or thousands of small, modular services. While that yields huge potential for increased speed, availability, and reach, a sprawling system of microservices requires a strategic and systematic approach to o11y. By keeping an eye on all of your microservices, you'll ensure that they are functioning as they ought to, are available to your users, and are using resources appropriately. When any of these expectations are not met, you can respond by taking proper action.

  > - [Observability (o11y)](/o11y/)

### Design Patterns

- [Event-Driven Architecture (EDA)](./eda.md)
- [Hexagonal Architecture](./hexagonal.md)
- [Event Sourcing Pattern](./event-sourcing.md)
- [Saga Pattern](./saga.md)
- [CQRS](./cqrs.md)
- [Micro Frontends](https://micro-frontends.org/)
