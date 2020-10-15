# Provision GKE Cluster on GCP with Terraform

This module will help provision a GKE (Google Kubernetes Engine) Cluster on GCP with Terraform. This module only provision Cluster without Node Pool, you could use module [tf-gke-nodepool-gcp](https://github.com/ducmeit1/tf-gke-nodepool-gcp) to create Node Pool.

## Usages

```hcl
module "gke-cluster" {
    source          = "github.com/ducmeit1/tf-gke-gcp"
    
    name            = "gke-dc1"
    gcp_project     = "ducmeit1"
    gcp_region      = "asia-east1"
    gcp_location    = "asia-east1"
    gcp_network     = "global-network"
    gcp_subnetwork  = "gke-dc1-subnet"
    master_ipv4_cidr_block  = "10.255.10.1/28"
    master_authorized_networks_config = [{
        cidr_blocks = [{
            cidr_block      = "10.255.9.1/24"
            display_name    = "bastion"
        }],
    }]
}
```

```shell
terraform plan
terraform apply --auto-approve
```