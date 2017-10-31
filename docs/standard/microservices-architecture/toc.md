

# [.NET 微服务：适用于容器化 .NET 应用的体系结构](index.md)


## [容器和 Docker 简介](container-docker-introduction/index.md)


### [什么是 Docker？](container-docker-introduction/docker-defined.md)


### [Docker 术语](container-docker-introduction/docker-terminology.md)


### [Docker 容器、映像和注册表](container-docker-introduction/docker-containers-images-registries.md)


## [为 Docker 容器选择 .NET Core 还是 .NET Framework](net-core-net-framework-containers/index.md)


### [通用指南](net-core-net-framework-containers/general-guidance.md)


### [何时为 Docker 容器选择 .NET Core](net-core-net-framework-containers/net-core-container-scenarios.md)


### [何时为 Docker 容器选择 .NET Framework](net-core-net-framework-containers/net-framework-container-scenarios.md)


### [决策表：用于 Docker 的 .NET Framework](net-core-net-framework-containers/container-framework-choice-factors.md)


### [使用 .NET 容器时定位的操作系统](net-core-net-framework-containers/net-container-os-targets.md)


### [官方 .NET Docker 映像](net-core-net-framework-containers/official-net-docker-images.md)


## [构建容器化微服务应用](architect-microservice-container-applications/index.md)


### [容器化整体式应用](architect-microservice-container-applications/containerize-monolithic-applications.md)


### [Docker 应用中的状态和数据](architect-microservice-container-applications/docker-application-state-data.md)


### [面向服务的体系结构](architect-microservice-container-applications/service-oriented-architecture.md)


### [微服务体系结构](architect-microservice-container-applications/microservices-architecture.md)


### [每个微服务的数据主权](architect-microservice-container-applications/data-sovereignty-per-microservice.md)


### [逻辑体系结构与物理体系结构](architect-microservice-container-applications/logical-versus-physical-architecture.md)


### [分布式数据管理挑战和解决方案](architect-microservice-container-applications/distributed-data-management.md)


### [标识每个微服务的域模型边界](architect-microservice-container-applications/identify-microservice-domain-model-boundaries.md)


### [微服务之间的通信](architect-microservice-container-applications/communication-between-microservices.md)


### [基于消息的异步通信](architect-microservice-container-applications/asynchronous-message-based-communication.md)


### [创建、改进和版本控制微服务 API 及协定](architect-microservice-container-applications/maintain-microservice-apis.md)


### [微服务可寻址性和服务注册表](architect-microservice-container-applications/microservices-addressability-service-registry.md)


### [根据微服务创建复合 UI，包括多个微服务生成的可视 UI 形状和布局](architect-microservice-container-applications/microservice-based-composite-ui-shape-layout.md)


### [微服务中的复原和高可用性](architect-microservice-container-applications/resilient-high-availability-microservices.md)


### [安排微服务和多容器应用的业务流程，以实现高可伸缩性和高可用性](architect-microservice-container-applications/scalable-available-multi-container-microservice-applications.md)


### [使用 Azure Service Fabric](architect-microservice-container-applications/using-azure-service-fabric.md)


## [Docker 应用开发流程](docker-application-development-process/index.md)


### [Docker 应用开发工作流](docker-application-development-process/docker-app-development-workflow.md)


## [在 Linux 或 Windows Nano Server 主机上部署单容器 .NET Core Web 应用](net-core-single-containers-linux-windows-server-hosts/index.md)


## [将旧版整体式 .NET Framework 应用迁移到 Windows 容器](containerize-net-framework-applications/index.md)


## [设计和开发多容器化微服务 .NET 应用](multi-container-microservice-net-applications/index.md)


### [设计面向微服务的应用](multi-container-microservice-net-applications/microservice-application-design.md)


### [创建简单的数据驱动 CRUD 微服务](multi-container-microservice-net-applications/data-driven-crud-microservice.md)


### [使用 docker-compose.yml 定义多容器应用](multi-container-microservice-net-applications/multi-container-applications-docker-compose.md)


### [使用作为容器运行的数据库服务器](multi-container-microservice-net-applications/database-server-container.md)


### [在微服务（集成事件）之间实现基于事件的通信](multi-container-microservice-net-applications/integration-event-based-microservice-communications.md)


