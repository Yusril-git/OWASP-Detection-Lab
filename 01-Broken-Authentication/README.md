# 🛡️ A01: Broken Authentication - Deteksi Serangan Brute Force dengan Hydra

[![Wazuh](https://img.shields.io/badge/SIEM-Wazuh-005571?style=flat&logo=wazuh&logoColor=white)](https://wazuh.com/)
[![OWASP Top 10](https://img.shields.io/badge/OWASP%20Top%2010-Broken%20Authentication-red)](https://owasp.org/Top10/A01_2021-Broken_Access_Control/)
[![MITRE ATT&CK](https://img.shields.io/badge/MITRE%20ATT%26CK-T1110%20(Brute%20Force)-purple)](https://attack.mitre.org/techniques/T1110/)

## 📋 Ringkasan Proyek

Dokumentasi ini menunjukkan keberhasilan implementasi **Wazuh SIEM** untuk mendeteksi serangan **Brute Force** secara real-time pada lingkungan lab cybersecurity. Serangan ini termasuk dalam kategori **A01: Broken Authentication** pada OWASP Top 10.

## 🛠️ Arsitektur Lab

* **Attacker**: Kali Linux (IP: 192.168.15.138)
* **SIEM Manager**: Wazuh Manager (Ubuntu 22.04)
* **Target/Agent**: Ubuntu Server 22.04 dengan Apache2 & DVWA (IP: 192.168.15.139)

## ⚙️ Konfigurasi Deteksi (Wazuh Rule)

Saya membuat *custom rule* pada file `/var/ossec/etc/rules/local_rules.xml` di Wazuh Manager. Rule ini menggunakan **Regex Case-Insensitive** untuk menangkap identitas Hydra pada *User-Agent* di log akses Apache.

> **📁 Lokasi file rule**: [`../rules/local_rules.xml`](../rules/local_rules.xml)

### Custom Rule (ID: 100002)

```xml
<rule id="100002" level="10">
  <if_sid>31100,31101,31108</if_sid>
  <regex type="pcre2">(?i)hydra</regex>
  <description>🚨 [A01: Broken Authentication] Serangan Brute Force Web (Hydra) Terdeteksi!</description>
  <mitre>
    <id>T1110</id>
  </mitre>
</rule>
