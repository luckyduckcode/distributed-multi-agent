# Distributed Multi-Agent Automation System

A pragmatic architecture for running a **central AI brain** and **distributed sub-agents** across multiple machines using **Docker Swarm**, **Ansible**, and lightweight agent containers.

This project is currently an **architecture and planning repository**. It documents a buildable approach for combining centralized reasoning with decentralized execution for tasks such as patching, monitoring, configuration management, failover, and workload orchestration.

## Project Vision

The system is designed around one simple idea:

- **Centralized intelligence** on a manager node
- **Distributed execution** on every node in the cluster

The central brain handles reasoning, planning, and delegation. Sub-agents run on each machine, perform local work, and escalate complex decisions back to the central brain when needed.

## Architecture Summary

### Node Roles

**Master Node (Swarm Manager)**
- Runs Docker Swarm manager services
- Hosts the central AI brain
- Coordinates the cluster
- Maintains SSH access for Ansible-driven automation

**Worker Nodes (Swarm Workers)**
- Run lightweight sub-agent containers
- Perform local tasks and health checks
- Execute automation workflows
- Call the central brain when higher-level reasoning is required

### Core Stack

| Layer | Technology | Purpose |
| --- | --- | --- |
| Infrastructure | Docker | Package services into portable containers |
| Orchestration | Docker Swarm | Deploy, scale, network, and recover services across nodes |
| Automation | Ansible | Execute safe, repeatable changes over SSH |
| Intelligence | Hermes Agent or Ollama-based brain | Planning, reasoning, and delegation |
| Edge Execution | PicoClaw or lightweight sub-agents | Local autonomy and distributed action |

## How It Works

1. A user or scheduled workflow submits an objective to the central brain.
2. The central brain decomposes the work into smaller tasks.
3. Sub-agents running on each node receive instructions.
4. Each sub-agent inspects local state and performs the required work.
5. If a task needs more reasoning, the sub-agent calls the central brain API.
6. Execution happens through Ansible playbooks, SSH actions, or node-local automation.
7. Results flow back to the central brain for coordination and future improvement.

## Why This Design

- **Scalable:** New worker nodes can join the Swarm and receive a sub-agent automatically.
- **Resilient:** Distributed agents keep execution close to the systems being managed.
- **Consistent:** Containers standardize runtime environments across all machines.
- **Auditable:** Ansible provides predictable, idempotent automation.
- **Extensible:** The architecture can grow from a 4-node setup to larger clusters.

## Current Repository Contents

```text
.
├── README.md
└── distributed-swarm-computing/
    ├── DEFINITIONS EXPLANATIONS.txt
    └── DISTRIBUTED MULTI AGENT.txt
```

### Included Documents

- **`distributed-swarm-computing/DEFINITIONS EXPLANATIONS.txt`**  
  Glossary and role descriptions for the main technologies and concepts.

- **`distributed-swarm-computing/DISTRIBUTED MULTI AGENT.txt`**  
  Rough architecture draft covering node roles, layers, data flow, scaling, and security.

## Suggested Initial Deployment Shape

- **1 manager node** for orchestration and the central AI brain
- **3 worker nodes** for distributed sub-agent execution
- **1 overlay network** for internal service discovery and private communication
- **1 global sub-agent service** so each node automatically runs one local agent

## Security Considerations

- Mount SSH keys read-only where possible
- Keep internal traffic on the Swarm overlay network
- Limit container privileges
- Prefer audited Ansible workflows over ad hoc remote commands
- Expose external access only through deliberate entry points

## Potential Use Cases

- Automated patching across a fleet of machines
- Distributed monitoring and health remediation
- Configuration drift detection and correction
- Intelligent task delegation across heterogeneous nodes
- Event-driven operational workflows

## Roadmap

Short-term priorities:

1. Define the central brain service interface
2. Containerize the sub-agent runtime
3. Create initial Ansible playbooks for a single workflow
4. Add Docker Swarm stack definitions
5. Test monitoring and patching end to end on a small cluster

## Status

This repository is an **early-stage design baseline**. The current material focuses on architecture, terminology, and deployment direction rather than implementation code.

## License

No license has been added yet.
