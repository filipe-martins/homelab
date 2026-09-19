
Esta nota detalha o fluxo de tráfego, o roteamento de DNS e a segmentação de acesso remoto da infraestrutura.

---

## 📐 Diagrama de Fluxo (Mermaid)

```mermaid
graph TD
    UserPublic[Cliente Externo / Telemóvel] -->|VPN / Tailscale| TS[Tailscale Mesh Network]
    UserLocal[Rede Local LAN] --> NPM[Nginx Proxy Manager]
    
    TS --> NPM
    
    subgraph "Proxmox Host (Virtualização)"
        PiHole[Pi-hole DNS]
        NPM -->|HTTP 80/443| Portainer[Portainer UI]
        NPM -->|Reverse Proxy| Jellyfin[Jellyfin]
        NPM -->|Reverse Proxy| Navidrome[Navidrome]
        NPM -->|Reverse Proxy| ArrStack[Sonarr / Radarr / Bazarr]
        NPM -->|Reverse Proxy| FreshRSS[FreshRSS]
    end
    
    UserLocal -->|Consultas DNS| PiHole