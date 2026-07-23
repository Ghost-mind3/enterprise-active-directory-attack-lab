# 👥 Active Directory Groups Design

## 📌 Présentation

Cette étape consiste à concevoir la structure des **Security Groups** de l'environnement Active Directory avant la création des comptes utilisateurs.

Dans Active Directory, les groupes jouent un rôle central dans la gestion des accès. Une bonne conception permet d'éviter l'attribution directe de permissions aux utilisateurs et facilite l'administration du domaine.

L'objectif est de préparer une structure basée sur le modèle **AGDLP (Accounts, Global Groups, Domain Local Groups, Permissions)** afin de reproduire une approche utilisée dans les environnements professionnels.

---

# 🎯 Objectifs

Cette phase a pour objectifs :

- Définir les rôles métiers de l'entreprise.
- Créer une convention de nommage pour les groupes.
- Séparer les rôles utilisateurs des permissions sur les ressources.
- Préparer l'implémentation du modèle AGDLP.
- Faciliter la future administration et les scénarios de Pentest Active Directory.

---

# 🏢 Contexte

L'environnement Active Directory appartient à l'entreprise fictive :

```
VulnCorp
```

Domaine :

```
vulncorp.local
```

La structure des groupes sera utilisée pour gérer les droits des différents départements :

- IT
- Finance
- Human Resources
- Developers
- Support
- Management

---

# 🔐 Modèle de gestion des accès

Le laboratoire utilise le modèle :

```
AGDLP
```

Signification :

```
Accounts

    ↓

Global Groups

    ↓

Domain Local Groups

    ↓

Permissions
```

---

## Pourquoi utiliser AGDLP ?

Attribuer directement une permission à un utilisateur crée une gestion difficile à maintenir.

Mauvaise approche :

```
User
 |
 └── Permission SMB
```

Problèmes :

- difficile à auditer ;
- difficile à modifier ;
- risque d'erreur humaine.

---

Approche recommandée :

```
User

 ↓

Global Group

 ↓

Domain Local Group

 ↓

Permission
```

Avantages :

- administration simplifiée ;
- meilleure traçabilité ;
- gestion centralisée des accès.

---

# 📁 Organisation des groupes

Les groupes seront stockés dans :

```
OU=Groups
```

---

# 🌐 Global Groups (GG)

Les **Global Groups** représentent les rôles et fonctions des utilisateurs dans l'entreprise.

Convention :

```
GG_<Role>
```

Exemple :

```
GG_IT_Admins
```

---

## Groupes définis

### IT Department

```
GG_IT_Admins
```

Rôle :

Administrateurs du département informatique.

---

```
GG_IT_Support
```

Rôle :

Techniciens support avec des privilèges limités.

---

### Finance Department

```
GG_Finance
```

Rôle :

Utilisateurs appartenant au service Finance.

---

### Human Resources

```
GG_HR
```

Rôle :

Utilisateurs du département RH.

---

### Developers

```
GG_Developers
```

Rôle :

Développeurs de l'entreprise.

---

### Management

```
GG_Management
```

Rôle :

Membres de la direction.

---

### Service Accounts

```
GG_Service_Admins
```

Rôle :

Gestion des comptes utilisés par les services.

---

# 🔒 Domain Local Groups (DL)

Les **Domain Local Groups** seront utilisés pour représenter les permissions appliquées aux ressources.

Convention :

```
DL_<Resource>_<Permission>
```

Exemples :

```
DL_Finance_Read

DL_Finance_Modify

DL_IT_Admin_Access
```

Ces groupes seront utilisés plus tard lors de la configuration :

- des SMB Shares ;
- des NTFS Permissions ;
- des ressources internes.

---

# Exemple d'utilisation

Scénario :

Un utilisateur du département Finance doit accéder au partage Finance.

Structure :

```
finance.user

      ↓

GG_Finance

      ↓

DL_Finance_Read

      ↓

SMB Share Finance
```

L'utilisateur n'a jamais de permission directement appliquée.

---

# 📷 Architecture des groupes

Le design des groupes Active Directory a été défini avant leur création effective.

![Active Directory Groups Design](Images/AD-Groups-Design.png)

---

# 🔐 Security Perspective

Une mauvaise gestion des groupes Active Directory peut entraîner :

- une élévation de privilèges involontaire ;
- des permissions excessives ;
- une mauvaise visibilité des accès.

La séparation entre rôles métiers (**Global Groups**) et permissions sur les ressources (**Domain Local Groups**) permet de limiter ces risques.

Cette organisation servira également lors des futures phases de Pentest, notamment pour analyser :

- les relations entre utilisateurs et groupes ;
- les chemins d'accès ;
- les privilèges excessifs.

---

# 📚 Compétences mises en œuvre

- Active Directory Security Groups
- AGDLP Model
- Access Control Design
- Privilege Management
- Enterprise Active Directory Administration

---

# 🚀 Prochaine étape

La prochaine phase consistera à créer les comptes utilisateurs Active Directory et à les intégrer dans les **Global Groups** correspondants.

Objectif :

```
Users

↓

Global Groups

↓

Access Management
```
