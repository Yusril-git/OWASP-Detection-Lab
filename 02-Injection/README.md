# 🛡️ A03: Injection - SQL Injection (SQLMap)

Dokumentasi ini menunjukkan simulasi serangan **SQL Injection** menggunakan alat otomatis **SQLMap** dan bagaimana **Wazuh SIEM** mendeteksi aktivitas tersebut melalui analisis log Apache secara real-time.

---

## 📋 Ringkasan Lab
* **Objektif**: Mendeteksi percobaan eksploitasi database pada aplikasi web (DVWA).
* **Metode Serangan**: Automated SQL Injection (UNION Based).
* **Target**: DVWA (Damn Vulnerable Web Application) - Security Level: Low.

## 🛠️ Arsitektur Lab
* **Attacker (Kali Linux)**: `192.168.15.138`
* **Victim (Ubuntu Server)**: `192.168.15.139` (Wazuh Agent)
* **SIEM (Wazuh Manager)**: `192.168.15.140`



## ⚔️ Simulasi Serangan (Step-by-Step)

### 1. Eksekusi di Kali Linux
Serangan dilakukan dengan menyertakan Cookie sesi (PHPSESSID) agar SQLMap bisa melewati halaman login dan langsung menguji parameter `id` pada modul SQL Injection.

```bash
sqlmap -u "[http://192.168.15.139/dvwa/vulnerabilities/sqli/?id=1&Submit=Submit](http://192.168.15.139/dvwa/vulnerabilities/sqli/?id=1&Submit=Submit)" --cookie="security=low; PHPSESSID=vhdaet9nouc2sf95tpn89p7c9t" --dbs

```

**Bukti Eksekusi Terminal:**

### 2. Analisis Payload (Apache Logs)

Pada sisi server, SQLMap mengirimkan ribuan permintaan dengan *payload* berbahaya untuk mengidentifikasi struktur database. Wazuh Agent menangkap User-Agent `sqlmap` pada setiap permintaan tersebut.

**Tampilan Log Apache:**

---

## 🛡️ Strategi Deteksi (Wazuh Configuration)

### Custom Rule Implementation

Saya menerapkan *custom rule* (ID: 100003) pada Wazuh Manager untuk memantau log akses web secara spesifik terhadap identitas alat SQLMap.

```xml
<rule id="100003" level="10">
  <if_sid>31100,31101,31108</if_sid>
  <regex type="pcre2">(?i)sqlmap</regex>
  <description>Waspada! Aktivitas SQL Injection (SQLMap) Terdeteksi!</description>
  <mitre>
    <id>T1190</id>
  </mitre>
</rule>

```

---

## 📊 Hasil Analisis di Wazuh Dashboard

Wazuh berhasil memicu alert **Level 10** secara masif ketika serangan berlangsung, memberikan visibilitas penuh kepada SOC Analyst mengenai lonjakan aktivitas mencurigakan.

---

*Created by Envy - IT Student & Cybersecurity Enthusiast*

```

