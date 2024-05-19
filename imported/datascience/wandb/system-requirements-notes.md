# Weights & Biases 

## Pricing

After some back and forth, Will Pleskow was able to get the following approvals.

This will be an **academic license**, which is quantified by the end user being academic in nature.

You will have full functionality of the platform, and the prices listed below are for a **1-year agreement**.

1. Private Cloud Deployment: $50,000
2. On-Premise Deployment: $75,000

I have these approvals through the end of February, which should give us enough time.

## System Requirements
### Infrastructure
Hosted by customer on their on-prem infrastructure

- Can be hosted in any of the major cloud providers or (GCP, AWS, Azure, etc.) or on customer's bare-metal servers
- W&B Service (Docker Container) - recommended to run Kubernetes
- Setup an external MySQL5.7/MySQL8 database instance to store metadata from the application
- Setup an external scalable object storage solution to store artifact data logged from the application

W&B Provides Terraform templates for all major private clouds that customers can use to spin up all the required infrastructure

### Scalability
- W&B's docker container currently scales vertically, meaning it scales the resources requirements as opposed to the replica count
- Kubernetes Pod configuration requirements:
    - Minimum configuration (xlarge instances):
        - 4 VCPUs
        - 8 GB Ram
    - Recommended scaling configuration (2xlarge instances):
        - 8 VCPUs
        - 32 GB Ram

### Reliability & Maintenance


