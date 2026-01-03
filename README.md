# 🏁 Architecture Réseau Multi-Sites : Design & Connectivité WAN
> **Projet Technique :** Conception et déploiement d'une infrastructure Cisco complète.

![Cisco](https://img.shields.io/badge/Cisco-Packet_Tracer-049fd9?style=for-the-badge&logo=cisco)
![Status](https://img.shields.io/badge/Status-Opérationnel-success?style=for-the-badge)
![Year](https://img.shields.io/badge/Année-2025%2F2026-blueviolet?style=for-the-badge)

## 📌 Présentation du Projet
Ce projet consiste en la création d'un réseau d'entreprise interconnectant un siège social à des entités distantes. L'objectif est de démontrer la maîtrise des technologies de commutation avancée et de routage hybride pour assurer la disponibilité et la sécurité des données.

**Étudiant :** Oussama Ougui
**Encadrant :** Pr. Azzedine Khiat 

---

## 🏗️ Topologie & Matériel
L'infrastructure utilise une approche modulaire pour séparer les services et optimiser les performances.
![Texte Alternatif](chemin/vers/votre/image.png)
### Inventaire des Équipements
| Matériel | Quantité | Rôle Stratégique |
| :--- | :---: | :--- |
| **Routeur Cisco 2811** | 3 | Gestion du cœur de réseau et passerelles WAN. |
| **Switch Cisco 2960** | 2 | Commutation d'accès et distribution (LAN). |
| **PC Clients** | Plusieurs | Postes utilisateurs segmentés par département. |

> [!NOTE]
> La topologie complète inclut une zone LAN pour le siège et une simulation d'accès distant via des liaisons séries.

---

## 🛠️ Schéma d'Adressage IP
Une planification rigoureuse a été appliquée pour éviter les conflits et faciliter l'évolutivité.

| Périphérique | Interface | Adresse IP / Masque | Description |
| :--- | :--- | :--- | :--- |
| **R1** | Fa0/0.10 | 172.18.10.14 /28 | Passerelle VLAN 10 |
| **R1** | S0/0/0 | 10.0.30.177 /30 | Lien vers R2 (Backbone) |
| **S2** | Vlan 60 | 172.18.60.2 /28 | IP de Management |
| **R3** | Loopback0 | 10.0.30.129 /32 | Serveur de Test Distant |

---

## 🚀 Fonctionnalités Déployées

### 1. Commutation de Couche 2 (Switching)
- **Segmentation VLAN :** Division du réseau en 5 domaines de diffusion (10, 20, 30, 50, 60).
- **EtherChannel (LACP) :** Agrégation de ports entre S1 et S2 pour doubler la bande passante.
- **IEEE 802.1Q :** Mise en œuvre de Trunks pour le transport multi-VLAN.

### 2. Solutions de Routage (Routing)
- **Router-on-a-Stick :** Communication entre VLANs via les sous-interfaces de R1.
- **Interconnexion WAN :** Liaisons séries haut débit avec encapsulation HDLC.
- **Routage Statique :** Optimisation des tables de routage pour une convergence rapide.

---

## 🔍 Validation du Fonctionnement (Tests)

### Test de Connectivité WAN (Traceroute)
Le test suivant confirme que le trafic transite avec succès du siège vers le site distant en passant par le cœur de réseau.

```text
C:\> tracert 10.0.30.129
1    3 ms    0 ms    0 ms    172.18.10.14
2    0 ms    1 ms    0 ms    10.0.30.129
Trace complete.
