# Prototype v0.1 — Lineage-Aware Rollback-Capable Digital Life Simulation
Author: Gavin Mai
Purpose: NIW Exhibit — Demonstration of Novel Approach to Self-Healing, Lineage-Tracked Distributed Simulation

---

## 1. Overview

This prototype demonstrates the core concepts of a lineage-aware, 
rollback-capable digital life simulation system. It implements:

- A simple digital "Agent" with internal state.
- A behavior loop (`step()`) that evolves the agent state.
- A Kafka-backed lineage event system that records each state transition.
- A rollback service that restores the agent to a previous known state.
- A replay service that reconstructs the agent's entire evolution from Kafka events.

This minimal version illustrates the foundation of the broader NIW project.
It demonstrates feasibility, architectural clarity, and the novel concept 
of combining digital life simulation with distributed rollback and event lineage.

---

## 2. Architecture Diagram (Mermaid)

```mermaid
flowchart TD
    A[Agent State] -->|step()| B[Simulation Service]
    B -->|emit event| C[Kafka Topic: lineage-events]
    C --> D[Lineage Consumer]
    D --> E[State Store]
    E -->|rollback| F[Rollback Service]
    C -->|replay events| G[Replay Service]
    G --> A
