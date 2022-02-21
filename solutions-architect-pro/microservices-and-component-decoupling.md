# Microservices and Component Decoupling

## ECS
- Elastic Container Service
- Secrets manager integration: KMS, password  (RDS)rotation, more expensive than SSM param store
    - Secrets mgr and ECS cluster must be in the same account
    - When to use:
        - SSM Param store: single store for configuration and secrets
        - Secrets mgr: dedicated secrets store with lifecycle management
    - `Docker Secrets`. Secrets mgr for Docker Swarm, not used w ECS

## Apache Camel
- Open source integration framework. 
- uses queueing, message bus, etc. 
> Camel is an Open Source integration framework that empowers you to quickly and easily integrate various systems consuming or producing data. - https://camel.apache.org/