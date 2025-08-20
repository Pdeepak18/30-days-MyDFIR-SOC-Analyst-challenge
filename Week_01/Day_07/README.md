# 🚀 Elastic Agent and Fleet Server Setup Tutorial | Day 7

## 🎯 Objective

- Install the **Elastic Agent** on a **WinEndpoint-01 (Windows Server 2022 VM)**
- Enroll **WinEndpoint-01** into the **Fleet Server** for centralized management

---

## 🛠️ Setup Overview

We will:

- Set up a **Fleet Server** on an Ubuntu VM
- Enroll a **Windows Server 2022 VM (WinEndpoint-01)** using Elastic Agent
- Manage all configurations through the **Fleet UI in Kibana**

---

## 📌 Prerequisites

- ✅ Elasticsearch and Kibana already installed and running
- ✅ Ubuntu VM to act as the **Fleet Server**
- ✅ Windows Server 2022 VM (`WinEndpoint-01`) with RDP access
- ✅ Internet access **or port forwarding** configured so `WinEndpoint-01` can reach the Fleet Server

---

## 🔧 Step-by-Step Instructions

### 🖥️ Step 1: Set Up Fleet Server on Ubuntu

1. SSH into your **Ubuntu VM**
2. Open a browser and visit:

```text
http://<your-elasticsearch-vm-ip>:5601
```

3. Navigate to:

```
Management → Fleet → Add Fleet Server
```

4. Under **Quick Start**, provide:

```
Fleet Server name: <any-name>
Fleet Server host URL: https://<fleet-server-ip>:8220
```

👉 Use the IP address of your Ubuntu VM as `<fleet-server-ip>` (example: `172.31.0.6`)

---

### 🧾 Step 2: Install Fleet Server on Ubuntu

1. Copy the **Linux command** generated in the Fleet UI
2. Paste it into your **Ubuntu Fleet VM** terminal
3. When prompted, type `Y` to confirm and install the **Elastic Agent**

✅ This turns your Ubuntu machine into a Fleet Server and connects it to Kibana.

---

### 🪟 Step 3: Enroll WinEndpoint-01 into Fleet

1. Go back to **Kibana UI → Fleet → Agents**
2. Click **Add agent**
3. Create or select a **Custom Agent Policy** (e.g., `Windows Monitoring Policy`)
4. Copy the **Windows command** shown in Kibana
5. On **WinEndpoint-01 (Windows Server 2022 VM)**:
   - Open **PowerShell as Administrator**
   - Paste the command and run it
   - Confirm installation by typing `Y` when prompted

✅ This installs the Elastic Agent and enrolls **WinEndpoint-01** into the Fleet UI.

---

## ✅ Post-Setup Verification

- Go back to **Fleet → Agents** in Kibana
- **WinEndpoint-01** should show as **online**
- It should be assigned to your custom policy

---

## 📌 Summary

| Component      | Action                                  |
| -------------- | --------------------------------------- |
| Ubuntu VM      | Acts as Fleet Server                    |
| Kibana UI      | Used for agent enrollment               |
| WinEndpoint-01 | Enrolled into Fleet using Elastic Agent |
| Fleet          | Centralized policy & data control       |

---

## 📚 Additional Tips

- Use **HTTPS with valid certs** in production
- Keep `WinEndpoint-01` **isolated** when practicing (better security)
- Monitor agent logs at:
  - Windows: `C:\Program Files\Elastic\Agent\data\elastic-agent.log`
  - Linux: `/opt/Elastic/Agent/data/elastic-agent.log`
- Later, add integrations (Windows Event Logs, Sysmon, Security events) in Kibana
