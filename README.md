# 🛡️ OWASP Detection Lab: Real-Time Threat Detection with Wazuh SIEM

[![Wazuh](https://img.shields.io/badge/SIEM-Wazuh-005571?style=flat&logo=wazuh&logoColor=white)](https://wazuh.com/)
[![OWASP Top 10](https://img.shields.io/badge/Project-OWASP%20Top%2010%20Detection-blue)](https://owasp.org/Top10/)
[![MITRE ATT&CK](https://img.shields.io/badge/MITRE%20ATT%26CK-Mapping-purple)](https://attack.mitre.org/)

## 📌 Tentang Proyek Ini

Repositori ini merupakan **koleksi portofolio lab keamanan siber** yang mendokumentasikan implementasi **Wazuh SIEM** untuk mendeteksi berbagai serangan yang termasuk dalam daftar **OWASP Top 10**.

Setiap skenario serangan dikonfigurasi dengan *custom rules* di Wazuh, diuji dalam lingkungan lab terkendali, dan di-mapping ke kerangka **MITRE ATT&CK** untuk memberikan konteks ancaman yang lebih mendalam.

## 📂 Struktur Repositori

```
OWASP-Detection-Lab/
├── 01-Broken-Authentication/   # Skenario A01: Broken Authentication
│   └── README.md                # Dokumentasi deteksi Brute Force dengan Hydra
├── 02-Injection/                # Skenario A03: Injection
│   └── README.md                # Dokumentasi deteksi SQL Injection dengan SQLMap
├── images/                      # Screenshot dan gambar pendukung
│   ├── apache-sqli-log.png
│   ├── sqlmap-attack.png
│   └── wazuh-sqli-alert.png
├── rules/                       # Kumpulan custom rules Wazuh (XML)
│   ├── local_rules.xml           # Rule untuk deteksi Brute Force Hydra (A01)
│   └── sqli_rules.xml            # Rule untuk deteksi SQL Injection (A03)
└── README.md                    # Dokumentasi utama (file ini)
```

## 📋 Daftar Skenario Deteksi (OWASP Top 10 2025)

| Project | Kode OWASP | Kategori | Vektor Serangan | Status | Dokumentasi |
|:-------:|:----------:|----------|-----------------|--------|-------------|
| **#1** | **A07:2025** | Authentication Failures | Brute Force Attack dengan Hydra | ✅ Selesai | [01-Broken-Authentication/](./01-Broken-Authentication/) |
| **#2** | **A05:2025** | Injection | SQL Injection dengan SQLMap | ✅ Selesai | [02-Injection/](./02-Injection/) |
| **#3** | A02:2025 | Security Misconfiguration | *(Coming Soon)* | ⏳ Rencana | - |
| **#4** | A01:2025 | Broken Access Control | *(Coming Soon)* | ⏳ Rencana | - |

> **Catatan:** Penomoran mengikuti kode OWASP Top 10 asli (A01, A02, A03, dst). Folder `02-Injection` berisi skenario **A03: Injection**.

## 🧪 Arsitektur Lab Umum

Lingkungan lab yang digunakan relatif konsisten untuk setiap skenario:

| Peran | Sistem Operasi | Tools/Aplikasi |
|-------|----------------|----------------|
| **Attacker** | Kali Linux | Hydra, SQLMap, dll (sesuai skenario) |
| **Target (Agent)** | Ubuntu Server 22.04 | Apache2, DVWA, Wazuh Agent |
| **SIEM Manager** | Ubuntu 22.04 | Wazuh Manager |

Detail spesifik seperti IP Address dan konfigurasi akan dijelaskan di setiap dokumentasi skenario.

## 🛠️ Koleksi Custom Rules

Semua *custom rules* yang dibuat untuk proyek ini dapat ditemukan di folder [`/rules`](./rules/). Saat ini tersedia:

| File Rule | Skenario | Keterangan |
|-----------|----------|------------|
| [`rules/local_rules.xml`](./rules/local_rules.xml) | A01 - Broken Authentication | Deteksi Brute Force dengan Hydra |
| [`rules/sqli_rules.xml`](./rules/sqli_rules.xml) | A03 - Injection | Deteksi SQL Injection dengan SQLMap |

## 🎯 Tujuan Proyek

1. **Membangun Portofolio** - Menunjukkan kemampuan praktis dalam SIEM Engineering dan Threat Detection
2. **Validasi OWASP Top 10** - Mendemonstrasikan deteksi untuk setiap kategori risiko
3. **Penerapan MITRE ATT&CK** - Memberikan konteks ancaman standar industri
4. **Dokumentasi Terstruktur** - Menyediakan panduan yang jelas dan *replicable*

## 🚀 Mulai Jelajahi

- **[Skenario 1: A01 - Broken Authentication (Brute Force Hydra)](./01-Broken-Authentication/)** → Deteksi serangan Brute Force
- **[Skenario 2: A03 - Injection (SQL Injection dengan SQLMap)](./02-Injection/)** → Deteksi serangan SQL Injection

## 🙋‍♂️ Tentang Pembuat

Proyek ini dikembangkan sebagai bagian dari portofolio keamanan siber. Fokus utama: **SOC Operations**, **SIEM Engineering**, **Threat Hunting**, dan **Detection Rule Writing**.

---
*Dokumentasi ini disusun sebagai bagian dari portofolio keamanan siber.*

---
