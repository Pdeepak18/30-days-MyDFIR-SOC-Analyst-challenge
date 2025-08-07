🚀 Elasticsearch Setup Tutorial | Day 3
⚠️ Note:
This tutorial uses a local Ubuntu Server 22.04 VM (not a cloud platform) to provide real hands-on experience.
If you're new and want to install Elasticsearch on your local machine, follow this step-by-step guide.

🔗 Official Download Page – Elasticsearch
🎯 What You'll Learn
How to install Elasticsearch on Ubuntu Server

Basic configuration for local access

How to set up port forwarding to access VM services from your host machine

🧰 Requirements
Ubuntu Server 22.04 VM

VirtualBox installed on your system

Internet connection

Basic terminal knowledge

🌐 Understanding NAT and Port Forwarding (📦 Important Concept)
🧠 What is NAT?
NAT (Network Address Translation) hides your VM behind the host machine's IP address.
This allows the VM to access the internet, but blocks direct access from your host to the VM.

🔁 Why Do We Need Port Forwarding?
Since the VM is hidden behind NAT, you cannot directly access it from the host—for example, for SSH or accessing services like Elasticsearch.
Port forwarding solves this by mapping a port on the host to a port on the VM.

✅ Example: SSH Port Forwarding
Suppose your Ubuntu VM has the IP: 10.0.2.15 (default for NAT).
To SSH into the VM from your host:

🧭 Set Port Forwarding in VirtualBox:
Go to:

VirtualBox → File → Tools → Network Manager

Select your NAT Network → Click on Port Forwarding

Then add a rule like this:

Setting	Value
Name	ssh-connection
Protocol	TCP
Host IP	127.0.0.1
Host Port	2222
Guest IP	10.0.2.15
Guest Port	22

💻 Connect via Host Terminal:

ssh yourusername@127.0.0.1 -p 2222
🔐 This connects your host machine to the VM over SSH using the forwarded port.

🌐 Example: Elasticsearch Port Forwarding
Elasticsearch runs on port 9200 inside the VM.

To access it from your host, add another port forwarding rule:

Setting	Value
Name	elasticsearch
Protocol	TCP
Host IP	127.0.0.1
Host Port	9200
Guest IP	10.0.2.15
Guest Port	9200

Now you can access Elasticsearch in your browser or terminal:


curl -u elastic https://127.0.0.1:9200 --insecure
🔧 Installation Steps
🟢 Step 1: Download Elasticsearch
Visit: https://www.elastic.co/downloads/elasticsearch
Choose the "DEB x86_64" package, copy the link, and run:


wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-<version>-amd64.deb
📌 Replace <version> with the actual version number.

🟢 Step 2: Install Elasticsearch

sudo dpkg -i elasticsearch-<version>-amd64.deb

🔐 During installation:

A superuser password will be generated.

Copy and save all info shown on the screen.

🟢 Step 3: Configure Elasticsearch
Edit the configuration file:


sudo nano /etc/elasticsearch/elasticsearch.yml
Uncomment and modify the following lines:


network.host: 0.0.0.0
http.port: 9200

📌 Setting network.host: 0.0.0.0 allows connections from all network interfaces, including port-forwarded access from the host.

🟢 Step 4: Start the Elasticsearch Service
Run the following commands:


sudo systemctl daemon-reexec
sudo systemctl enable elasticsearch
sudo systemctl start elasticsearch
sudo systemctl status elasticsearch

✅ You should see the status: active (running)

🧪 Test the Setup
From your host machine (outside the VM), run:


curl -u elastic https://127.0.0.1:9200 --insecure

Enter the password that was generated during installation.
You should receive a JSON response from Elasticsearch.

📌 Tips
Save your elastic superuser password and enrollment token securely.

If Elasticsearch fails to start, check logs with:

sudo journalctl -u elasticsearch
Double-check that port 9200 is forwarded correctly in VirtualBox settings.