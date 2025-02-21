# Troubleshooting Common Issues

This document covers typical problems that can arise when setting up and managing a secure AWS VPC environment with a Bastion Host and private EC2 instances.

---

## 1. SSH Connection Timeout
**Symptom**: You run `ssh -i key.pem ubuntu@<Public-EC2-or-Elastic-IP>` and it times out.
- **Security Group**: Port 22 must be open (inbound) from your IP to the Bastion Host’s Security Group.
- **Elastic IP**: Double-check if you’re using the correct Elastic IP address if one is allocated.
- **Key Permissions**: Ensure your `.pem` file has proper permissions (`chmod 400 key.pem`).
- **Route Table**: The public subnet route table should point `0.0.0.0/0` to the Internet Gateway.

## 2. Cannot SSH from Bastion to Private EC2
**Symptom**: You can connect to the Bastion, but `ssh -i key.pem ubuntu@<Private-IP>` fails.
- **Security Group Rules**: The Private EC2 SG must allow SSH inbound from the Bastion’s SG or private IP.
- **Key Pair**: Confirm you’re using the correct key pair for the Private EC2 instance.
- **Subnet**: The Private EC2 must be in the same VPC and subnet range that the Bastion can reach.

## 3. No Internet from Private EC2
**Symptom**: Your Private EC2 cannot reach external services (e.g., `apt-get update` fails).
- **NAT Gateway**: A NAT Gateway in a public subnet is required for outbound internet from a private subnet (unless you’re routing traffic via the Bastion).
- **Route Table**: The private subnet route table should direct `0.0.0.0/0` to the NAT Gateway.
- **DNS**: Ensure DNS is enabled in the VPC. Check `/etc/resolv.conf` or the instance’s DNS settings.

## 4. Elastic IP Issues
**Symptom**: Elastic IP is allocated but not working as expected.
- **Association**: Make sure the Elastic IP is associated with the correct EC2 instance or network interface.
- **Release/Reallocate**: If the IP is still causing conflicts, you might release and reallocate it in the same region.

## 5. Instances Not Starting
**Symptom**: EC2 instance status is “stuck” or errors occur on launch.
- **AWS Limits**: Check if you have reached your instance or IP limits in that region.
- **AMI Availability**: Certain instance types and AMIs may not be available in every AZ or region.

---

## Further Resources
- [AWS Knowledge Center](https://aws.amazon.com/premiumsupport/knowledge-center/)
- [AWS Forums](https://forums.aws.amazon.com/)
- [AWS Documentation](https://docs.aws.amazon.com/)
