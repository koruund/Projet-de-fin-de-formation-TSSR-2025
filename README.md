<div align="center">

# Projet de fin de formation TSSR 2025
### Conception et déploiement d’une infrastructure informatique pour une PME

**Groupe B · Technicien Supérieur Systèmes et Réseaux (TSSR)**

[📄 Rapport final](Docs/rapport-final-infra-pme-tssr-2025.pdf) · [🖧 Schéma réseau](Docs/Diagrammes/topologie-finale.png) · [✏️ Source Draw.io](Docs/Diagrammes/topologie-finale.drawio)

</div>

---

## 📑 Sommaire

- [Présentation du projet](#-présentation-du-projet)
- [Architecture réseau](#-architecture-réseau)
- [Plan d’adressage](#-plan-dadressage)
- [Services et composants](#-services-et-composants)
- [Sécurité et disponibilité](#-sécurité-et-disponibilité)
- [Livrables du dépôt](#-livrables-du-dépôt)
- [Organisation de l’équipe](#-organisation-de-léquipe)
- [Consulter le projet](#-consulter-le-projet)

## 🎯 Présentation du projet

Dans le cadre de la formation **TSSR 2025**, notre groupe a conçu une infrastructure informatique pour une PME spécialisée dans la vente d’articles de sport. L’objectif est de proposer un environnement **virtualisé, segmenté, administrable et sécurisé**, adapté aux équipes internes comme aux utilisateurs nomades.

Le projet couvre notamment :

- La conception de l’architecture réseau et du plan d’adressage IP.
- La virtualisation des serveurs et l’administration centralisée.
- Le déploiement des services d’infrastructure et applicatifs.
- La segmentation du réseau par VLAN et le filtrage des flux.
- Le stockage partagé, la redondance et les sauvegardes.
- La documentation technique et la préparation de la soutenance.

## 🖧 Architecture réseau

Le schéma ci-dessous présente la topologie cible de l’infrastructure.

<div align="center">

![Topologie réseau de l’infrastructure PME](Docs/Diagrammes/topologie-finale.png)

*Figure 1 — Topologie finale de l’infrastructure.*

</div>

Le fichier source est disponible au format Draw.io : [`topologie-finale.drawio`](Docs/Diagrammes/topologie-finale.drawio).

### Principaux composants

| Composant | Fonction |
|---|---|
| **pfSense** | Pare-feu, filtrage réseau et accès VPN nomade |
| **Switch Cisco Layer 3** | Routage inter-VLAN |
| **VMware ESXi** | Hébergement des machines virtuelles |
| **vCenter (VCSA)** | Administration centralisée de l’environnement VMware |
| **SAN iSCSI** | Stockage partagé des données et des ISO |
| **Serveurs Windows et Linux** | Services d’annuaire, réseau, gestion de parc et applications |

## 🌐 Plan d’adressage

| VLAN | Usage | Réseau | Passerelle |
|---:|---|---|---|
| **10** | Serveurs | `10.10.10.0/24` | `10.10.10.1` |
| **20** | Clients | `10.10.20.0/24` | `10.10.20.1` |
| **30** | Connexion WAN | `10.10.30.0/24` | `10.10.30.1` |
| **99** | Infrastructure physique | `10.10.99.0/24` | `10.10.99.1` |

Cette segmentation permet de séparer les serveurs, les postes utilisateurs, la connexion WAN et les équipements d’infrastructure. Les règles de filtrage doivent contrôler les communications entre ces zones.

## 🧰 Services et composants

### Environnement Windows

| Serveur | Services / rôle |
|---|---|
| **SRV-AD01** | Active Directory, DNS, DHCP et partage de fichiers |
| **SRV-MDM** | ManageEngine Mobile Device Manager Plus (MDM) |

### Environnement Linux

| Serveur | Services / rôle |
|---|---|
| **SRV-LX01** | CMS web (HTTP/HTTPS) et FTP(S) |
| **SRV-LX02** | GLPI et supervision Zabbix |
| **SRV-LX03** | VoIP et Syslog — prévus dans le périmètre du projet |
| **SRV-LX04** | Messagerie Postfix — prévue dans le périmètre du projet |

### Réseau, virtualisation et stockage

- **pfSense** : sécurisation des flux, pare-feu et accès distant.
- **Switch Cisco Layer 3** : interconnexion et routage entre les VLAN.
- **VMware ESXi / vCenter** : hébergement et gestion des machines virtuelles.
- **SAN iSCSI** : stockage partagé, notamment pour les données des VM et les images ISO.

> **Note :** certains services sont indiqués comme prévus dans la documentation du projet. Leur présence dans cette liste ne signifie pas nécessairement qu’ils ont été déployés et validés en production.

## 🔐 Sécurité et disponibilité

Les principaux axes de sécurité et de résilience étudiés dans le projet sont :

- **Segmentation VLAN** afin de limiter les communications entre les zones.
- **Pare-feu pfSense** pour le filtrage et la maîtrise des accès.
- **VPN nomade** pour l’accès distant sécurisé.
- **Centralisation de l’administration** de l’environnement virtualisé via vCenter.
- **Stockage partagé et sauvegardes** pour contribuer à la continuité et à la restauration des services.

Les configurations détaillées et les éléments de mise en œuvre sont à consulter dans le rapport final.

## 📦 Livrables du dépôt

```text
.
├── README.md
└── Docs/
    ├── rapport-final-infra-pme-tssr-2025.pdf
    └── Diagrammes/
        ├── topologie-finale.png
        └── topologie-finale.drawio
```

| Livrable | Description |
|---|---|
| [Rapport final (PDF)](Docs/rapport-final-infra-pme-tssr-2025.pdf) | Documentation détaillée du projet, de l’architecture et des choix techniques |
| [Topologie réseau (PNG)](Docs/Diagrammes/topologie-finale.png) | Aperçu visuel du schéma d’infrastructure |
| [Source du schéma (Draw.io)](Docs/Diagrammes/topologie-finale.drawio) | Fichier modifiable de la topologie |

## 👥 Organisation de l’équipe

Les rôles de travail couvraient les domaines suivants :

- **Administration systèmes** : annuaire, DHCP, fichiers et MDM.
- **Administration réseau** : switch Layer 3, VLAN, pfSense et routage.
- **Virtualisation et stockage** : ESXi, vCenter et SAN.
- **Services applicatifs** : GLPI, supervision, CMS, VoIP et messagerie.

## 📖 Consulter le projet

1. Consultez le [rapport final](Docs/rapport-final-infra-pme-tssr-2025.pdf) pour les explications et les détails techniques.
2. Ouvrez [`topologie-finale.png`](Docs/Diagrammes/topologie-finale.png) pour visualiser rapidement l’architecture.
3. Importez [`topologie-finale.drawio`](Docs/Diagrammes/topologie-finale.drawio) dans [draw.io](https://app.diagrams.net/) pour explorer ou modifier le schéma.

---

<div align="center">

**Projet pédagogique — Formation TSSR 2025**  
*Groupe B · Du 22 septembre au 2 octobre 2025*

</div>
