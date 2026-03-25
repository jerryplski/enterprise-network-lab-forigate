# 2. Netzwerkdesign & Topologie

## 2.1 Topologie


## 2.2 Netzsegmente

- LAN
- WAN
- DMZ
- VPN
- VLANs

## 2.3 Geräte

- Firewall01: NL-FW-HUB_2.OG_NLAB
- Firewall02: NL-FW-SPK_3.OG
- Switch01: NLAB_2.OG_NETZWERK
- Switch02: NLAB_2.OG_NLAB

## 2.4 IP-Adressräume

**WAN-Privat:**  
HUB: WAN-1 xx.xx.xx.xx, WAN-2 yy.yy.yy.yy  
SPK: entsprechend  

**LAN-Öffentlich:**  
HUB: 10.60.0.0/16  
SPK: 10.61.0.0/16  

**VLANs (HUB)**

| VLAN | Netz                 | Beschreibung  |
| ---- | ------------------ | ------------- |
| 10   | 10.60.10.0/24       | Management    |
| 11   | 10.60.11.0/24       | Admins        |
| 12   | 10.60.12.0/24       | Clients       |
| 66   | 10.60.66.0/24       | Guest         |
| 100  | 10.60.100.0/24      | Printer       |
| 1    | 10.60.1.0/24        | Server        |

**Switchports Beispiel**

| Port   | Modus  | VLAN  |
| ------ | ------ | ----- |
| 0/0/1  | Trunk  | alle  |
| 0/0/3  | Access | 101   |

## 2.5 Benutzerverwaltung

Noch nicht implementiert
