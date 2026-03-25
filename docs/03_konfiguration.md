# 3. Konfiguration & Sicherheitsrichtlinien

## 3.1 Interfaces & Zonen
- LAN
- WAN
- VPN
- DMZ

## 3.2 Adressobjekte & Services
- Definition von Netzobjekten
- Service-Gruppen für Policies

## 3.3 Policies (inkl. NAT)

| ID | Source | Destination | Service | Action |
| -- | ------ | ----------- | ------- | ------ |
| 1  | LAN    | WAN         | ANY     | ALLOW  |
| 2  | LAN    | DNS         | DNS     | ALLOW  |

## 3.4 VPN-Konfiguration

### Site-to-Site VPN / Spoke to Hub

- Phase 1: IKEv2, PSK, AES256, SHA512, DH20, Lifetime 83600
- Phase 2: AES256, SHA512, DH20, Lifetime 3600

### Client VPN

- IPsec IKEv2
- Troubleshooting bei Phase-1 Errors

## 3.5 Security Profile

- Antivirus
- Webfilter
- IPS

## 3.6 Logging & Monitoring

- Firewall Logs
- VPN Monitoring
- Traffic Analyse

## 3.7 Switch Konfiguration (Beispiel)

```bash
interface GigabitEthernet1/0/2
 description JERRY_TEST
 switchport access vlan 2783
 switchport mode access
end
