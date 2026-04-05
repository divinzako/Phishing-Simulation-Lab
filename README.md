# Phishing-Simulation-Lab

## 🛡️ Présentation du Projet
Ce projet consiste en la mise en place d'une infrastructure de simulation de phishing de bout en bout dans un environnement virtualisé isolé. L'objectif est de démontrer ma capacité à concevoir un scénario d'attaque réaliste, à gérer l'infrastructure système/réseau associée et à analyser les vecteurs de compromission liés au facteur humain.

> **⚠️ Note de sécurité :** Ce projet a été réalisé dans un environnement de laboratoire strictement isolé sur VMware (Host-Only). Aucune donnée réelle n'a été collectée ou compromise. Ce dépôt ne contient que de la documentation et des fichiers de configuration à but éducatif.

---

## 🏗️ Architecture Technique (VMware)
L'infrastructure repose sur un réseau virtuel privé interconnectant deux machines critiques pour simuler un environnement d'entreprise réel.

* **Serveur d'Infrastructure & Attaque : SRV-WIN-2022**
    * **OS :** Windows Server 2022
    * **Rôles :** Active Directory (AD DS), Serveur DNS.
    * **Solution :** Framework GoPhish (Hébergé localement sur le serveur).
    * **Usage :** Gestion de l'identité, résolution DNS et pilotage de la campagne.

* **Poste Cible (Victime) : CLI-WIN10-01**
    * **OS :** Windows 10 Pro
    * **Usage :** Consultation des emails (Outlook/Webmail) et navigation web (Edge/Chrome).

### 🌐 Plan d'Adressage IP (Lab Isolé)
| Machine | Système d'Exploitation | IP Statique | Rôle Principal |
| :--- | :--- | :--- | :--- |
| **SRV-WIN-2022** | Windows Server 2022 | `192.168.10.10` | Contrôleur de Domaine / DNS / GoPhish |
| **CLI-WIN10-01** | Windows 10 Pro | `192.168.10.20` | Poste de travail (Cible) |

---

## 🚀 Étapes de Réalisation

### 1. Configuration de l'Infrastructure DNS
Pour maximiser le réalisme de la simulation, j'ai configuré une zone DNS spécifique sur **Windows Server 2022**.
* **Technique :** Création d'enregistrements de type `A` pointant vers de faux noms de domaines.
* **Exemple :** `login.microsoft-security.local` pointe vers l'IP du serveur (`192.168.10.10`).
* **Objectif :** Tromper la vigilance de l'utilisateur lors du survol du lien dans l'email.

### 2. Déploiement et Durcissement de GoPhish
* Installation et configuration de GoPhish en tant que service sur Windows Server.
* **Hardening :** Modification du fichier `config.json` pour sécuriser l'interface d'administration (changement de port par défaut et restriction d'accès).
* Configuration du profil d'envoi SMTP pour assurer la délivrabilité dans le lab.

### 3. Design du Scénario d'Attaque (Social Engineering)
* **Email Template :** Rédaction d'un courriel utilisant des leviers psychologiques (urgence technique, mise à jour de sécurité obligatoire).
* **Landing Page :** Clonage d'une mire d'authentification réelle (type Microsoft 365) pour la capture sécurisée d'identifiants simulés.
* **Just-in-time Training :** Redirection après clic vers une page de sensibilisation expliquant les indices de phishing manqués.

---

## 📊 Analyse et KPIs (Indicateurs Clés)
Le tableau de bord GoPhish permet de suivre en temps réel :
* **Taux d'ouverture :** Pourcentage d'utilisateurs ayant ouvert l'email.
* **Taux de clics :** Pourcentage d'utilisateurs ayant cliqué sur le lien malveillant.
* **Taux de soumission :** Nombre d'utilisateurs ayant "livré" leurs identifiants sur la page de phishing.

---

## 🛠️ Stack Technique
* **Hyperviseur :** VMware Workstation
* **Systèmes :** Windows Server 2022, Windows 10 Pro
* **Outils :** GoPhish, Microsoft DNS Manager, Active Directory
* **Protocoles :** SMTP, DNS, HTTP/S
