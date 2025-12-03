# 🔧 Application de Gestion Lydec - Système de Management Intégré

[![.NET Framework](https://img.shields.io/badge/.NET%20Framework-4.7.2-blue.svg)](https://dotnet.microsoft.com/)
[![C#](https://img.shields.io/badge/C%23-8.0-green.svg)](https://docs.microsoft.com/en-us/dotnet/csharp/)
[![MySQL](https://img.shields.io/badge/MySQL-8.4-orange.svg)](https://www.mysql.com/)
[![License](https://img.shields.io/badge/License-Academic-yellow.svg)](LICENSE)

## 📋 Table des Matières

- [À Propos](#à-propos)
- [Fonctionnalités Principales](#fonctionnalités-principales)
- [Architecture du Système](#architecture-du-système)
- [Technologies Utilisées](#technologies-utilisées)
- [Modèle de Données](#modèle-de-données)
- [Installation et Configuration](#installation-et-configuration)
- [Démonstration](#démonstration)
- [Compétences Développées](#compétences-développées)
- [Perspectives d'Amélioration](#perspectives-damélioration)
- [Contact](#contact)

---

## 🎯 À Propos

**Application de Gestion Lydec** est une solution complète de gestion développée pour optimiser les opérations d'une entreprise de services publics. Ce projet académique simule un système réel de gestion client, permettant la gestion intégrée des clients, des compteurs, des facturations, des paiements et des interventions techniques.

> 💡 **Contexte du Projet** : Développé dans le cadre de mes études supérieures, ce projet démontre ma capacité à concevoir et implémenter des solutions logicielles complexes répondant à des besoins métier réels.

### 🎓 Objectifs Pédagogiques

- Maîtrise du développement d'applications desktop avec C# et Windows Forms
- Conception et implémentation de bases de données relationnelles avec MySQL
- Application des principes de l'architecture logicielle et des patterns de conception
- Gestion complète du cycle de vie d'un projet logiciel

---

## ✨ Fonctionnalités Principales

### 🔐 1. Système d'Authentification

- Interface de connexion sécurisée
- Gestion des sessions utilisateurs
- Contrôle d'accès à l'application

### 🏙️ 2. Gestion Territoriale

**Villes (Form1.cs)**

- CRUD complet (Create, Read, Update, Delete)
- Recherche avancée par ID
- Affichage en temps réel dans DataGridView

**Quartiers (Quartier.cs)**

- Gestion hiérarchique des quartiers par ville
- Association automatique avec les villes parentes
- Gestion des codes postaux
- Recherche multicritère (par ID de quartier ou de ville)

### 👥 3. Gestion Clientèle (Client.cs)

- **Enregistrement complet** : nom, prénom, adresse, téléphone, email
- **Localisation précise** : association automatique au quartier et à la ville
- **Recherche intelligente** : par ID client ou ID quartier
- **Jointures complexes** : affichage des informations complètes (client + quartier + ville)
- **Opérations CRUD** : avec validation des données

### ⚡ 4. Gestion des Compteurs (Compteur.cs)

- **Enregistrement des équipements** : date d'installation, type (eau/électricité)
- **Association client-compteur** : traçabilité complète
- **Recherche multicritère** : par ID compteur ou ID client
- **Historique** : suivi de tous les compteurs installés
- **Affichage relationnel** : compteur → client → quartier → ville

### 💰 5. Facturation et Paiement

**Module Factures (Facture.cs)**

- Génération de factures liées aux compteurs
- Calcul automatique des montants
- Gestion des statuts de paiement (payé/impayé/en cours)
- Types de services (eau, électricité, assainissement)
- Recherche par ID facture ou ID compteur

**Module Paiements (Paiement.cs)**

- Enregistrement des paiements clients
- Association facture-paiement
- Suivi chronologique des paiements
- Calcul des montants et dates
- Recherche par ID paiement ou ID facture

### 🛠️ 6. Service Client (Service_Client.cs)

- **Gestion des demandes clients** : enregistrement des réclamations et demandes
- **Suivi des statuts** : en cours, résolu, en attente
- **Descriptions détaillées** : documentation de chaque demande
- **Traçabilité** : association client-demande avec horodatage
- **Recherche** : par ID service ou ID client

### 👷 7. Gestion des Techniciens (echnoque.cs)

- **Base de données techniciens** : nom, prénom, spécialité
- **Spécialités** : électricité, plomberie, maintenance générale
- **Disponibilité** : gestion de l'équipe technique
- **Opérations CRUD** : avec recherche par ID

### 🔧 8. Interventions Techniques (Intervention_Technicien.cs)

- **Planification des interventions** : date, description, assignation
- **Association complexe** : technicien + compteur + client
- **Traçabilité complète** : historique de toutes les interventions
- **Recherche avancée** : par ID intervention, ID compteur ou ID technicien
- **Reporting** : affichage complet des informations d'intervention

---

## 🏗️ Architecture du Système

### Structure Modulaire

```
Application-de-Gestion-Lydec/
│
├── 🔐 Authentification
│   └── loginhome.cs (Login & Session)
│
├── 🌍 Gestion Territoriale
│   ├── Form1.cs (Villes)
│   └── Quartier.cs (Quartiers)
│
├── 👥 Gestion Clients
│   ├── Client.cs (Clients)
│   └── Compteur.cs (Compteurs)
│
├── 💼 Gestion Financière
│   ├── Facture.cs (Facturation)
│   └── Paiement.cs (Paiements)
│
├── 🛠️ Gestion Services
│   ├── Service_Client.cs (Support Client)
│   ├── echnoque.cs (Techniciens)
│   └── Intervention_Technicien.cs (Interventions)
│
└── 🗄️ Couche Données
    └── databasehelper.cs (Accès BD centralisé)
```

### 📊 Modèle Relationnel Hiérarchique

```
Ville (1) ──┐
            ├──> Quartier (N) ──┐
                                ├──> Client (N) ──┐
                                                   ├──> Compteur (N) ──┐
                                                   │                   ├──> Facture (N) ──> Paiement (N)
                                                   │                   └──> Intervention (N) ←── Technicien (1)
                                                   └──> Service_Client (N)
```

### 🎨 Pattern Architectural

**Pattern :** Forms & Data Access Layer (DAL)

- **Couche Présentation** : Windows Forms avec DataGridView
- **Couche Logique Métier** : Classes C# avec validation
- **Couche Données** : `databasehelper.cs` - centralisation de l'accès MySQL
- **Avantages** :
  - Séparation des préoccupations
  - Réutilisabilité du code
  - Maintenance facilitée
  - Sécurité des connexions

---

## 🛠️ Technologies Utilisées

### Langages & Frameworks

| Technologie  | Version    | Usage                 |
| ------------ | ---------- | --------------------- |
| **C#**       | 8.0        | Langage principal     |
| **WinForms** | .NET 4.7.2 | Interface utilisateur |
| **MySQL**    | 8.4.0      | Base de données       |
| **ADO.NET**  | -          | Accès aux données     |

### Packages NuGet Principaux

```xml
- MySql.Data (8.4.0) : Connecteur MySQL optimisé
- System.Configuration.ConfigurationManager (4.4.1) : Gestion configuration
- System.Data.SqlClient : Opérations base de données
```

### Outils de Développement

- **IDE** : Visual Studio 2022
- **Contrôle de version** : Git & GitHub
- **Base de données** : MySQL Workbench
- **Design** : Windows Forms Designer

---

## 💾 Modèle de Données

### Schéma de Base de Données

#### 📍 Table : `Ville`

```sql
CREATE TABLE Ville (
    Id_ville INT PRIMARY KEY AUTO_INCREMENT,
    nom_ville VARCHAR(100) NOT NULL
);
```

#### 📍 Table : `Quartier`

```sql
CREATE TABLE Quartier (
    Id_quartier INT PRIMARY KEY AUTO_INCREMENT,
    nom_quartier VARCHAR(100) NOT NULL,
    code_postal VARCHAR(10),
    Id_ville INT,
    nom_ville VARCHAR(100),
    FOREIGN KEY (Id_ville) REFERENCES Ville(Id_ville)
);
```

#### 👤 Table : `Client`

```sql
CREATE TABLE Client (
    Id_client INT PRIMARY KEY AUTO_INCREMENT,
    nom VARCHAR(50) NOT NULL,
    prénom VARCHAR(50) NOT NULL,
    adresse VARCHAR(200),
    telephone VARCHAR(15),
    email VARCHAR(100),
    Id_quartier INT,
    nom_quartier VARCHAR(100),
    FOREIGN KEY (Id_quartier) REFERENCES Quartier(Id_quartier)
);
```

#### ⚡ Table : `Compteur`

```sql
CREATE TABLE Compteur (
    Id_compteur INT PRIMARY KEY AUTO_INCREMENT,
    date_installation DATE,
    type VARCHAR(50), -- eau, électricité
    Id_client INT,
    nom VARCHAR(50),
    FOREIGN KEY (Id_client) REFERENCES Client(Id_client)
);
```

#### 📄 Table : `Facture`

```sql
CREATE TABLE Facture (
    Id_facture INT PRIMARY KEY AUTO_INCREMENT,
    date_facturation DATE,
    montant DECIMAL(10,2),
    statut_paiement VARCHAR(50), -- payé, impayé, en cours
    type_service VARCHAR(50),
    Id_compteur INT,
    FOREIGN KEY (Id_compteur) REFERENCES Compteur(Id_compteur)
);
```

#### 💳 Table : `Paiement`

```sql
CREATE TABLE Paiement (
    Id_paiement INT PRIMARY KEY AUTO_INCREMENT,
    date_paiement DATE,
    montant_paiement DECIMAL(10,2),
    id_facture INT,
    FOREIGN KEY (id_facture) REFERENCES Facture(Id_facture)
);
```

#### 🛠️ Table : `Service_Client`

```sql
CREATE TABLE Service_Client (
    Id_service INT PRIMARY KEY AUTO_INCREMENT,
    date_demande DATE,
    description_demande TEXT,
    statut VARCHAR(50), -- en cours, résolu, en attente
    client_id INT,
    name_patient VARCHAR(100),
    FOREIGN KEY (client_id) REFERENCES Client(Id_client)
);
```

#### 👷 Table : `Technicien`

```sql
CREATE TABLE Technicien (
    id_technicien INT PRIMARY KEY AUTO_INCREMENT,
    nom VARCHAR(50) NOT NULL,
    prenom VARCHAR(50) NOT NULL,
    specialite VARCHAR(100) -- électricité, plomberie, etc.
);
```

#### 🔧 Table : `Intervention_Technicien`

```sql
CREATE TABLE Intervention_Technicien (
    id_intervention INT PRIMARY KEY AUTO_INCREMENT,
    date_intervention DATE,
    description TEXT,
    Id_compteur INT,
    Id_technicien INT,
    nom VARCHAR(50),
    FOREIGN KEY (Id_compteur) REFERENCES Compteur(Id_compteur),
    FOREIGN KEY (Id_technicien) REFERENCES Technicien(id_technicien)
);
```

#### 🔐 Table : `Users`

```sql
CREATE TABLE Users (
    id INT PRIMARY KEY AUTO_INCREMENT,
    editor VARCHAR(50) NOT NULL,
    password VARCHAR(255) NOT NULL
);
```

### Relations Clés

- **Hiérarchie géographique** : Ville → Quartier → Client
- **Équipements** : Client → Compteur
- **Facturation** : Compteur → Facture → Paiement
- **Services** : Client → Service_Client
- **Interventions** : Compteur + Technicien → Intervention

---

## 🚀 Installation et Configuration

### Prérequis

```bash
- .NET Framework 4.7.2 ou supérieur
- MySQL Server 8.0+
- Visual Studio 2019/2022
- MySQL Workbench (recommandé)
```

### Étapes d'Installation

#### 1️⃣ Cloner le Repository

```bash
git clone https://github.com/MohammedBelmekki01/Application-de-Gestion-de-lydec-.git
cd Application-de-Gestion-de-lydec-
```

#### 2️⃣ Configuration de la Base de Données

**Créer la base de données :**

```sql
CREATE DATABASE simolydec;
USE simolydec;
```

**Exécuter les scripts de création de tables** (voir section Modèle de Données)

**Créer un utilisateur de test :**

```sql
INSERT INTO Users (editor, password) VALUES ('admin', 'admin123');
```

#### 3️⃣ Configuration de la Connexion

Modifier `databasehelper.cs` ligne 11 :

```csharp
private static string connectionString =
    "server=localhost;user id=root;password=VOTRE_PASSWORD;database=simolydec";
```

#### 4️⃣ Restaurer les Packages NuGet

Dans Visual Studio :

```
Tools > NuGet Package Manager > Restore NuGet Packages
```

Ou via ligne de commande :

```bash
nuget restore simofinal.sln
```

#### 5️⃣ Compilation et Exécution

1. Ouvrir `simofinal.sln` dans Visual Studio
2. Définir `simofinal` comme projet de démarrage
3. Appuyer sur **F5** ou cliquer sur **Démarrer**

### Configuration de Production (Optionnel)

Pour une utilisation en production, considérer :

- Chiffrement des mots de passe (BCrypt, SHA256)
- Paramétrage externe de la chaîne de connexion (App.config)
- Gestion des rôles utilisateurs
- Logging des opérations sensibles

---

## 🎬 Démonstration

### Captures d'Écran Principales

#### Interface de Connexion

```
┌─────────────────────────────┐
│   🔐 LYDEC Management       │
│                             │
│   Username: [____________]  │
│   Password: [____________]  │
│                             │
│   [ Login ]  [ Clear ]      │
└─────────────────────────────┘
```

#### Dashboard Principal

- Menu latéral avec navigation vers tous les modules
- Zone d'affichage centrale avec DataGridView
- Barre d'outils avec boutons d'action (Ajouter, Modifier, Supprimer)
- Champs de recherche dynamiques

### Workflow Typique

1. **Création d'une Ville** → Ajout d'un **Quartier**
2. Enregistrement d'un **Client** dans ce quartier
3. Installation d'un **Compteur** pour le client
4. Génération d'une **Facture** basée sur le compteur
5. Enregistrement du **Paiement** de la facture
6. Création d'une demande de **Service Client** si nécessaire
7. Planification d'une **Intervention Technique** par un technicien

---

## 💡 Compétences Développées

### Techniques

- ✅ **Programmation Orientée Objet (POO)** : encapsulation, héritage, polymorphisme
- ✅ **Conception de Bases de Données** : modélisation relationnelle, normalisation
- ✅ **Requêtes SQL Avancées** : jointures multiples, sous-requêtes, agrégations
- ✅ **ADO.NET & MySql.Data** : connexions, commandes paramétrées, DataAdapters
- ✅ **Windows Forms** : conception d'interfaces, événements, validation
- ✅ **Gestion des Exceptions** : try-catch, logging, messages utilisateurs
- ✅ **Sécurité** : prévention des injections SQL, gestion des connexions

### Méthodologiques

- 📊 **Analyse des Besoins** : compréhension du domaine métier
- 🎨 **Conception UML** : diagrammes de classes, modèle ER
- 🔄 **Gestion de Projet** : planification, versioning Git
- 🐛 **Debugging** : utilisation du debugger Visual Studio
- 📝 **Documentation** : code commenté, README structuré

### Transversales

- 🧩 **Résolution de Problèmes** : décomposition de problèmes complexes
- 🔍 **Attention aux Détails** : validation des données, gestion des cas limites
- ⚡ **Optimisation** : requêtes efficaces, gestion de la mémoire
- 🎯 **Orientation Utilisateur** : interfaces intuitives, retours visuels

---

## 🔮 Perspectives d'Amélioration

### Court Terme

- [ ] **Système de Reporting** : génération de PDF pour factures et paiements
- [ ] **Chiffrement des Mots de Passe** : implémentation de bcrypt/SHA256
- [ ] **Validation Avancée** : expressions régulières pour email/téléphone
- [ ] **Gestion des Erreurs Centralisée** : logger les exceptions

### Moyen Terme

- [ ] **Architecture 3-tiers** : séparation stricte des couches
- [ ] **API REST** : exposition des services pour applications mobiles
- [ ] **Gestion des Rôles** : administrateur, opérateur, technicien
- [ ] **Tableaux de Bord** : statistiques et KPIs en temps réel
- [ ] **Notifications** : alertes pour factures impayées, interventions urgentes

### Long Terme

- [ ] **Migration vers .NET Core** : application cross-platform
- [ ] **Application Web** : ASP.NET Core MVC ou Blazor
- [ ] **Application Mobile** : Xamarin/MAUI pour techniciens sur terrain
- [ ] **Intelligence Artificielle** : prédiction de pannes, optimisation des tournées
- [ ] **Intégration IoT** : relevés automatiques des compteurs connectés

---

## 🎓 Contexte Académique

### Projet de Fin d'Études (PFE)

- **Année** : 2023-2024
- **Institution** : [Votre Université/École]
- **Filière** : Informatique / Génie Logiciel
- **Durée** : [X] mois
- **Encadrement** : [Nom de l'encadrant]

### Objectifs Atteints

✅ Maîtrise du développement d'applications desktop professionnelles  
✅ Conception et implémentation d'une base de données relationnelle complexe  
✅ Application des bonnes pratiques de programmation  
✅ Gestion complète d'un projet logiciel de A à Z  
✅ Résolution de problèmes techniques et organisationnels

---

## 📚 Documentation Technique

### Classes Principales

#### `databasehelper.cs` - Gestionnaire de Base de Données

```csharp
public static class databasehelper
{
    public static MySqlConnection GetConnection()
    public static DataTable GetHospitalIDs()
    public static void GetClientId(ComboBox comboBox)
    public static string GetClienyName(int patientId)
    // ... autres méthodes utilitaires
}
```

**Rôle** : Centralise toutes les opérations d'accès aux données, garantissant la réutilisabilité et la sécurité.

#### Pattern Utilisé : Singleton-like

- Connexion unique et centralisée
- Méthodes statiques réutilisables
- Gestion cohérente des exceptions

---

## 🤝 Contribution

Ce projet étant un projet académique, les contributions ne sont pas acceptées. Cependant, n'hésitez pas à :

- 🐛 **Signaler des bugs** via les Issues GitHub
- 💡 **Proposer des améliorations** conceptuelles
- ⭐ **Star le projet** si vous le trouvez intéressant

---

## 📄 Licence

Ce projet est développé dans un cadre **académique** et est partagé à des fins **éducatives** uniquement.  
© 2024 Mohammed Belmekki - Tous droits réservés.

---

## 📞 Contact

**Mohammed Belmekki**  
🎓 Candidat Master en Informatique - France  
📧 Email : [votre.email@example.com]  
🔗 LinkedIn : [linkedin.com/in/mohammed-belmekki](https://linkedin.com/in/mohammed-belmekki)  
💻 GitHub : [github.com/MohammedBelmekki01](https://github.com/MohammedBelmekki01)  
🌐 Portfolio : [votre-portfolio.com]

---

## 🙏 Remerciements

- **Encadrant académique** : [Nom] pour ses conseils précieux
- **MySQL Community** : pour la documentation complète
- **Microsoft Docs** : pour les ressources C# et .NET
- **Stack Overflow Community** : pour le support technique

---

<div align="center">

### ⭐ Si ce projet vous intéresse, n'hésitez pas à le mettre en favoris !

**Développé avec passion pour démontrer mes compétences en ingénierie logicielle** 🚀

---

_README rédigé avec ❤️ pour une candidature Master en France_

</div>
