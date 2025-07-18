In Phase 2 we’ll:

1. SSH into the new EC2 instance.  
2. Resolve the locale warning so Ansible and apt work correctly.  
3. Install Docker, Docker Compose, Git and UFW.

---

### Step 1: SSH into Your Instance

````bash
chmod 400 tpot_honeypot_key.pem
ssh -i tpot_honeypot_key.pem admin@<YOUR_PUBLIC_IP>
````

### Step 2: Generate & Configure UTF‑8 Locale

1. **Install the locales package** (if not already present):

```bash
sudo apt update 
sudo apt install -y locales
````

2. **Generate `en_US.UTF-8`** and make it the default:

```bash
sudo locale-gen en_US.UTF-8 
sudo dpkg-reconfigure locales
 ````


- In the interactive menu, **space‑select** `en_US.UTF-8 UTF‑8`, then choose it as **Default locale**.

![[Screenshot 3.png]]
### Step 3: Update & Upgrade the System

```bash
sudo apt update && sudo apt upgrade -y
```


### Step 4: Install Docker, Docker Compose, Git & UFW

```bash
sudo apt install -y docker.io docker-compose git ufw
```
- **Docker** will run our T‑Pot containers.
- **UFW** (Uncomplicated Firewall) will let us lock down ports later.

![[Screenshot 4.png]]
![[Screenshot 5.png]]
