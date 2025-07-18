This repository contains all the scripts, configuration and documentation needed to deploy T‑Pot honeypot on AWS EC2.  
We break the setup into **Phases**—this document covers **Phase 1: Launching the EC2 instance**.

---

## Phase 1: Launch an EC2 Instance

### Overview
In Phase 1 we:
1. Create and configure a new EC2 instance.
2. Choose a Debian 12 AMI.
3. Assign a key‐pair for SSH access.
4. Configure network and security group to allow SSH (port 22).

### Prerequisites
- AWS account with permissions to create EC2 instances, key pairs, and security groups.
- A local folder `images/` in this repo where you store your screenshots (e.g. `images/Screenshot1.png`, `images/Screenshot2.png`).

---

### Step 1: Name & AMI Selection

1. In the AWS console, navigate to **EC2 → Instances → Launch Instances**.  
2. Under **Name and tags**, set `Name = my_honeypot`.  
3. Under **Application and OS Images (AMIs)**, select the **Quick Start → Debian** tile and then **Debian 12 (HVM), SSD Volume Type**.  
4. Confirm the **Architecture** is set to **64‑bit (x86)** and note the **AMI ID**. 
   ![[Screenshot 1.png]]
   
   ---

### Step 2: Instance Type

1. Scroll to **Instance type**.  
2. Choose a free‑tier‑eligible (or small) instance, for example **t2.micro**.  
3. (Optional) If you expect heavy honeypot traffic or more containers later, you can select a larger instance (e.g. **t2.large**).

   > **Note:** Larger instances incur higher hourly costs.

---

### Step 3: Key Pair & SSH Access

1. Under **Key pair (login)**, either select an existing key‑pair or **Create a new key pair** named `tpot_honeypot_key`.  
2. **Download** the `.pem` file and store it securely—this will be used to SSH in.  

---

### Step 4: Network & Security Group

1. Under **Network settings**, ensure **Auto‑assign public IP** is **Enable** so you get a reachable Elastic IP.  
2. Create (or select) a **Security group** with at least:
   - **Type:** SSH  
   - **Protocol:** TCP  
   - **Port range:** 22  
   - **Source:** Your IP (CIDR), e.g. `203.0.113.45/32`  

   AWS will warn if you open SSH to `0.0.0.0/0`—we recommend restricting it to your workstation IP.![[Screenshot 2.png]]

---

### Step 5: Review & Launch

1. In the **Summary** panel, verify:
   - **AMI:** Debian 12  
   - **Instance type:** t2.micro (or chosen size)  
   - **Security group:** Allows SSH from your IP  
   - **Storage:** ≥ 50 GiB (to hold logs and Docker images)
2. Click **Launch instance**.

---

## Next

Once your EC2 instance is up:
- Note its **Public IPv4 address** (or Elastic IP).
- **SSH** in using:
  ```bash
  chmod 400 tpot_honeypot_key.pem
  ssh -i tpot_honeypot_key.pem admin@<YOUR_PUBLIC_IP>