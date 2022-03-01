# Microservices and Component Decoupling

## ECS
- Elastic Container Service
- Secrets manager integration: KMS, password  (RDS)rotation, more expensive than SSM param store
    - Secrets mgr and ECS cluster must be in the same account
    - When to use:
        - SSM Param store: single store for configuration and secrets
        - Secrets mgr: dedicated secrets store with lifecycle management
    - `Docker Secrets`. Secrets mgr for Docker Swarm, not used w ECS
- For spot instances to use `connection draining` must **manually** set this option: `ECS_ENABLE_SPOT_INSTANCE_DRAINING=true` in the local `/etc/ecs/ecs.config` file. 

Spot instances cluster: 
- Choose `Diversified` provisioning mode which lets ECS choose the best instance size
    - combined w spot instance draining keeps uptime high.  

## Apache Camel
- Open source integration framework. 
- uses queueing, message bus, etc. 
> Camel is an Open Source integration framework that empowers you to quickly and easily integrate various systems consuming or producing data. - https://camel.apache.org/

## Containers vs VM
- performance: containers spin up faster
- size: containers smaller (MB's vs Gb)
