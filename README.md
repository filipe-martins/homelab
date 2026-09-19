# 🚀 Homelab & Personal Infrastructure

Bem-vindo à documentação pública da minha infraestrutura pessoal de servidor e automação local.

Este repositório documenta a arquitetura, topologia e stack de software do meu Homelab. Este projeto serve como o meu laboratório pessoal onde testo conceitos de **Administração de Sistemas, Redes, Containers (Docker) e Segurança** em ambiente real.

---
![[Drawing Homelab.excalidraw|400]]
____
## 🛠️ Hardware & Infraestrutura
* **Servidor Principal BMax:** Mini PC (Intel n100, 12 GB RAM, 512 GB SSD) executando Proxmox Server 8.
* Servidor Secundário Herox:  Mini PC (Intel n100, 8 GB RAM, 256 GB SSD) executando Proxmox Server 8.
  Estrutura de dois servidores Proxmox em cluster para alta disponibilidade. 
  Dois servidores Docker para Load Balancing. 
  Dois Servidores Backup Proxmox para Rapidez e Redundância Dados.
* **Rede:** Dois Routers  para a rede Lan e IoT.

### 🛡️ Core & Segurança
* **Nginx Proxy Manager (Reverse Proxy):** Gere o tráfego externo seguro (HTTPS) com certificados automáticos Let's Encrypt.
* **Uptime Kuma:** Monitorização do estado dos serviços com alertas integrados.

## 🧰 Stack de Hardware & Virtualização

* **Rede & VPN:** [[Diagrama do acesso remoto#rede-e-segurança|Pi-hole DNS, Tailscale & Nginx Proxy Manager]]
* **Automação:** HomeAssistant, Smartlife, EweLink e Custom Scripts (PowerShell, Bash, Go, Python)
### 💾 Armazenamento e Produtividade
	Armazenamento:** Discos locais & mounts de armazenamento externo, através **Samba (NAS):** para a artilha de ficheiros local na rede doméstica.  
---

## 📦 Serviços em Execução (Docker Containers)

| Categoria          | Serviço                  | Descrição                                                                                  | Ficheiro Compose                          |     |
| :----------------- | :----------------------- | :----------------------------------------------------------------------------------------- | :---------------------------------------- | --- |
| **Gestão & proxy** | Nginx Proxy Manager      | Reverse Proxy com SSL automático<br>[[docs/Diagrama do acesso remoto#nginx-proxy-manager]] | `docker/reverse-proxy/docker-compose.yml` |     |
| Virtualização      | Portainer                | Gestão visual de containers Docker                                                         | ????                                      |     |
| **Rede & DNS**     | Pi-hole                  | DNS server & bloqueador de anúncios<br>[[Diagrama do acesso remoto#PI Hole]]               | CasaOS container                          |     |
| **Media & Áudio**  | Jellyfin                 | Streaming de filme/séries local Netflix                                                    | VM do Proxmox                             |     |
| **Áudio**          | Navidrome                | Servidor de streaming de música em alta fidelidade                                         | stack do portainer                        |     |
| **Arr Stack**      | Radarr / Sonarr / Bazarr | Automação e gestão de bibliotecas de media                                                 | stacks do portainer                       |     |
| **Feed & Leitura** | FreshRSS                 | Agregador de podcasts, RSS, feeds do Reddit e YouTube                                      | stack do portainer                        |     |

---

## 📁 Estrutura do Repositório

```text
meu-homelab/
├── README.md               # Cartão de visita e visão geral
├── .gitignore              # Proteção de credenciais e ficheiros sensíveis
├── docs/                   # Documentação detalhada e topologia
│   └── Diagrama do acesso remoto.md
├── ansible/                # Scripts de aprovisionamento (opcional)
└── docker/                 # Ficheiros Docker Compose limpos (sem credenciais)
    ├── reverse-proxy/
    │   └── docker-compose.yml
    └── media-server/
        └── docker-compose.yml


