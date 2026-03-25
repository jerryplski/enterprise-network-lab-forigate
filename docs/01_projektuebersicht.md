# 1. Projektübersicht & Zielsetzung

## 1.1 Projektbeschreibung

Planung eines Projektes "NLAB Solutions GmbH" mit zwei simulierten Standorten:

* Zwei Standorte mit eigenen /16 Netzbereichen
* Standort A: VLANs auf einer physischen Firewall-Schnittstelle
* Standort B: mehrere physische Interfaces auf Firewall
* Switchports entsprechend VLAN/Client/Management angepasst
* WAN- und DNS-Regeln erstellt

## 1.2 Meilensteine

**KW-29**
- Projektplanung, Netzsegmentierung
- Interfaces einrichten
- LAN-to-LAN, LAN-to-WAN, LAN-to-DNS Policies
- Security Profiles & DNS Security
- Site-to-Site/Hub-to-Spoke VPN vorbereiten

**KW-30**
- Site-to-Site VPN mit Overlapping Subnets (SNAT/DNAT & 1-to-1 Mapping)

**KW-31**
- Dynamisches Routing Hub-to-Spoke mit BGP

**KW-32**
- Dual-WAN Interfaces für Standort B
- SD-WAN & Performance SLA

**KW-33**
- Remote Client IPsec VPN IKEv2
- Site-to-Site mit Redundanz

**KW-34**
- Monitoring der VPNs (NLAB ↔ Mekos)

## 1.3 To-Do

- Traffic Shaper konfigurieren
- Client VPN finalisieren
- IPv6 Integration
- Transportnetz & Site-to-Site VPN neu aufbauen
- BGP erneut aufsetzen

## 1.4 Lernziele

- Routing vs NAT verstehen
- VLAN-Design und Port-Strategien
- VPN-Implementierung (Site-to-Site & Remote)
- BGP Grundlagen, Troubleshooting

## 1.5 Lernnotizen

- **NAT-Grundprinzip (15.07.25)**  
  „Es ist immer NAT – oder Routing oder DNS.“

- **BGP (29.07.25)**  
  * Routen müssen lokal bekannt sein, bevor sie verteilt werden
  * Blackhole Route zur Ankündigung
  * Administrative Distance:  
    1. Connected  
    2. Static  
    3. Dynamic (BGP, OSPF, RIP)
