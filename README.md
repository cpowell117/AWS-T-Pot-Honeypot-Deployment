# AWS-T-Pot-Honeypot-Deployment

A minimal guide to deploy T‑Pot on AWS EC2.

---

## Prerequisites

- AWS account (EC2, Security Groups, Key Pairs)  
- SSH client & Git installed locally  

---

## 1. Launch EC2 Instance
1. **AMI:** Debian 12 (HVM), SSD  
2. **Instance:** t2.micro (free‑tier)  
3. **Key Pair:** create/download `tpot_key.pem`  
4. **Security Group:** allow SSH (port 22) from your IP only  

---

## 2. SSH & Prepare
chmod 400 tpot_key.pem
ssh -i tpot_key.pem admin@<PUBLIC_IP>

- Fix locale:
sudo apt update
sudo apt install -y locales
sudo locale-gen en_US.UTF-8
sudo dpkg-reconfigure locales

- Install deps:
sudo apt upgrade -y
sudo apt install -y docker.io docker-compose git ufw

## 3. Install T‑Pot
git clone https://github.com/telekom-security/tpotce.git
cd tpotce
sudo ./install.sh

Wait for “Installation complete.”

## 4. Secure & Access
- Reboot & Proxy SSH:
sudo reboot
ssh -i tpot_key.pem -p 64295 admin@<PUBLIC_IP>

- Lock SG: allow only ports 64295, 64297, 64298 from your IP.
- Dashboards:
    - Kibana: http://<PUBLIC_IP>:64297
    - Cowrie UI: http://<PUBLIC_IP>:64298
