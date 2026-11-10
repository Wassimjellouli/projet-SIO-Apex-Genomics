# projet-SIO-Apex-Genomics
Voici le projet de fin d'année "Apex Genomics" de Lily Boigeaud et Wassim Jellouli portant sur la création complète d'une infrastructure réseau

# 🧬 Apex Genomics : Infrastructure IT sécurisée et redondée

> Une infrastructure segmentée, hautement disponible et supervisée, reliant deux sites pour une société de biotechnologie spécialisée dans la recherche d'antibiotiques par intelligence artificielle.


---

## 📑 Sommaire

- [Contexte du projet](#-contexte-du-projet)
- [Présentation de l'entreprise](#-présentation-de-lentreprise)
- [Organisation géographique](#-organisation-géographique)
- [Problématique](#-problématique)
- [Besoins exprimés par la direction](#-besoins-exprimés-par-la-direction)
- [Contraintes](#-contraintes)
- [Objectifs du projet](#-objectifs-du-projet)

---

## 📌 Contexte du projet

### 🏢 Présentation de l'entreprise

**Apex Genomics** est une société de biotechnologie spécialisée dans l'**intelligence artificielle appliquée à la recherche de nouveaux antibiotiques**. Face à l'essor de l'antibiorésistance, l'entreprise développe des modèles d'IA capables d'analyser des millions de molécules pour identifier de nouvelles pistes thérapeutiques et réduire les délais de la recherche pharmaceutique.

Elle collabore avec des laboratoires, des hôpitaux et des partenaires pharmaceutiques. Ses équipes réunissent des chercheurs, des data scientists, des ingénieurs IA et du personnel administratif.

### 🗺️ Organisation géographique

| Site | Rôle | Infrastructure |
|------|------|----------------|
| **Site A : siège (Lyon)** | Direction, administration, support IT, data scientists. Héberge les services applicatifs exposés (web, ticketing). | Routeur/pare-feu central, DMZ, 2 switches en stack, VLAN 10 et VLAN 20, serveurs web et GLPI en load balancing, reverse proxies redondants |
| **Site B : laboratoire de recherche** | Chercheurs, biologistes, ingénieurs IA. Héberge les services critiques (annuaire, sauvegarde, supervision, accès d'administration). | Hyperviseur Proxmox, cluster pfSense redondant, serveurs Windows 2022, serveur de sauvegarde, supervision, bastions |

Les deux sites sont reliés par un **tunnel VPN site-à-site sécurisé** passant par le réseau intermédiaire (réseau pédagogique dans le cadre du projet).

### ⚠️ Problématique

Apex Genomics manipule des **données de recherche très sensibles** : résultats de criblage de molécules, modèles d'IA propriétaires, données issues de partenaires hospitaliers. Une panne ou une fuite aurait un impact direct sur :

- 🔬 **la propriété intellectuelle** : brevets, modèles d'IA
- 🏥 **la confiance des partenaires hospitaliers**
- ⚖️ **la conformité réglementaire** : RGPD, données de santé
- ⏱️ **la continuité des projets de recherche**, coûteux et soumis à des délais stricts

Aujourd'hui, l'entreprise **ne dispose pas d'infrastructure centralisée** : pas d'annuaire commun, pas de supervision, pas de sauvegarde structurée, pas de séparation entre les flux utilisateurs, administrateurs et services exposés.

### 🎯 Besoins exprimés par la direction

- **Interconnexion sécurisée** des deux sites par VPN site-à-site
- **Authentification centralisée** : annuaire Active Directory, DHCP, DNS, nom de domaine
- **Segmentation réseau** : VLAN utilisateurs (VLAN 10), VLAN d'administration et d'analyse (VLAN 20), DMZ pour les services exposés
- **Gestion des incidents** via un outil de ticketing (GLPI) en haute disponibilité
- **Services web** : intranet et site vitrine, répartis sur deux serveurs avec équilibrage de charge
- **Publication sécurisée** via des reverse proxies redondants sur chaque site (keepalived)
- **Supervision** de l'ensemble des équipements et services (Zabbix, redondé)
- **Sauvegarde automatique** des services critiques vers un serveur de sauvegarde dédié
- **Accès d'administration sécurisés** : bastions SSH/RDP par clés et double authentification (FreeOTP)
- **Sécurité périmétrique** : pare-feu pfSense en haute disponibilité avec IDS/IPS (Suricata) et authentification RADIUS
- **Haute disponibilité à tous les niveaux** : stack de switches, agrégation de liens, cluster de pare-feu, services en load balancing ou VRRP/keepalived

### 🔒 Contraintes

| Contrainte | Description |
|------------|-------------|
| 🛡️ **Sécurité** | Protection des données de recherche, conformité RGPD, traçabilité des accès administrateurs |
| 🟢 **Disponibilité** | Aucun point de défaillance unique sur les services critiques |
| 📈 **Évolutivité** | Possibilité d'ajouter des collaborateurs, des services, voire un troisième site |
| 💶 **Budget maîtrisé** | Privilégier les solutions open source (pfSense, Proxmox, Zabbix, GLPI, Docker) |
| 📚 **Documentation** | Schémas, procédures d'exploitation, procédures de restauration, comptes rendus de tests |

### ✅ Objectifs du projet

À l'issue du projet, l'équipe IT d'Apex Genomics doit disposer :

- [ ] D'une **infrastructure fonctionnelle, segmentée, sécurisée et redondée** sur les deux sites
- [ ] D'un **tunnel VPN opérationnel** entre le siège et le laboratoire
- [ ] D'une **supervision et d'une sauvegarde automatisées**
- [ ] D'un **accès d'administration sécurisé** via bastion avec double authentification
- [ ] D'une **documentation technique complète**
- [ ] D'une **démonstration de continuité de service** : simulation de panne d'un pare-feu, d'un reverse proxy, d'un serveur web, puis reprise automatique

---

## 🧰 Stack technique

![pfSense](https://img.shields.io/badge/pfSense-212121?logo=pfsense&logoColor=white)
![Proxmox](https://img.shields.io/badge/Proxmox-E57000?logo=proxmox&logoColor=white)
![Zabbix](https://img.shields.io/badge/Zabbix-DC382D?logo=zabbix&logoColor=white)
![GLPI](https://img.shields.io/badge/GLPI-FEC95C?logoColor=black)
![Docker](https://img.shields.io/badge/Docker-2496ED?logo=docker&logoColor=white)
![Suricata](https://img.shields.io/badge/Suricata-EF3B2D?logoColor=white)
![Keepalived](https://img.shields.io/badge/keepalived-VRRP-green)
![Windows Server](https://img.shields.io/badge/Windows%20Server%202022-0078D4?logo=windows&logoColor=white)
