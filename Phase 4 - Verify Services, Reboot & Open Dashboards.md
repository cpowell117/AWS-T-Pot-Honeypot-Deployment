In Phase 4 we’ll:

1. Review the installer’s final output and port assignments.  
2. Reboot the instance so all containers start on their new ports.  
3. SSH back in on the T‑Pot SSH proxy port (64295).  
4. Open your honeypot dashboards in the browser.  
5. Lock down UFW to only allow the ports you need.

---

### Step 1: Review Installer Output

After `sudo ./install.sh` completes, you should see each honeypot container pulled and a list of listening ports:

```text
✔ sentrypeer  Pulled    42.6s
✔ tanner_api  Pulled    69.4s
…
✔ cowrie      Pulled    56.2s
✔ miniprint   Pulled     6.6s

### Please review for possible honeypot port conflicts.
### While SSH is taken care of, other services such as
### SMTP, HTTP, etc. might prevent T‑Pot from starting.

Active Internet connections (only servers)
Proto Recv‑Q Send‑Q Local Address     Foreign Address State  PID/Program name
tcp   0      0      0.0.0.0:64295     0.0.0.0:*       LISTEN 4836/sshd: /usr/sbi
tcp   0      0      0.0.0.0:64297     0.0.0.0:*       LISTEN …/kibana
tcp   0      0      0.0.0.0:64298     0.0.0.0:*       LISTEN …/cowrie
…
### Done. Please reboot and re‑connect via SSH on tcp/64295.
```


---

### Step 2: Reboot & SSH on Port 64295

Reboot the VM so that all Docker containers and the SSH proxy bind correctly:

```bash
sudo reboot
```

Once it’s back up, SSH in on port 64295 instead of 22:

```bash
ssh -i tpot_honeypot_key.pem -p 64295 admin@<YOUR_PUBLIC_IP>
```


---

### Step 3: Open Your Dashboards

- **Kibana (All dashboards):**  
    `http://<YOUR_PUBLIC_IP>:64297`
    
- **Cowrie Web UI:**  
    `http://<YOUR_PUBLIC_IP>:64298`
    

You should now see real‑time logs, the attack map, and individual honeypot feeds.

![[Screenshot 6.png]]![[Screenshot 7.png]]
