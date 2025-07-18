In Phase 5 we’ll:

1. Lock down your AWS Security Group to exactly the ports you need.  
2. SSH back in on the proxied port 64295 to confirm access.  
3. Finalize documentation of the security rules.

---

### Step 1: Edit AWS Security Group Inbound Rules

In the AWS console, navigate to **EC2 → Security Groups → [your honeypot SG] → Edit inbound rules**. Replace any wide‐open rules with these three:

| Type        | Protocol | Port range | Source         | Description                      |
|-------------|----------|------------|----------------|----------------------------------|
| Custom TCP  | TCP      | 64295      | My IP (×/32)   | SSH via T‑Pot proxy              |
| Custom TCP  | TCP      | 64297      | My IP (×/32)   | Kibana dashboard                 |
| Custom TCP  | TCP      | 64298      | My IP (×/32)   | Cowrie web interface (honeypot)  |

> **Note:** Remove any “0.0.0.0/0” rules to avoid exposing SSH or dashboards to the world.  


Click **Save rules**.

---

### Step 2: SSH via the T‑Pot SSH Proxy

With your Security Group updated, confirm you can still SSH in on the proxy port:

```bash
ssh -i tpot_honeypot_key.pem -p 64295 admin@<YOUR_PUBLIC_IP>
```

