# Day 2 - ELK Stack Introduction

## 📦 What is the ELK Stack?

**ELK** stands for:

- **E**lasticsearch – The **search engine** and **database** where logs are stored and indexed.
- **L**ogstash – A **data collector** that gathers, filters, and sends data to Elasticsearch.
- **K**ibana – A **dashboard and visualization** tool to search, analyze, and display data from Elasticsearch.

✅ Together, they help collect, store, search, and visualize logs — very useful for security monitoring, troubleshooting, and analytics.

---

## 🎯 Objective

Understand how each ELK component works and how they help with log collection and security monitoring (like a SIEM).

---

## ⚙️ ELK Stack Components (In Detail)

### 🔍 Elasticsearch
- Acts like a **searchable database** for logs.
- Can store **millions of log entries** and retrieve them fast.
- Uses **ES|QL** (Elasticsearch Query Language) to find and analyze data.

### 🔄 Logstash
- Works like a **data pipeline**.
- Collects logs from servers, applications, and devices.
- Can **filter**, **transform**, and **clean data** before sending it to Elasticsearch.

### 📊 Kibana
- Provides a **web interface** to view and explore data.
- You can:
  - Search logs easily.
  - Create **dashboards**, **alerts**, and **reports**.
  - Monitor activity in real-time.

---

## 🛰️ Beats – Lightweight Data Shippers

**Beats** are small agents that send specific types of data to Logstash or Elasticsearch.

| Beat Type     | What It Does                         |
|---------------|--------------------------------------|
| **Filebeat**   | Collects log files (e.g., syslog, Apache logs) |
| **Metricbeat** | Sends system metrics (CPU, memory, disk)     |
| **Packetbeat** | Captures network traffic              |
| **Winlogbeat** | Collects Windows Event Logs           |
| **Auditbeat**  | Tracks user actions on Linux systems  |
| **Heartbeat**  | Checks if services are alive/up       |

✅ **Elastic Agent** – A newer, all-in-one agent that replaces individual Beats.

---

## 🔁 ELK Stack vs. Splunk (Quick Comparison)

| ELK Component      | Similar in Splunk         | Purpose                         |
|--------------------|---------------------------|----------------------------------|
| Elasticsearch      | Indexer/Search Head       | Stores and searches data         |
| Logstash           | Heavy Forwarder           | Preprocesses and sends data      |
| Kibana             | Web UI                    | Visual interface for dashboards  |
| Beats/Elastic Agent| Universal Forwarder       | Sends logs from devices/systems  |

---

## ✅ Why Use ELK Stack?

1. **Centralized Logging** – All your logs in one place
2. **Custom Parsing** – Handle any data format your way
3. **Real-Time Visualization** – Spot trends, attacks, or errors fast
4. **Scalability** – Works for small labs or large enterprises
5. **Free & Open Source** – No license costs, highly flexible

---
## 📚 References & Learning Resources

https://tryhackme.com/room/investigatingwithelk101
https://www.elastic.co/elastic-stack/features
