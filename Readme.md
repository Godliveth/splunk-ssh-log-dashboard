

# 🧠 Create Your First Splunk Dashboard

### 📅 Project Title

**Day 18 of #3DaysOfSOC – Splunk Dashboard for SSH Log Analysis**

---

## 🎯 Objective

As part of my SOC Analyst learning journey, I built my **first Splunk Dashboard** to visualize SSH activity logs.
The goal was to identify SSH login patterns, analyze authentication outcomes, and understand how to present security insights using Splunk visualizations.

---

## 🧰 Tools & Environment

* **Splunk Enterprise (Free Edition)**
* **Dataset:** `ssh_logs.txt` (synthetic SSH log data)
* **Index Name:** `ssh_index`
* **Visualization Type:** Dashboard Panels
* **SPL (Search Processing Language)**

---

## 🧩 Key Learning Outcomes

* How to **ingest and index log data** in Splunk
* How to **build SPL queries** for data analysis
* How to **visualize security metrics** using bar charts, single values, and tables
* How dashboards help analysts **spot trends and anomalies** in SSH activity

---

## 🛠️ Step-by-Step Implementation

### 🔹 Step 1: Upload the Dataset

1. Navigate to `Settings → Add Data → Upload`.
2. Upload `ssh_logs.txt`.
3. Set **Source Type:** `json`.
4. Create **Index:** `ssh_index`.
5. Launch **Search & Reporting** to query data.

---

### 📊 Step 2: Top Source IPs (Bar Chart)

**SPL Query:**

```spl
index=ssh_index
| stats count by id.orig_h
| rename id.orig_h as "Source IP"
| sort - count
```

* **Title:** Top Source IPs
* **Visualization:** Bar Chart

---

### 📊 Step 3: Top Destination IPs (Bar Chart)

**SPL Query:**

```spl
index=ssh_index
| stats count by id.resp_h
| rename id.resp_h as "Destination IP"
| sort - count
```

* **Title:** Top Destination IPs
* **Visualization:** Bar Chart

---

### 📈 Step 4: Failed SSH Logins (Single Value)

**SPL Query:**

```spl
index=ssh_index auth_success=false
| stats count as "Failed SSH Logins"
```

* **Title:** Total Failed SSH Logins
* **Visualization:** Single Value

---

### 📈 Step 5: Successful SSH Logins (Single Value)

**SPL Query:**

```spl
index=ssh_index auth_success=true
| stats count as "Successful SSH Logins"
```

* **Title:** Total Successful SSH Logins
* **Visualization:** Single Value

---

### 📋 Step 6: Source → Destination IP Mapping (Table)

**SPL Query:**

```spl
index=ssh_index
| stats count by id.orig_h, id.resp_h
| rename id.orig_h as "Source IP", id.resp_h as "Destination IP", count as "Total Connections"
| sort - "Total Connections"
```

* **Title:** Source to Destination IP Pairs
* **Visualization:** Table

---

## 📊 Final Dashboard Overview

| Panel                        | Visualization | Description                       |
| ---------------------------- | ------------- | --------------------------------- |
| Top Source IPs               | Bar Chart     | IPs initiating SSH connections    |
| Top Destination IPs          | Bar Chart     | Target hosts of SSH connections   |
| Failed SSH Logins            | Single Value  | Total number of failed attempts   |
| Successful SSH Logins        | Single Value  | Total number of successful logins |
| Source → Destination Mapping | Table         | Shows IP connection relationships |

---

## 🧠 SOC Insight

From this dashboard, I learned how **failed login spikes** could indicate **brute-force attempts** and how **source–destination relationships** can help track suspicious hosts.

It was a great introduction to how SOC teams use **SIEM dashboards** to monitor system activity and detect potential threats in real time.

---

## 📸 Screenshot

*(Insert your Splunk Dashboard screenshot here once completed.)*

---

## 🧩 Skills Demonstrated

* SIEM Configuration
* SPL Query Writing
* Log Analysis & Visualization
* SSH Authentication Monitoring
* Dashboard Building in Splunk

---

## 🏁 Conclusion

This project helped me understand how to convert **raw log data into actionable insights** — a critical skill for every SOC Analyst.
It’s my first step into **security visualization and real-time monitoring** using Splunk.

---

