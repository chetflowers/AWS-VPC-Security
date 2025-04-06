# 🛡️ AWS VPC Security Lab

Hands‑on guide for spinning up a **two‑tier VPC**: public bastion up front, private subnet hiding everything else. Quick, tight, and zero fluff.

[![License](https://img.shields.io/github/license/chetflowers/AWS-VPC-Security?color=blue)](LICENSE)  
[![Last Commit](https://img.shields.io/github/last-commit/chetflowers/AWS-VPC-Security)](../../commits)  
[![Stars](https://img.shields.io/github/stars/chetflowers/AWS-VPC-Security?style=social)](../../stargazers)

## Architecture (the 30‑second version)

* Public subnet `10.0.1.0/24` – Bastion EC2, one Elastic IP, SSH allowed **only from your laptop**
* Private subnet `10.0.2.0/24` – Workload EC2, no direct Internet
* Internet Gateway + optional NAT if your private stuff needs outbound calls
* Security Groups + Network ACLs + VPC Flow Logs because logs save lives
* Diagram lives at `screenshots/vpc-architecture.png`

## Quick start (all clicky‑click in the AWS console)

1. VPC Wizard → “VPC with Public and Private Subnets”  
2. Name it **vpc-security-lab** and keep the default CIDR `10.0.0.0/16`  
3. Tweak the subnets so they match the CIDRs above  
4. Make two Security Groups  
   * **bastion-sg** → inbound SSH (22) from *your* IP  
   * **private-sg** → inbound SSH (22) from bastion‑sg  
5. Launch a t3.micro in each subnet with the right SG  
6. SSH flow: **you → bastion → private host**. Done.

## Repo map

* `docs/setup-guide.md` – step‑by‑step with screenshots  
* `docs/security-hardening.md` – extra lock‑down tricks (Flow Logs, IAM, etc.)  
* `docs/troubleshooting.md` – “why can’t I SSH?” greatest hits  
* `screenshots/` – all the PNG receipts  
* `LICENSE` – MIT, so go wild

## Screenshot sampler

* `screenshots/vpc-created.png` – fresh VPC in the console  
* `screenshots/subnets.png` – public vs. private layout  
* `screenshots/sg-rules.png` – SG rules that keep the noise out

## Stuff still on the whiteboard

* Terraform version (because IaC is king)  
* Least‑privilege IAM policy example  
* 90‑second demo GIF

## License

MIT
