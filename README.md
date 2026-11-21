# Laboratorio de Seguridad Perimetral, Enrutamiento y Servicios en Linux

Implementación y validación de una arquitectura de red segmentada multi-máquina sobre Linux, aplicando políticas de filtrado de paquetes con **Netfilter / nftables**, traducción de direcciones (**NAT / DNAT**) y despliegue seguro de servicios de transferencia de archivos (**Samba** y **ProFTPD**).

---

## 1. Topología de Red

La infraestructura consta de una pasarela perimetral (**Gateway**) que conecta una red externa con una subred interna (DMZ / LAN) donde residen los servidores de aplicaciones:

```text
[ Red Externa / Cliente (VM3) ]
       192.168.20.0/24
              │
              ▼  (IP Pública: 192.168.20.34)
     ┌─────────────────┐
     │  Gateway (GW)   │  <-- Firewall nftables + NAT/DNAT
     └────────┬────────┘
              │  (Red Interna: 192.168.7.0/24)
              ▼
   ┌─────────────────────┐
   │ Servidor Interno    │  <-- Samba (SMB) + ProFTPD (FTP)
   │  (192.168.7.101)    │
   └─────────────────────┘
