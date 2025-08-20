# Windows Server 2022 Installation & RDP Setup | Day 5  

## 🎯 Objective  
Set up **Windows Server 2022 inside VirtualBox** and enable **Remote Desktop Protocol (RDP)** for remote access.  
This is useful for practicing Windows administration and later forwarding logs to your SOC lab (Ubuntu servers).  

---

## 📝 Task Summary  
- Install Windows Server 2022 on VirtualBox  
- Enable and configure Remote Desktop (RDP)  
- Set up port forwarding in VirtualBox to connect from the host machine  
- (Optional & risky) Expose RDP to the internet  

---

## 🖥️ Step 1: Install Windows Server 2022  
1. Download the ISO from the official Microsoft site (evaluation copy is free).  
2. Create a new VM in VirtualBox:  
   - **Type:** Microsoft Windows  
   - **Version:** Windows 2022 (64-bit)  
   - **Memory:** 4 GB minimum  
   - **Disk:** 50 GB (dynamically allocated)  
3. Boot with the ISO and follow the installer steps.  

---

## 🔑 Step 2: Enable RDP on Windows Server  
1. Log in to the server with an administrator account.  
2. Open **Server Manager → Local Server**.  
3. Find **Remote Desktop → Disabled → Enable it**.  
4. Allow RDP through **Windows Defender Firewall**.  

---

## 🌐 Step 3: Configure Port Forwarding in VirtualBox  

We are separating this Windows Server from the SOC Ubuntu NAT network.  

👉 **Why?**  
If someone gains access to this Windows Server and it’s in the same NAT Network, they could perform **lateral movement** and compromise your SOC machines.  
For better security practice, we isolate this server and use **NAT with Port Forwarding** instead.  

---

### 🔹 Option 1: NAT (Recommended for Isolation)  

1. Open VirtualBox → Select your **Windows Server VM**.  
2. Go to **Settings → Network**.  
3. Make sure **Adapter 1 is attached to NAT (⚠️ not NAT Network)**.  
4. Click **Advanced → Port Forwarding**.  
5. Add a new rule:  

| Setting   | Value     |
|-----------|-----------|
| Name      | rdp-access |
| Protocol  | TCP       |
| Host IP   | 127.0.0.1 |
| Host Port | 3389      |
| Guest IP  | 10.0.2.15 |
| Guest Port| 3389      |

This forwards RDP traffic from your **host machine** to the **Windows Server VM**.  

---

### 🔹 Option 2: NAT Network (If you want it to talk to other SOC VMs)  

1. Go to **VirtualBox → File → Tools → Network Manager → NAT Network → Port Forwarding**.  
2. Add a new rule:  

| Setting   | Value         |
|-----------|---------------|
| Name      | rdp-win-server |
| Protocol  | TCP           |
| Host IP   | 127.0.0.1     |
| Host Port | 3339          |
| Guest IP  | 172.31.0.10   | (replace with your VM’s NAT Network IP) |
| Guest Port| 3389          |

This lets you access the Windows Server while it’s part of the **same NAT Network** as your SOC lab.  

---

## 🖧 Step 4: Connect via RDP  

From your **host machine**:  

```powershell
mstsc /v:127.0.0.1:3389   # If using Option 1 (NAT)
mstsc /v:127.0.0.1:3339   # If using Option 2 (NAT Network)
```

✅ You now have Windows Server 2022 accessible via RDP either in isolation or as part of your SOC NAT network(in which our all other VM's Are there).  
