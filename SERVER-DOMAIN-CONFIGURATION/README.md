# 🖥️ Server & Domain Configuration

## 📌 Présentation

Cette première étape consiste à mettre en place les fondations de l'infrastructure **Active Directory** du laboratoire **VulnCorp**.

Avant de commencer les phases d'administration, d'énumération et de Pentest Active Directory, il est nécessaire de disposer d'un environnement stable avec un **Domain Controller (DC)** correctement configuré.

Cette phase comprend :

- Installation du système Windows Server
- Configuration réseau avec une adresse IP statique
- Installation du rôle **Active Directory Domain Services (AD DS)**
- Création d'une nouvelle **Forest**
- Promotion du serveur en **Domain Controller**
- Validation du bon fonctionnement du domaine

---

# 🎯 Objectifs

Les objectifs de cette phase sont :

- Déployer le premier serveur de l'infrastructure VulnCorp.
- Configurer une base réseau stable pour Active Directory.
- Créer le domaine `vulncorp.local`.
- Mettre en place le premier **Domain Controller**.
- Vérifier que les services Active Directory et DNS sont opérationnels.

---

# 🏢 Contexte du laboratoire

Le laboratoire simule l'infrastructure informatique d'une entreprise fictive appelée :

> **VulnCorp**

Cette entreprise utilisera progressivement un environnement Active Directory complet permettant de reproduire des scénarios réalistes d'administration et de sécurité.

---

# 🖥️ Environnement

| Machine | Rôle | Système |
|---|---|---|
| VULN-DC01 | Domain Controller | Windows Server 2019 |
| VULN-CL01 | Client Domain Member | Windows 10 |
| ATTACK01 | Machine d'attaque | Debian |

---

# 🌐 Configuration réseau

Le premier serveur Active Directory utilise la configuration réseau suivante :

| Paramètre | Valeur |
|---|---|
| Hostname | VULN-DC01 |
| Adresse IP | 192.168.32.148 |
| Masque réseau | 255.255.255.0 |
| Gateway | 192.168.32.2 |
| Domaine | vulncorp.local |
| NetBIOS Name | VULNCORP |

Une adresse IP statique a été configurée afin de garantir la stabilité des services Active Directory et DNS.

---

# ⚙️ Installation du serveur

La première étape consiste à installer Windows Server 2019 qui servira de base au futur **Domain Controller**.

Le serveur sera ensuite préparé pour accueillir les rôles nécessaires au fonctionnement d'un environnement Active Directory.

## Capture

![Installation Windows Server](Images/VULNAD-InstallServer.png)

---

# 🌐 Configuration réseau

Avant la promotion du serveur en **Domain Controller**, une configuration IP statique a été appliquée.

Cette étape est essentielle car un contrôleur de domaine ne doit pas dépendre d'une adresse IP dynamique.

Configuration appliquée :

```
IP Address : 192.168.32.148

Gateway : 192.168.32.2
```

Le serveur utilisera également son propre service DNS après la promotion en contrôleur de domaine.

---

# 🏛️ Création et promotion du Domain Controller

Le rôle **Active Directory Domain Services (AD DS)** a été installé puis le serveur a été promu comme premier **Domain Controller** d'une nouvelle forêt.

Configuration utilisée :

```
Forest Name :

vulncorp.local


NetBIOS Name :

VULNCORP
```

Options activées :

- ✅ Active Directory Domain Services
- ✅ DNS Server
- ✅ Global Catalog

Option désactivée :

- ❌ Read Only Domain Controller (RODC)

## Capture

![Promotion du domaine](Images/VULNAD-DomainPromote.png)

---

# ✅ Validation du domaine

Après le redémarrage du serveur, plusieurs vérifications ont été réalisées afin de confirmer que le domaine fonctionne correctement.

## Vérification du nom de la machine

Commande utilisée :

```powershell
hostname
```

Résultat attendu :

```
VULN-DC01
```

---

## Vérification du domaine Active Directory

Commande utilisée :

```powershell
Get-ADDomain
```

Cette commande permet de vérifier :

- Le nom du domaine.
- Le domaine DNS.
- Le nom NetBIOS.
- Les informations liées à la configuration Active Directory.

## Captures

![Informations domaine](Images/VULNAD-DomainInfo.png)

![Informations domaine PowerShell](Images/VULNAD-DomainInfo-01.png)

---

# 🔐 Security Perspective

À ce stade, l'environnement Active Directory est volontairement conservé dans un état propre.

Aucune vulnérabilité n'a encore été introduite.

Cette configuration servira de **baseline** pour les prochaines phases du projet.

Les futures vulnérabilités (mauvaise gestion des comptes, permissions excessives, faibles configurations Kerberos, SMB ou authentification Windows) seront ajoutées progressivement afin de comprendre leur impact dans un environnement réel.

---

# 📚 Compétences mises en œuvre

- Windows Server 2019
- Active Directory Domain Services (AD DS)
- Domain Controller Deployment
- DNS Integration
- Network Configuration
- PowerShell
- Active Directory Fundamentals

---

# 🚀 Prochaine étape

La prochaine phase sera consacrée à la conception de l'architecture logique Active Directory :

- Organizational Units (OU)
- Security Groups
- Naming Convention
- Administration Model
- Organisation des utilisateurs et des ordinateurs

Cette étape permettra de préparer une structure d'entreprise réaliste avant la création des premiers comptes et ressources.
