In Phase 3 we’ll:

1. Update and upgrade the OS packages.  
2. Clone the T‑Pot repository.  
3. Run the `install.sh` playbook.  
4. Verify the T‑Pot containers are up and healthy.

---

### Step 1: Update & Upgrade

Before pulling the latest playbook, refresh your package lists and apply outstanding upgrades:

```bash
sudo apt update
sudo apt upgrade -y
```

---

### Step 2: Clone the T‑Pot Installer

```bash
git clone https://github.com/telekom-security/tpotce.git cd tpotce
```

- This fetches the official T‑Pot CE playbook and configurations.


---

### Step 3: Run the Installer

```bash
sudo ./install.sh
```

- You’ll be prompted to confirm defaults (network interface, single‑host mode, Docker setup).

- The script downloads and configures all honeypot modules (Cowrie, Dionaea, Elastic Stack, etc.).


---

### Step 4: Verify Containers & Services

Once the installer finishes:

```bash
docker ps
```

- Look for containers such as `cowrie`, `dionaea`, `elasticsearch`, `kibana`, `tpotproxy`, etc.

- Each should show `STATUS: Up (healthy)`.

