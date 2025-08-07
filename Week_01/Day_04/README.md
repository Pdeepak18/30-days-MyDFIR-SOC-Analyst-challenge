# 📊 Kibana Setup Tutorial | Day 4

---

## 🎯 Objective

Set up Kibana on your local VM and securely enroll it with your Elasticsearch instance.

---

## 🧰 Prerequisites

- Elasticsearch 9.1.1 already installed and running ✅
- Ubuntu Server 22.04
- Internet access
- `sudo` access

---

## 🔧 Installation Steps

### 1. 📦 Download Kibana

Go to: [Kibana Download Page](https://www.elastic.co/downloads/kibana)

Download the `.deb x86_64` version:

```bash
wget https://artifacts.elastic.co/downloads/kibana/kibana-9.1.1-amd64.deb
```

Install it:

```bash
sudo dpkg -i kibana-9.1.1-amd64.deb
```

**Output Sample:**

```
Setting up kibana (9.1.1) ...
Creating kibana group... OK
Creating kibana user... OK
Created Kibana keystore in /etc/kibana/kibana.keystore
```

---

### 2. ⚙️ Configure `kibana.yml`

Edit the config file:

```bash
sudo nano /etc/kibana/kibana.yml
```

Uncomment and update the following lines:

```yaml
server.port: 5601
server.host: "YOUR_VM_IP"
```

📌 Example:

```yaml
server.host: "172.31.0.4"
```

---

### 3. 🚀 Start Kibana

Run the following to enable and start Kibana:

```bash
sudo systemctl daemon-reexec
sudo systemctl enable kibana
sudo systemctl start kibana
sudo systemctl status kibana
```

You should see:

```
Active: active (running)
```

---

## 🔐 Secure Enrollment with Elasticsearch

### 4. 📤 Generate Enrollment Token

Switch to Elasticsearch bin directory:

```bash
cd /usr/share/elasticsearch/bin/
```

Generate the token:

```bash
sudo ./elasticsearch-create-enrollment-token --scope kibana
```

You'll get an output like this:

```
eyJ2ZXIiOiI4LjE0LjAiLCJhZHIiOlsiMTcyLjMxLjAuNDo5MjAwIl0sImZnciI6IjQ3NmUyOTUyMGZjZGYwM2Q3ODA4OGNmMjRhZjc4N2Y4ZDU3MmE0ZjZkMjFjZGE1NWQ4Y2M0NzdjMGU4ZmU1N2YiLCJrZXkiOiJiM19JaFpnQnFqN1ZHZldsRGpmVToxVDYtMHVJNDAwaHBoNmJ0SXdFdk5RIn0=
```

---

### 5. 🌐 Access Kibana

(First do the port forwarding for port 5601 in your virtualbox so that you can access the kibana at your local host)

> Go to: `VirtualBox > File > Tools > Network Manager > NAT Network > Port Forwarding`  
> Add
> | Setting | Value |
> |-------------|---------------|
> | Name | GUI (ELK) |
> | Protocol | TCP |
> | Host IP | 127.0.0.1 |
> | Host Port | 5602 |
> | Guest IP | 172.0.0.4 |(Your VM Ip)
> | Guest Port | 5601 |

Now
In your browser, visit:

```
http://YOUR_VM_IP:5601
```

Paste the **enrollment token** when prompted.

---

### 6. ✅ Enter Verification Code

Switch to Kibana bin directory:

```bash
cd /usr/share/kibana/bin/
```

Generate the code:

```bash
sudo ./kibana-verification-code
```

Example:

```
Your verification code is:  801 467
```

Enter this code in the browser prompt.

---

### 7. 🔐 Login to Kibana

Use the credentials you saved in **Day 3**:

- **Username**: `elastic`
- **Password**: (Remember from Day 3 setup we get the secet token paste it here)

---

## 🔐 Optional But Recommended: Add Encryption Keys

### 8. Generate Encryption Keys

Run:

```bash
./kibana-encryption-keys generate
```

Sample output:

```
xpack.encryptedSavedObjects.encryptionKey: 44142bc43bb5845d6c660ff9e8f6ea40
xpack.reporting.encryptionKey: 38316cb7c5e23df04697f194c36eb192
xpack.security.encryptionKey: 1fad53fff636937f3e7e4d3ffc5456ac
```

---

### 9. Add Keys to Kibana Keystore

Run each command and paste the keys:

```bash
./kibana-keystore add xpack.encryptedSavedObjects.encryptionKey
./kibana-keystore add xpack.reporting.encryptionKey
./kibana-keystore add xpack.security.encryptionKey
```

---

### 10. 🔁 Restart Kibana

```bash
sudo systemctl restart kibana
```

Check status:

```bash
sudo systemctl status kibana
```

---

## ✅ Final Notes

- Your Kibana is now securely connected to Elasticsearch
- Always store your enrollment tokens, passwords, and keys securely
- Encryption keys protect saved data and API integrations

---
