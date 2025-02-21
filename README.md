# AWS VPC Security Project 🚀

## Overview
This project documents the setup of a **secure AWS Virtual Private Cloud (VPC)** with a **Bastion Host**, a **Private EC2 Instance**, and properly configured firewall rules. This was done manually via the AWS Management Console, and includes detailed step-by-step documentation with screenshots.

## Features
✅ **Public-EC2 (Bastion Host)** for secure access.  
✅ **Private-EC2** with no direct public exposure.  
✅ **Internet Gateway & Route Tables** for controlled access.  
✅ **Key-based SSH authentication** (No password login).  
✅ **Root login disabled** for added security.  
✅ **Security Groups & Network ACLs** for access control.  
✅ **Step-by-step guide with screenshots.**  

---

## Project Structure
```
AWS-VPC-Security/
├── README.md                # Project overview & usage guide
├── docs/                    # Detailed setup and configuration guides
│   ├── setup-guide.md        # Step-by-step AWS VPC setup with screenshots
│   ├── security-hardening.md # Best security practices
│   └── troubleshooting.md    # Common issues and fixes
├── config/                  # Configuration files
│   ├── vpc-config.json      # VPC + subnet details
│   ├── security-groups.json # Security group rules
│   └── route-tables.json    # Routing setup
└── screenshots/             # AWS console and CLI screenshots
```

---

## Requirements
✅ **AWS Account** with IAM permissions to create VPC resources.  
✅ **AWS Management Console Access** (No CLI automation required).  
✅ **SSH Key Pair** for secure authentication.  
✅ **Basic Networking & AWS Knowledge.**  

---

## Setup & Configuration
### **Step 1: Create the VPC**
- Navigate to **AWS Management Console** → **VPC Dashboard**.
- Click **Create VPC**.
- Set **CIDR Block** to `10.0.0.0/16`.
- Enable **DNS Support & DNS Hostnames**.
- Save & note the **VPC ID**.
- 📸 **[Screenshot] VPC Created**

### **Step 2: Configure Subnets**
- Create a **Public Subnet** (`10.0.1.0/24` in `us-east-1a`).
- Create a **Private Subnet** (`10.0.2.0/24` in `us-east-1b`).
- 📸 **[Screenshot] Subnets Created**

### **Step 3: Set Up Internet Gateway & Route Tables**
- Create **Internet Gateway**, attach to **VPC**.
- Create **Route Table** and add **0.0.0.0/0 → Internet Gateway**.
- Associate **Public Subnet** with **Public Route Table**.
- 📸 **[Screenshot] Route Tables Configured**

### **Step 4: Security Group Rules**
- **Bastion SG:** Allow **SSH from your IP** (`22/TCP`).
- **Private EC2 SG:** Allow **SSH only from Bastion Host**.
- 📸 **[Screenshot] Security Groups Configured**

### **Step 5: Deploy Bastion & Private EC2**
- Launch **Bastion Host** in **Public Subnet**.
- Launch **Private EC2** in **Private Subnet**.
- Associate Bastion Host with **Bastion SG**.
- Associate Private EC2 with **Private EC2 SG**.
- 📸 **[Screenshot] Instances Running**

### **Step 6: Connect to Private EC2 via Bastion**
```bash
ssh -i Public-EC2.pem ubuntu@<Public-EC2-IP>
ssh -i Public-EC2.pem ubuntu@<Private-EC2-IP>
```
- 📸 **[Screenshot] SSH from Bastion to Private EC2**

---

## Security Best Practices
- 🚫 **Disable Password Authentication**: Enforce key-based SSH.
- 🔒 **Restrict Security Groups**: Limit access by IP.
- 📜 **Enable AWS CloudTrail**: Track API events.
- 🔐 **Use IAM Roles**: Avoid static AWS credentials.
- 📊 **Monitor with AWS GuardDuty & VPC Flow Logs**.

---

## Screenshots
📸 **VPC Dashboard**  
📸 **Security Group Rules**  
📸 **Route Table Configuration**  
📸 **SSH Bastion to Private EC2**  
(All images stored in `screenshots/` folder.)

---

## Troubleshooting
### SSH Connection Issues
If you can’t SSH into the Private EC2:
```bash
ssh -v -i Public-EC2.pem ubuntu@<Private-EC2-IP>
```
Check security group rules and route table settings.

### No Internet from Private EC2
Ensure **NAT Gateway** or Bastion forwarding is set up.
```bash
curl -s ifconfig.me  # Check outbound traffic
```

---

## License
This project is licensed under the **MIT License**.

---

## Acknowledgments
Thanks to **AWS**, **Cloud Security Experts**, and **Cybersecurity Communities** for guidance.

---

### **🔥 Next Steps**
✅ **Upload Configuration & Screenshots**  
✅ **Finalize Documentation**  
✅ **Test Security Measures**  
🚀 **Expand with AWS WAF & Logging**  

---

### **🌟 Contributing**
Pull requests are welcome! If you have security improvements or optimizations, feel free to contribute.

---

🔥 **Project Complete? No, Just the Beginning.** 🚀💾

