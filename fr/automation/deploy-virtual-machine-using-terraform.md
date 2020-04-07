---
title: "Déployer une machine virtuelle à l'aide de Terraform"
slug: deployer-une-machine-virtuelle-a-l-aide-de-terraform
---


Utiliser [Terraform](https://www.terraform.io/) pour créer une instance basée sur une offre avec ressources personnalisées.

### Prérequis

- [Terraform](https://www.terraform.io/downloads.html) installé localement
- Installer le pilote terraform pour cloud.ca [https://github.com/cloud-ca/terraform-provider-cloudca](https://github.com/cloud-ca/terraform-provider-cloudca)
- votre *api_key* pour cloud.ca
- *environment_id*
- *network_id*,  sous réseau de votre VPC auquel l'instance sera connectée.


### Définition des ressources

Se référer à [la documentation du pilote](https://github.com/cloud-ca/terraform-provider-cloudca/tree/development/cloudca#cloudca_instance) afin de connaître les attributs les plus récents.

```
resource "cloudca_instance" "prod-app01" {
  environment_id = "4cad744d-bf1f-423d-887b-bbb34f4d1b5b"
  name = "prod-app01"
  network_id = "672016ef-05ee-4e88-b68f-ac9cc462300b"
  template = "CentOS 7.4 HVM"
  compute_offering = "Standard"
  ssh_key_name = "my_ssh_key"
  root_volume_size_in_gb = 100
     cpu_count = 1
     memory_in_mb = 1024
}
```

Créer plusieurs instances du même type :

```
resource "cloudca_instance" "prod-app" {
  count = "10"
  environment_id = "4cad744d-bf1f-423d-887b-bbb34f4d1b5b"
  name = "prod-app${count.index}"
  network_id = "672016ef-05ee-4e88-b68f-ac9cc462300b"
  template = "CentOS 7.4 HVM"
  compute_offering = "Standard"
  ssh_key_name = "my_ssh_key"
  root_volume_size_in_gb = 100
  cpu_count = 1
  memory_in_mb = 1024
}
```
