# AWS Security Hardening

This document provides additional best practices and security measures you can implement to strengthen your AWS VPC and EC2 environment.

## 1. SSH Hardening
- **Disable password authentication** in `/etc/ssh/sshd_config`.
- Use **key-based authentication** only.
- Restrict SSH access to specific IP addresses.

## 2. IAM Best Practices
- Use **IAM Roles** for EC2 to avoid storing long-term credentials.
- Enforce **MFA** for all IAM users with console access.
- Assign permissions based on **least privilege**.

## 3. Logging and Monitoring
- **Enable CloudTrail** to track API calls.
- Use **CloudWatch Logs** and **GuardDuty** to detect suspicious activity.
- Consider enabling **VPC Flow Logs** to monitor traffic within the VPC.

## 4. Patch Management
- Keep EC2 instances updated with **security patches**.
- Consider using **AWS Systems Manager** Patch Manager.

## 5. Network Segmentation
- Separate subnets for **public** and **private** workloads.
- Use **Network ACLs** to further restrict traffic if needed.

## 6. Further Reading
- [AWS Security Best Practices](https://docs.aws.amazon.com/general/latest/gr/aws-security-best-practices.html)
- [AWS Well-Architected Framework - Security Pillar](https://docs.aws.amazon.com/wellarchitected/latest/security-pillar/welcome.html)
