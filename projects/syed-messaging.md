# Syed.Messaging

**Public, MIT-licensed, transport-agnostic .NET messaging framework** — one API across RabbitMQ, Kafka, and Azure Service Bus, with the operational stack built in rather than bolted on.

🔗 **[github.com/moshiur/Syed.Messaging](https://github.com/moshiur/Syed.Messaging)** — this one you can read right now.
📦 **16 packages on [NuGet](https://www.nuget.org/packages?q=Syed.Messaging), 4,700+ combined downloads**, currently at v1.3.0.

## What it is

```csharp
// Register everything in one fluent chain — swap the transport without touching handler code
services.AddMessaging(builder => ...);
```

- 🔌 **One API, three transports** — RabbitMQ, Kafka, Azure Service Bus
- 🧰 **Production patterns included** — outbox, inbox, sagas, retry + DLQ, middleware pipeline, RPC, health checks
- 📊 **Observability-first** — OpenTelemetry traces, 7 counters + 1 histogram, a DLQ dashboard, and a KEDA autoscaling playbook ship with the library
- 📖 **Migration guide from MassTransit** — consumer registration, sagas, outbox, retry, and middleware side by side

## The package family

`Abstractions` · `Core` · `RabbitMq` · `Kafka` · `AzureServiceBus` · `Outbox.EfCore` · `Inbox.EfCore` · `Sagas` · `Sagas.EfCore` · `Sagas.Redis` · `OpenTelemetry` · `HealthChecks` · `SignalR` · `Aspire` · `Chaos` · `BuildingBlocks`

## Architecture at a glance

```mermaid
flowchart LR
    App["Your handlers<br/>(transport-agnostic)"] --> Core["Syed.Messaging.Core<br/>pipeline · retry · DLQ"]
    Core --> R["RabbitMq"]
    Core --> K["Kafka"]
    Core --> A["AzureServiceBus"]
    Core --- OB["Outbox / Inbox<br/>(EF Core)"]
    Core --- SG["Sagas<br/>(EF Core / Redis)"]
    Core --- OT["OpenTelemetry<br/>+ Prometheus"]
    Core --- HC["HealthChecks<br/>+ KEDA scaling"]
```

**Dogfooded in production-style use:** the [Help or Yelp](help-or-yelp.md) microservices communicate exclusively through these packages — outbox, retry, and the SignalR bridge included. Library pain points get found by the library author.

## Why it's interesting engineering-wise

- Designing a **transport abstraction that doesn't leak** is the hard part — delivery semantics, partitioning, and dead-lettering differ meaningfully across the three brokers
- The timing matters: built as MassTransit announced its move to commercial licensing — an MIT-licensed alternative with the operational patterns teams actually rely on
- 120 automated tests, CI/CD publishing pipeline via GitHub Actions, versioned docs, a chaos-testing package (`Syed.Messaging.Chaos`) for failure injection
- Real-world operability: DLQ-driven autoscaling means consumers scale on *backlog pain*, not just CPU

[← Back to portfolio](../README.md)