### [使用 RabbitMQ 实现用于开发或测试环境的事件总线](multi-container-microservice-net-applications/rabbitmq-event-bus-development-test-environment.md)


### [订阅事件](multi-container-microservice-net-applications/subscribe-events.md)


### [测试 ASP.NET Core 服务和 Web 应用](multi-container-microservice-net-applications/test-aspnet-core-services-web-apps.md)


## [使用 DDD 和 CQRS 模式降低微服务中的业务复杂性](microservice-ddd-cqrs-patterns/index.md)


### [在微服务中应用简化后的 CQRS 和 DDD 模式](microservice-ddd-cqrs-patterns/apply-simplified-microservice-cqrs-ddd-patterns.md)


### [在 eShopOnContainers 的 DDD 微服务中应用 CQRS 和 CQS 方法](microservice-ddd-cqrs-patterns/eshoponcontainers-cqrs-ddd-microservice.md)


### [在 CQRS 微服务中实现读取/查询](microservice-ddd-cqrs-patterns/cqrs-microservice-reads.md)


### [设计面向 DDD 的微服务](microservice-ddd-cqrs-patterns/ddd-oriented-microservice.md)


### [设计微服务域模型](microservice-ddd-cqrs-patterns/microservice-domain-model.md)


### [使用 .NET Core 实现微服务域模型](microservice-ddd-cqrs-patterns/net-core-microservice-domain-model.md)


### [Seedwork（适用于域模型的可重用基类和接口）](microservice-ddd-cqrs-patterns/seedwork-domain-model-base-classes-interfaces.md)


### [实现值对象](microservice-ddd-cqrs-patterns/implement-value-objects.md)


### [使用枚举类（而不是枚举类型）](microservice-ddd-cqrs-patterns/enumeration-classes-over-enum-types.md)


### [在域模型层中设计验证](microservice-ddd-cqrs-patterns/domain-model-layer-validations.md)


### [客户端验证（表示层中的验证）](microservice-ddd-cqrs-patterns/client-side-validation.md)


### [域事件：设计和实现](microservice-ddd-cqrs-patterns/domain-events-design-implementation.md)


### [设计基础结构持久性层](microservice-ddd-cqrs-patterns/infrastructure-persistence-layer-design.md)


### [使用 Entity Framework Core 实现基础结构持久性层](microservice-ddd-cqrs-patterns/infrastructure-persistence-layer-implemenation-entity-framework-core.md)


### [将 NoSQL 数据库用作持久性基础结构](microservice-ddd-cqrs-patterns/nosql-database-persistence-infrastructure.md)


### [设计微服务应用层和 Web API](microservice-ddd-cqrs-patterns/microservice-application-layer-web-api-design.md)


### [使用 Web API 实现微服务应用层](microservice-ddd-cqrs-patterns/microservice-application-layer-implementation-web-api.md)


## [实现复原应用](implement-resilient-applications/index.md)


### [处理部分失败错误](implement-resilient-applications/handle-partial-failure.md)


### [部分失败错误的处理策略](implement-resilient-applications/partial-failure-strategies.md)


### [实现使用指数退避算法的重试](implement-resilient-applications/implement-retries-exponential-backoff.md)


### [实现复原 Entity Framework Core SQL 连接](implement-resilient-applications/implement-resilient-entity-framework-core-sql-connections.md)


### [实现使用指数退避算法的自定义 HTTP 调用重试](implement-resilient-applications/implement-custom-http-call-retries-exponential-backoff.md)


### [使用 Polly 实现使用指数退避算法的 HTTP 调用重试](implement-resilient-applications/implement-http-call-retries-exponential-backoff-polly.md)


### [实现断路器模式](implement-resilient-applications/implement-circuit-breaker-pattern.md)


### [运行状况监视](implement-resilient-applications/monitor-app-health.md)


## [保护 .NET 微服务和 Web 应用](secure-net-microservices-web-applications/index.md)


### [关于 .NET 微服务和 Web 应用中的授权](secure-net-microservices-web-applications/authorization-net-microservices-web-applications.md)


### [在开发过程中安全地存储应用机密](secure-net-microservices-web-applications/developer-app-secrets-storage.md)


### [在生产时使用 Azure Key Vault 保护机密](secure-net-microservices-web-applications/azure-key-vault-protects-secrets.md)


## [关键结论](key-takeaways.md)
