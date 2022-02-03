# Compute

## Load Balancers
## Network Load balancer
- used for high perfomance (supports millions of requests/second)
- works at layer 4
- minimal routing capabilities (port number)
- improves security by improving availability (removes single point of failure)
- supports authentication with mutual TLS (2-way SSL).   See [Configuring Mutual TLS authentication for applications running on Amazon EKS](https://docs.aws.amazon.com/prescriptive-guidance/latest/patterns/configure-mutual-tls-authentication-for-applications-running-on-amazon-eks.html). Example use cases: [Open Banking](https://docs.aws.amazon.com/wellarchitected/latest/financial-services-industry-lens/open-banking.html) ![](https://docs.aws.amazon.com/prescriptive-guidance/latest/patterns/images/pattern-img/ae2761e3-7ed2-4c2a-ba54-a4ddce8a1e7e/images/cefc60f9-2f29-4052-b7ae-df4eb6395e1c.png)
