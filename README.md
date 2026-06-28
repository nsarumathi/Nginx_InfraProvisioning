# Terraform Nginx Ubuntu

## Project Description

This project uses Terraform to provision an AWS EC2 instance running Ubuntu 20.04 LTS in the default VPC. The instance installs and configures the Nginx web server automatically using a user data script and displays a custom web page.
---

## Resources Created

- AWS Provider
- Default VPC (existing AWS resource)
- Default Subnet (existing AWS resource)
- Security Group
  - Allows SSH (Port 22)
  - Allows HTTP (Port 80)
- EC2 Instance
  - Ubuntu 20.04 LTS
  - Instance Type: t2.micro
- User Data Script
  - Installs Nginx
  - Starts and enables Nginx service
  - Replaces the default Nginx page with a custom HTML page
- Output
  - Public IP address of the EC2 instance
---


## Project Structure

```text
terraform-nginx-ubuntu/
│── main.tf
│── variables.tf
│── outputs.tf
│── README.md
```
---

## Steps to Run

### Step 1: Launch EC2 instacne & install required tools
           a.install aws cli & configure
           b.install terraform
  <img width="1707" height="826" alt="EC2" src="https://github.com/user-attachments/assets/22a63ea1-41ed-438a-a51d-12ba677ce02d" />
  <img width="1006" height="832" alt="EC2_SetupTools" src="https://github.com/user-attachments/assets/625b6dfa-fd15-4770-b2d8-a541fa8c1c50" />


### Step 2: Initialize Terraform  & Validate the Configuration

```bash
terraform init
terraform validate
```
<img width="1012" height="832" alt="tf_commands" src="https://github.com/user-attachments/assets/0ae4a440-26c8-4d39-adc3-4cf196774331" />


### Step 3: Review the Execution Plan & deploy infrastructure

```bash
terraform plan
terraform apply
```
<img width="1011" height="822" alt="tf_apply" src="https://github.com/user-attachments/assets/40e241ee-c571-41b9-9bb0-b40361b4b968" />


Terraform creates:

- Security Group which allows port 80,22
- EC2 Instance
<img width="1692" height="722" alt="Provisionied_EC2" src="https://github.com/user-attachments/assets/f3847764-0599-46e8-b337-09124c39db2f" />
<img width="1692" height="605" alt="sg" src="https://github.com/user-attachments/assets/d8fcf8c1-8e2b-492f-b142-69d153a5b851" />


### Step 5: Get the Public IP

After deployment, Terraform displays:

```text
Outputs:

instance_public_ip = xx.xx.xx.xx
```

Open a browser and visit:

```text
http://<instance_public_ip>
```

Expected output:

```text
Welcome to the Terraform-managed Nginx Server on Ubuntu
```
<img width="1440" height="322" alt="ProvisionedEC2_Access" src="https://github.com/user-attachments/assets/31ec0a04-c2fc-4e92-ac6d-0681eac51fd4" />


## Destroy the Infrastructure

To remove all created resources:

```bash
terraform destroy
```

Type:

```text
yes
```
<img width="1067" height="831" alt="tf_destroysuccess" src="https://github.com/user-attachments/assets/5365ff19-c09f-478d-9a5a-3c82be8a9e70" />

Terraform deletes:

- EC2 Instance
- Security Group

The default VPC and subnet remain unchanged.

<img width="1695" height="712" alt="tf_destroysucc2" src="https://github.com/user-attachments/assets/1a31d3d8-f7b0-46f3-8ce6-215e47aa121d" />



## Notes

- Ubuntu 20.04 LTS AMI is used.
- EC2 instance is launched in the default VPC.
- No new VPC, subnet, or Internet Gateway is created.
- Resources are tagged appropriately.
- The infrastructure can be recreated and removed using Terraform commands.
