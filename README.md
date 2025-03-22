
# Proxmox Terraform VM Example 
This repository provides a Terraform example for deploying a virtual machine (VM) to a Proxmox VE server. It demonstrates how to use the Terraform Proxmox provider to provision a VM in a local environment, mirroring the experience of deploying VMs in cloud environments like AWS, Azure, GCP, or even VMware.

- This is a working and tested example; that should be easy to setup and will do my best below for that.
- For production environments, you'll typically use Terraform within CI/CD pipelines alongside other tools.

- Terraform in 2 Hours:** If you're looking for a comprehensive introduction to Terraform on AWS, this video is a great resource:
    * [https://www.youtube.com/watch?v=SLB_c_ayRMo&t=12s](https://www.youtube.com/watch?v=SLB_c_ayRMo&t=12s)
- This repo is for Proxmox - something you setup can your home.
    * Any working server / desktop / laptop will work to get started.
    * Go to proxmox.com and download a ISO, burn a USB key and boot off the key
    * You will setup the Proxmox server and have a root user and password
    * If you get me feedback; can update this documentation to improve.
    * This example focuses on basic VM deployment.
-Cost-Effective Practice:**
    * Cloud platforms are excellent, but they come with costs.
    * It essential to understand that real-world Terraform usage involves more complex workflows and integrations.
    * This Proxmox setup lets you practice Terraform with real virtual machines without incurring those costs. You can experiment, make mistakes, and learn from them without worrying about a hefty bill.
    * This is especially crucial for beginners who want to explore Terraform's capabilities without financial risk.
    * If on cloud - if you pause and come back later; there is a cost the whole time 
- Hands-On, Tangible Results:**
    * Instead of just reading documentation or watching videos, you'll be actively creating and managing real VMs. This hands-on experience solidifies your understanding of Terraform concepts.
    * You can see the direct impact of your Terraform code, which reinforces the learning process.
-Bridging the Gap to Cloud:**
    * The structure and workflow of this example are designed to closely resemble how Terraform is used in cloud environments. This makes it easier to transition to cloud deployments later on.
    * You'll learn the fundamental concepts of infrastructure as code (IaC) in a familiar context, preparing you for more complex cloud architectures.

## Features

* **VM and Container Creation:** Simplifies the creation of Proxmox VMs and LXC containers.
* **Networking Configuration:** Manages network interfaces, bridges, and VLANs.
* **Storage Management:** Handles storage pools and disk configurations.
* **Cloud-Init Support:** Integrates with Cloud-Init for initial VM/container configuration.
* **Template Support:** Enables deployment from existing Proxmox templates.
* **Resource Customization:** Allows fine-grained control over CPU, memory, and disk resources.
* **Firewall Management:** Basic firewall rule management.
* **SSH Key Injection:** Injects SSH keys for secure access.

## Prerequisites

- Terraform installed (version >= 1.5 recommended).
- Proxmox VE server accessible 3.7-1 or later
- Proxmox user or root user and password
- Appropriate Proxmox storage and network configurations.
- This Pipeline uses a `proxmox-base-module` for simplified VM creation. 
[https://github.com/ejbest/proxmox-base-module](https://github.com/ejbest/proxmox-base-module)

## Variables

| Name                  | Description                                    | Type          | Default | 
| :-------------------- | :--------------------------------------------- | :------------ | :------ |
| proxmox_host          | IP you used for your proxmox host              | quoted string |         |
| proxmox_node_hostname | Hostname you called your proxmox host "blue    | quoted string |         |
| `proxmox_password`  | Proxmox password.                              | string |         | Yes     |
| `node`              | Proxmox node name.                             | string |         | Yes      |
| `storage`           | Proxmox storage pool.                          | string |         | Yes      |
| `network_bridge`    | Proxmox network bridge.                        | string |         | Yes      |
| `vms`               | Map of VM configurations.                      | map    | `{}`    | No       |

       = "blue3"
  pm_api_url                = "https://${local.proxmox_host}:8006/api2/json"
  pm_user                   = "root@pam"
  proxmox_host_ssh_password = 88888888
  iso_storage_pool          = "local"
  storage_pool              = "local-lvm"
  cloud-init-disk-name      = "cloud-init-disk-name"
  ip_address                = "192.168.3.131"
  gateway                   = "192.168.3.1"
  hostname                  = "example-vm1"
  ipconfig                  = "ip=192.168.3.131/24,gw=192.168.3.1"
  network_bridge            = "vmbr0"
  private_ssh_keyname       = "key.pem"
  ssh_user                  = "ej"
  cores                     = 1
  sockets                   = 1
  memory                    = 1024
  disk_size                 = 20
  vmid                      = 8001
  cloud_init_config_file    = "cloud-init.yaml"


## Outputs

1.  **Clone the module:**

    ```bash
    git clone <repository_url>
    cd <module_directory>
    ```

3.  **Initialize Terraform:**

    ```bash
    terraform init
    ```

4.  **Plan and apply:**

    ```bash
    terraform plan
    terraform apply
    ```

## Contributing

Contributions are welcome! Please submit a pull request or open an issue for any bugs or feature requests.

## License

This module is licensed under the MIT License.
