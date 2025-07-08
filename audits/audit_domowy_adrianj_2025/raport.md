# 🛡️ RAPORT BEZPIECZEŃSTWA SIECI DOMOWEJ  
**Audytor:** Adrian J.  
**Data:** 2025-07-06  
**Sieć:** 192.168.1.0/24  
**System audytowy:** Parrot OS  
**Narzędzia:** Nmap, netcat, curl, tshark, skrypty własne  

---

## 🔍 PODSUMOWANIE OGÓLNE

- **Aktywne hosty:** 12
- **Zidentyfikowane typy urządzeń:** router, kamera IP, IoT, serwer Java
- **Łącznie otwarte porty:** >20
- **Wykryte luki:** 2 krytyczne, 3 umiarkowane
- **Nieznane urządzenia (brak MAC/portów):** 8

---

## 📡 SZCZEGÓŁOWA ANALIZA

### 🔴 192.168.1.1 – Router Fibrain

- **MAC:** 54:DB:A2:52:EC:48
- **Porty:** 53 (DNS), 80 (HTTP), 5555 (custom?)
- **Luka:** `SLOWLORIS` (CVE-2007-6750) – podatność DoS
- **Uwagi:** Port 5555 może sugerować Android Debug Bridge lub debug backdoor

**🛠 Rekomendacje:**
- Wyłączyć/filtr port 5555
- Zabezpieczyć port 80 logowaniem lub VPN
- Zaktualizować firmware routera
- Włączyć ochronę DoS (jeśli dostępna)

---

### 🟡 192.168.1.102–106 – Urządzenia z portami IRC-like

- **Porty:** jeden otwarty (6667?) – sugeruje komunikację typu IRC
- **MAC:** Brak
- **Podejrzenia:** masowo skonfigurowane IoT (czujniki, kamerki, ESP)

**🛠 Rekomendacje:**
- Odczytać ruch z `tshark` lub `tcpdump`
- Sprawdzić firmware/producenta fizycznie
- Rozważyć segmentację (VLAN dla IoT)

---

### 📸 192.168.1.107 – Kamera IP (Tianjin Hualai)

- **MAC Vendor:** Tianjin Hualai Technology
- **Porty:** brak otwartych
- **Podejrzenia:** urządzenie z ukrytym RTSP/ONVIF, możliwy firmware backdoor

**🛠 Rekomendacje:**
- Sniffing (RTSP, port 554)
- Blokada dostępu do Internetu
- Analiza komunikacji ONVIF (`nmap -p 3702 -sU`)

---

### 🟠 192.168.1.108 – Zhen Shi InfoTech (CN)

- **MAC Vendor:** Zhen Shi InfoTech
- **Porty:** brak
- **Ryzyko:** potencjalny pasywny smart-device (brak aktualizacji)

**🛠 Rekomendacje:**
- Sprawdzenie obecności MQTT (`nmap -p 1883`)
- Monitorowanie transmisji (`tshark -i wlan0`)

---

### 🔴 192.168.1.115 – Serwer Java (Tomcat/JBoss?)

- **Porty:** `ajp13`, `https-alt`, `ssl/unknown`, `tcpwrapped`
- **Podejrzenia:** Podatność **Ghostcat** (AJP13 / CVE-2020-1938)

**🛠 Rekomendacje:**
- `nmap --script ajp-headers -p 8009`
- Wyłączyć port AJP, jeśli nieużywany
- Weryfikacja HTTPS interfejsu (`curl -k https://192.168.1.115:8443`)

---

### 🟫 Pozostałe hosty

| IP            | Status         | Porty       | Uwagi                      |
|---------------|----------------|-------------|----------------------------|
| 192.168.1.109 | Nieznany       | Brak        | brak fingerprintu          |
| 192.168.1.110 | Aktywny        | 53 (DNS?)   | Może forwarder/dhcp        |
| 192.168.1.114 | Nieznany       | Brak        | Prawdopodobnie czujnik     |

---

## ⚠️ NAJWIĘKSZE RYZYKA

1. **Brak segmentacji sieci (brak VLAN)**
2. **Urządzenia IoT z nieznanym firmware i portami IRC**
3. **Brak uwierzytelnienia na porcie 80 routera**
4. **Otwarte porty AJP13 – Ghostcat**
5. **Obecność kamery IP z Chin bez jawnych portów**

---

## ✅ REKOMENDACJE OGÓLNE

- 🔐 Wprowadzenie VLAN dla IoT
- 🧱 Wzmocnienie firewalla (iptables/router)
- 🕵️‍♂️ Sniffowanie podejrzanych urządzeń
- 🚫 Zamknięcie zbędnych portów (5555, AJP13)
- 📋 Weryfikacja fizyczna urządzeń nieznanych
- 🛡 Użycie narzędzi typu `OpenVAS`, `Nessus` dla głębszej analizy

---

## 📎 ZAŁĄCZNIKI

- `audit_domowy_adrianj_2025.txt` – pełny log analizy
- `vuln_192.168.1.1.txt` – luka Slowloris
- `nmap_fullscan.txt` – portscan całej sieci

---

## 🧠 SYGNATURA

> Adrian J.  
> Cybersec | Reverse | Offensive Recon   
> `#audit #security #network #homeLAN #parrotOS #ALEX`

