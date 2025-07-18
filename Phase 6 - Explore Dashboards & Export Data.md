In Phase 6 we’ll:

1. Open the T‑Pot landing page and explore key dashboards.  
2. Verify incoming honeypot traffic on the Attack Map and Cowrie logs.  
3. Use Kibana and Cyberchef to analyze and export data.  
4. Capture screenshots and commit your findings.

---

### Step 1: Open the T‑Pot Landing Page

Browse to:

https://<YOUR_PUBLIC_IP>:64297


You’ll see the T‑Pot home screen with navigation tiles:

![[Screenshot 10.png]]

> **Tiles explained:**  
> - **Attack Map**: Real‑time global plot of incoming connections.  
> - **Cyberchef**: “Recipe”‑style tool to decode and analyze payloads.  
> - **Elasticvue**: Lightweight Elastic Stack index browser.  
> - **Kibana**: Full Elastic Stack dashboards (Attack Map, Cowrie, Dionaea, etc.).  
> - **Spiderfoot**: Automated threat‑intel and profiling.  
> - **SecurityMeter**: Status overview of your honeypot.  
> - **T‑Pot ReadMe**: Official docs.  
> - **T‑Pot @ GitHub**: Source repository.

---

### Step 2: Verify Incoming Traffic

1. **Attack Map**  
   - Click **Attack Map** → watch plotted dots and lines appear as IPs scan your honeypot in real time.  
   

2. **Cowrie Dashboard (via Kibana)**  
   - From the home screen, click **Kibana** → Login (no creds by default).  
   - Navigate to **Dashboards → Cowrie**.  
   - View lists of login attempts, successful shells, and extracted credentials.  
   

---

### Step 3: Analyze & Export Logs

1. **Use Kibana Discover**  
   - In **Discover**, select the `cowrie-*` index pattern.  
   - Apply a time filter “Last 24 hours.”  
   - Search for a sample field, e.g. `eventid: cowrie.login.success`.  
   - Click **Share → CSV Reports → Generate CSV** to download recent successful logins.  

2. **Cyberchef**  
   - Copy a base64‑encoded payload from Cowrie logs.  
   - Click **Cyberchef**, paste it in the “Input” pane.  
   - Add a “From Base64” operation → view decoded contents.  
   
