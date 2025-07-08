# 🛡️ Internal Security Audits – Home Network Pentesting Lab

![status](https://img.shields.io/badge/status-active-green)  
👤 Author: Adrian J.  
🗓️ Start: 2025-07-06  
🎯 Cel: Trening praktyczny z zakresu bezpieczeństwa sieci i IoT w środowisku domowym  

---

## 📌 Opis

To repozytorium dokumentuje **realne audyty bezpieczeństwa** wykonane w mojej domowej sieci lokalnej (`192.168.1.0/24`) przy użyciu **Parrot OS** oraz narzędzi klasy pentesterskiej.  
Celem projektu jest **eksperymentalna analiza zagrożeń, wykrywanie podatności i tworzenie własnych narzędzi** do automatyzacji i exploitacji.

--

## 🧪 Użyte narzędzia i techniki

- `nmap`, `masscan` – skanowanie portów, fingerprinting
- `vulners`, `nmap --script vuln` – skan podatności
- `netcat`, `curl`, `whois`, `tshark`, `pspy`, `arp-scan`
- Ręczna analiza konfiguracji sieci
- Identyfikacja urządzeń IoT i kamer
- Testy DoS i analiza potencjalnego CVE: `Ghostcat`, `Slowloris`

---

## 🔍 Przykładowe wyniki

- 📡 Router podatny na Slowloris (CVE-2007-6750)
- 🧱 Potencjalnie narażony serwer JBoss/Tomcat (`ajp13`, Ghostcat)
- 🔒 Brak segmentacji sieci – wszystkie urządzenia dostępne z jednej podsieci
- 📷 Kamera IP chińskiego producenta z brakiem portów – możliwy ukryty kanał
- 📟 Nierozpoznane urządzenia IRC-like (`6667/tcp`) – wymagają analizy

---

## 🧠 Co to pokazuje

✅ Rozumiem jak działa sieć  
✅ Umiem wykrywać realne podatności  
✅ Potrafię dokumentować i raportować wyniki  
✅ Tworzę własne skrypty i workflow pentesterski  
✅ Zabezpieczam, a nie tylko atakuję

---

## 📎 Dołączone pliki

- 🧾 **Raport PDF** – pełna dokumentacja audytu  
- 📜 **Logi Nmapa** – pełne dane portów i fingerprintu  
- 🧠 **Skrypt audytowy** – automatyzacja procesu
- 🧰 **Pliki surowe** – do własnej analizy

---

## 🏁 Plany rozwoju

- [ ] Integracja z `Shodan` API i `Censys`  
- [ ] Budowa własnego honeypota do testów  
- [ ] Wersja AI wspomagana (agent OSINT + audit assistant)  
- [ ] Wersja ofensywna z reverse shellami w labie  

---

> **Uwaga:** Wszystko testowane na prywatnej infrastrukturze – projekt edukacyjny.
