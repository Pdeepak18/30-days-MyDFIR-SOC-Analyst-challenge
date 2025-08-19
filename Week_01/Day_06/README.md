# 🚀 Elastic Agent & Fleet Server | Day 6

## 🎯 Objective
Today we’ll learn what **Elastic Agent** and **Fleet Server** are, why they exist, and how they fit into the **Elastic Stack**.  
These two components make it much easier to collect, manage, and monitor data across multiple machines.

---

## 📦 What is Elastic Agent?
The **Elastic Agent** is a single agent that you install on servers, endpoints, or containers to collect:
- 📄 Logs (system logs, app logs, etc.)
- 📊 Metrics (CPU, memory, disk, network)
- 🛡️ Security data (endpoint protection, malware detection)

👉 Before Elastic Agent existed, you had to install multiple **Beats** (Filebeat, Metricbeat, etc.) for different purposes.  
Now, **one agent does it all**, reducing complexity.

---

## ⚙️ Deployment Modes

Elastic Agent can run in two ways:

### 1️⃣ Managed Mode (via Fleet) ✅ *Recommended*
- Managed centrally in **Kibana → Fleet UI**
- You create **policies** in Kibana, and all connected agents receive the same settings automatically
- Benefits:
  - Centralized updates
  - Easier scaling across 100s of machines
  - Monitoring of agent health from one place

### 2️⃣ Standalone Mode
- No Fleet Server needed
- Configuration is done manually using local **YAML files**
- Benefits:
  - More control for small setups
- Downsides:
  - Harder to manage if you have many agents

---

## 🔄 Beats vs Elastic Agent (Quick View)

| Feature | Beats (Old) | Elastic Agent (New) |
|---------|-------------|----------------------|
| Install | One Beat per use case (Filebeat, Metricbeat, etc.) | One agent for all |
| Config  | Manual config per Beat | Centralized via Fleet |
| Security | Not built-in | Includes endpoint protection |
| Scaling | Harder, lots of configs | Easier, policies managed centrally |

---

## 🌐 What is Fleet Server?

The **Fleet Server** is the “traffic controller” for Elastic Agents.  
Think of it as a **middleman** between:
- Kibana’s **Fleet UI** (management console)  
- All the Elastic Agents running on your systems  

### Fleet Server does:
- 📦 Distributes **policies** and updates to Elastic Agents
- 📡 Collects agent status & monitoring data
- 🔑 Helps onboard new agents securely

👉 Without Fleet Server, Elastic Agents can still run (Standalone mode), but you lose centralized management.

---

## ✅ Why It Matters

- 🔗 **One agent** for everything → less complexity
- 🧑‍💻 **Centralized management** → easy at scale
- 🛡️ **Built-in endpoint security** → protects your systems
- 📊 **Better visibility** → know which agents are healthy or failing
- 🚀 **Future-proof** → Elastic is moving from Beats → Elastic Agent

---

## 🧠 Simple Analogy

- **Elastic Agent** = Employee (installed on each computer, does the work)  
- **Fleet Server** = Manager (gives instructions, checks progress, reports to Kibana)  
- **Kibana Fleet UI** = Head Office (where you define company rules/policies)  

---

