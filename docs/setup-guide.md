# AWS VPC Setup Guide

## Step 1: Create the VPC
- Navigate to **AWS Management Console** → **VPC Dashboard**.
- Click **Create VPC**.
- Set **CIDR Block** to `10.0.0.0/16`.
- Enable **DNS Support** and **DNS Hostnames**.
- Save and note the **VPC ID** for future reference.

## Step 2: Create Subnets
- **Public Subnet**: CIDR Block `10.0.1.0/24`, Region `us-east-1a`.
- **Private Subnet**: CIDR Block `10.0.2.0/24`, Region `us-east-1b`.

## Step 3: Create an Internet Gateway and Route Tables
- Go to the **Internet Gateways** section and click **Create Internet Gateway**.
- Attach the gateway to the VPC you created.
- Create a **Route Table** and add a default route `0.0.0.0/0` to the Internet Gateway.
- Associate the **Public Subnet** with the route table.

## Step 4: Set Up Security Groups

### Bastion Host Security Group:
- Allow **SSH** (port 22) from your IP.
- Allow **HTTP** (port 80) from anywhere (`0.0.0.0/0`).

### Private EC2 Security Group:
- Allow **SSH** (port 22) only from the Bastion Host’s IP.

## Step 5: Launch EC2 Instances
- **Public EC2 Instance** (Bastion Host): Launch in the **Public Subnet**.
- **Private EC2 Instance**: Launch in the **Private Subnet**.

## Step 6: SSH Access to Private EC2
- Connect to the **Bastion Host** using SSH:
  ```bash
  ssh -i BastionKey.pem ubuntu@<Bastion-IP>
