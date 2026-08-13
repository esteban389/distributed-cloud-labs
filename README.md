# Distributed Systems Lab

A collection of small, isolated experiments around **distributed systems, resilience, messaging, cloud-native architecture, and failure handling**.

Large distributed applications can make it difficult to understand one mechanism at a time.

This repository takes the opposite approach: isolate a behavior, deliberately create the failure condition, observe what happens, and then experiment with strategies for handling it.

# Goals

The repository is intended to explore questions such as:

- What actually happens when a message is delivered twice?
- What happens when a service crashes after committing state but before acknowledging a message?
- How should retries behave during partial failure?
- Why does retry jitter matter?
- How can an operation be made idempotent?
- What guarantees do different messaging approaches provide?
- How can services remain useful when one dependency is unhealthy?
- How do distributed transactions fail?
- How do systems recover from inconsistent state?
- How can failures be observed rather than hidden?

The objective is to move beyond diagrams of distributed systems and reproduce their failure modes in executable experiments.

# Repository Structure

```text
distributed-systems-lab/
├── resilience/
│   ├── retries/
│   ├── exponential-backoff/
│   ├── jitter/
│   ├── circuit-breaker/
│   ├── bulkhead/
│   └── rate-limiting/
│
├── messaging/
│   ├── duplicate-delivery/
│   ├── dead-letter-queue/
│   ├── idempotent-consumer/
│   └── ordering/
│
├── consistency/
│   ├── eventual-consistency/
│   ├── transactional-outbox/
│   ├── saga/
│   └── distributed-lock/
│
├── coordination/
│   ├── leader-election/
│   └── service-discovery/
│
├── observability/
│   ├── tracing/
│   ├── metrics/
│   └── structured-logging/
│
├── chaos/
│   ├── latency/
│   ├── service-failure/
│   └── network-failure/
│
└── infrastructure/
```

The structure will evolve as experiments are added.

# Experiment Format

Whenever practical, experiments should follow a structure similar to:

```text
README.md
docker-compose.yml / infrastructure/
src/
scripts/
results/
```

Each experiment should try to document:

## Problem

What distributed-systems problem is being explored?

## Failure Scenario

What condition will be deliberately introduced?

## Hypothesis

What do I expect to happen?

## Experiment

How can the behavior be reproduced?

## Observations

What actually happened?

## Mitigation

What technique or architectural pattern was introduced?

## Trade-offs

What new complexity or failure mode does that solution create?

This last part is important.

Distributed-systems patterns rarely remove complexity. They usually exchange one set of failure modes for another.

# Cloud Environments

Many experiments will emulate cloud infrastructure locally when possible.

The goal is to experiment with concepts commonly found in AWS and cloud-native systems without requiring every learning exercise to run against paid infrastructure.

Depending on the experiment, infrastructure may include local or AWS-compatible implementations of:

- queues;
- publish/subscribe messaging;
- object storage;
- serverless functions;
- databases;
- event buses;
- containers;
- service discovery.

Real cloud environments may still be used when a behavior cannot be meaningfully reproduced locally.

# Failure Is a Feature

Experiments in this repository should deliberately introduce failure.

Examples include:

- process termination;
- packet loss;
- artificial latency;
- duplicate messages;
- message reordering;
- unavailable dependencies;
- stale reads;
- connection exhaustion;
- database failure;
- consumer crashes;
- expired timeouts.

A distributed system that is only tested while every component is healthy does not reveal very much about distributed systems.

# What This Repository Is Not

This repository is not intended to present every pattern as something that should automatically be used in production.

A distributed solution is not inherently better than a simpler architecture.

Many of these experiments intentionally introduce complexity because the complexity itself is what I want to study.

The goal is to understand the trade-offs well enough to know when not to use them.
