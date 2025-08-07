# 🚀 Elasticsearch Setup Tutorial | Day 3

⚠️ **Note:** We're using a local Ubuntu Server 22.04 VM (not cloud) to get better hands-on experience.  
If you're new and want to install Elasticsearch locally, follow this step-by-step guide.

🔗 [Official Download Page – Elasticsearch](https://www.elastic.co/downloads/elasticsearch)

---

## 🎯 What You'll Learn

- Install Elasticsearch on Ubuntu Server  
- Basic configuration for local access  
- How to use port forwarding to access VM services from your host machine  

---

## 🧰 Requirements

- Ubuntu Server 22.04 VM  
- VirtualBox installed on your system  
- Internet connection  
- Basic terminal knowledge  

---

## 🌐 Understanding NAT and Port Forwarding

### 🧠 What is NAT?

NAT (Network Address Translation) hides the VM behind your host machine.  
Your VM can access the internet, but external systems (like your host) can't directly access the VM.

### 🔁 Why Do We Need Port Forwarding?

Since the VM is hidden behind NAT, you can’t directly access it from the host machine (like for SSH or Elasticsearch access).  
So, **Port Forwarding** helps us forward specific traffic from the host to the VM.

### ✅ Example: SSH Port Forwarding

Let’s say:

- Ubuntu Server VM IP (NAT): `10.0.2.15`  
- You want to SSH from your host to the VM

**Port Forwarding Setup in VirtualBox:**  

> Go to: `VirtualBox > File > Tools > Network Manager > NAT Network > Port Forwarding`  

| Setting     | Value         |
|-------------|---------------|
| Name        | ssh-connection |
| Protocol    | TCP           |
| Host IP     | 127.0.0.1     |
| Host Port   | 2222          |
| Guest IP    | 10.0.2.15     |
| Guest Port  | 22            |

**Now Connect via Host Terminal:**

```bash
ssh yourusername@127.0.0.1 -p 2222
```

🔐 This connects your local machine (host) to the VM over SSH using the forwarded port.

---

### 🌐 Example: Elasticsearch Port Forwarding

Elasticsearch by default runs on port `9200` inside the VM.

**Add Another Port Forward Rule:**

| Setting     | Value         |
|-------------|---------------|
| Name        | elasticsearch |
| Protocol    | TCP           |
| Host IP     | 127.0.0.1     |
| Host Port   | 9200          |
| Guest IP    | 10.0.2.15     |
| Guest Port  | 9200          |

**Now Access From Host:**

```bash
curl -u elastic https://127.0.0.1:9200 --insecure
```

---

## 🔧 Installation Steps

### 🟢 Step 1: Download Elasticsearch

Go to: [https://www.elastic.co/downloads/elasticsearch](https://www.elastic.co/downloads/elasticsearch)  
Choose the **"DEB x86_64"** package. Copy the link and run:

```bash
wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-<version>-amd64.deb
```

📌 Replace `<version>` with the actual version number

---

### 🟢 Step 2: Install Elasticsearch

```bash
sudo dpkg -i elasticsearch-<version>-amd64.deb
```

🔐 During installation:  
A superuser password will be generated. Copy and save all info shown on screen.

---

### 🟢 Step 3: Configure Elasticsearch

Edit the config file:

```bash
sudo nano /etc/elasticsearch/elasticsearch.yml
```

Uncomment and set the following values:

```yaml
network.host: 0.0.0.0
http.port: 9200
```

`0.0.0.0` allows connections from all interfaces (including port-forwarded access).

---

### 🟢 Step 4: Start the Elasticsearch Service

```bash
sudo systemctl daemon-reexec
sudo systemctl enable elasticsearch
sudo systemctl start elasticsearch
sudo systemctl status elasticsearch
```

✅ You should see: `active (running)`

---

## 🧪 Test the Setup

From your **host machine** (outside the VM):

```bash
curl -u elastic https://127.0.0.1:9200 --insecure
```

🔐 Enter the password generated during install. You should see a JSON response from the Elasticsearch node.

---

## 📌 Tips

- Keep your elastic superuser password and enrollment token saved.  
- Use `sudo journalctl -u elasticsearch` to check logs if it fails to start.  
- Ensure port `9200` is forwarded correctly in VirtualBox.