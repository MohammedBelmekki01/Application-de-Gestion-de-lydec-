# Gestion LYDEC -- Application de Bureau

Projet de Fin d'Annee (PFA) -- 2024

Application de gestion pour la societe LYDEC (Lyonnaise des Eaux de Casablanca), developpee en C# Windows Forms avec une base de donnees MySQL. Elle permet la gestion complete des clients, des compteurs, de la facturation, des paiements, des techniciens et de leurs interventions.

---

## Table des matieres

1. [Apercu du projet](#apercu-du-projet)
2. [Fonctionnalites](#fonctionnalites)
3. [Architecture technique](#architecture-technique)
4. [Schema de la base de donnees](#schema-de-la-base-de-donnees)
5. [Prerequis](#prerequis)
6. [Installation et mise en route](#installation-et-mise-en-route)
7. [Structure du projet](#structure-du-projet)
8. [Captures d'ecran](#captures-decran)

---

## Apercu du projet

L'application offre une interface graphique permettant a un administrateur de gerer l'ensemble des operations courantes de LYDEC :

- Enregistrement et suivi des villes et quartiers desservis
- Gestion du fichier clients (coordonnees, rattachement a un quartier)
- Suivi des compteurs installes chez les clients
- Edition et consultation des factures
- Enregistrement des paiements
- Gestion des techniciens et de leurs interventions sur les compteurs
- Systeme d'authentification par identifiant et mot de passe

---

## Fonctionnalites

### Authentification
- Ecran de connexion avec verification des identifiants en base de donnees
- Afficher/masquer le mot de passe

### Gestion des Villes
- Ajouter, modifier, supprimer et rechercher des villes
- Affichage en grille (DataGridView)

### Gestion des Quartiers
- Ajouter, modifier, supprimer et rechercher des quartiers
- Association automatique a une ville existante (cle etrangere)

### Gestion des Clients
- Enregistrement complet : nom, prenom, adresse, telephone, email
- Rattachement a un quartier
- Recherche de clients avec jointures sur Quartier et Ville

### Gestion des Compteurs
- Enregistrement des compteurs (date d'installation, type)
- Association a un client
- Recherche avec affichage des informations client et localisation

### Gestion des Factures
- Creation de factures (date, montant, statut de paiement, type de service)
- Liaison au compteur concerne
- Recherche avec jointures completes jusqu'a la ville

### Gestion des Paiements
- Enregistrement des paiements (date, montant)
- Liaison a une facture existante
- Consultation avec toute la chaine : paiement, facture, compteur, client, quartier, ville

### Gestion des Techniciens
- Ajout, modification et suppression de techniciens (nom, prenom, specialite)
- Affichage de la liste des techniciens

### Gestion des Interventions
- Enregistrement des interventions (date, description)
- Association a un compteur et a un technicien
- Recherche filtree par compteur et technicien avec jointures completes

### Navigation
- Menu lateral permettant d'acceder a chaque module (Ville, Quartier, Client, Service Client, Compteur, Facture, Paiement, Technicien, Intervention)
- Bouton de deconnexion pour revenir a l'ecran de connexion

---

## Architecture technique

| Composant        | Technologie                          |
|------------------|--------------------------------------|
| Langage          | C# (.NET Framework 4.7.2)           |
| Interface        | Windows Forms (WinForms)             |
| Base de donnees  | MySQL 8.x                           |
| Connecteur BDD   | MySql.Data 8.4.0 (MySQL Connector/NET) |
| IDE              | Visual Studio (solution .sln)        |

L'application suit une architecture simple a deux couches :
- Une couche d'acces aux donnees centralisee dans la classe `databasehelper`, qui fournit la connexion MySQL et des methodes utilitaires pour charger les listes deroulantes et recuperer les noms associes aux identifiants.
- Une couche presentation composee de formulaires Windows Forms, chacun correspondant a un module fonctionnel.

---

## Schema de la base de donnees

La base `simolydec` contient les tables suivantes :

```
Ville (Id_ville, nom_ville)
  |
  v
Quartier (Id_quartier, nom_quartier, code_postal, Id_ville, nom_ville)
  |
  v
Client (Id_client, nom, prenom, adresse, telephone, email, Id_quartier, nom_quartier)
  |
  +---> Service_Client (Id_service, date_demande, description_demande, statut, client_id, name_patient)
  |
  v
Compteur (Id_compteur, date_installation, type, Id_client, nom)
  |
  +---> Intervention_Technicien (id_intervention, date_intervention, description, Id_compteur, Id_technicien, nom)
  |
  v
Facture (Id_facture, date_facturation, montant, statut_paiement, type_service, Id_compteur)
  |
  v
Paiement (Id_paiement, date_paiement, montant_paiement, id_facture)

Technicien (id_technicien, nom, prenom, specialite)

simo (editor, password) -- table d'authentification
```

Relations :
- Quartier -> Ville (Id_ville)
- Client -> Quartier (Id_quartier)
- Service_Client -> Client (client_id)
- Compteur -> Client (Id_client)
- Facture -> Compteur (Id_compteur)
- Paiement -> Facture (id_facture)
- Intervention_Technicien -> Compteur (Id_compteur)
- Intervention_Technicien -> Technicien (id_technicien)

---

## Prerequis

- Windows 7 ou superieur
- .NET Framework 4.7.2
- MySQL Server 8.x installe et en cours d'execution
- Visual Studio 2017 ou superieur (pour la compilation)

---

## Installation et mise en route

1. Cloner le depot :
   ```
   git clone https://github.com/<votre-utilisateur>/gestion-lydec.git
   ```

2. Creer la base de donnees MySQL en executant le script SQL fourni :
   ```
   mysql -u root -p < datz.sql
   ```
   Ce script cree la base `simolydec` et toutes les tables necessaires. Il insere egalement un compte administrateur par defaut (identifiant : `simo`, mot de passe : `123456789`).

3. Configurer la connexion a la base de donnees :
   Ouvrir le fichier `simofinal/simofinal/databasehelper.cs` et modifier la chaine de connexion si necessaire :
   ```csharp
   private static string connectionString = "server=localhost;user id=root;password=VOTRE_MOT_DE_PASSE;database=simolydec";
   ```

4. Ouvrir la solution dans Visual Studio :
   ```
   simofinal/simofinal.sln
   ```

5. Restaurer les packages NuGet (clic droit sur la solution > Restaurer les packages NuGet).

6. Compiler et executer le projet (F5).

7. Se connecter avec les identifiants par defaut :
   - Identifiant : `simo`
   - Mot de passe : `123456789`

---

## Structure du projet

```
pfesimo/
|-- datz.sql                        Script de creation de la base de donnees
|-- IMAGElYDEC/                     Images et icones de l'interface
|-- imagepfe/                       Captures d'ecran du projet
|-- simofinal/
    |-- simofinal.sln               Fichier solution Visual Studio
    |-- packages/                   Packages NuGet (MySql.Data, etc.)
    |-- simofinal/
        |-- Program.cs              Point d'entree de l'application
        |-- databasehelper.cs       Classe d'acces aux donnees (connexion MySQL, methodes utilitaires)
        |-- loginhome.cs            Formulaire d'authentification
        |-- Form1.cs                Page d'accueil -- gestion des villes + navigation
        |-- Quartier.cs             Gestion des quartiers
        |-- Client.cs               Gestion des clients
        |-- Service_Client.cs       Gestion des demandes de service client
        |-- Compteur.cs             Gestion des compteurs
        |-- Facture.cs              Gestion des factures
        |-- Paiement.cs             Gestion des paiements
        |-- echnoque.cs             Gestion des techniciens
        |-- Intervention_Technicien.cs  Gestion des interventions
        |-- App.config              Configuration de l'application (.NET)
        |-- packages.config         Liste des packages NuGet
        |-- Properties/             Proprietes du projet (AssemblyInfo, Resources, Settings)
        |-- bin/                    Fichiers compiles
        |-- obj/                    Fichiers intermediaires de compilation
```

---

## Captures d'ecran

Les captures d'ecran de l'application sont disponibles dans les dossiers `IMAGElYDEC/` et `imagepfe/`.

Parmi les ecrans disponibles :
- Ecran de connexion
- Page d'accueil (gestion des villes)
- Gestion des quartiers
- Gestion des clients
- Gestion des compteurs
- Gestion des factures
- Gestion des paiements
- Gestion des techniciens
- Gestion des interventions

---

## Remarques

- Ce projet a ete realise dans le cadre d'un Projet de Fin d'Annee (PFA) en 2024.
- L'application est concue pour un usage local (localhost). Pour un deploiement en reseau, il faut adapter la chaine de connexion dans `databasehelper.cs`.
- Les identifiants par defaut sont stockes en clair dans la base de donnees. Pour un usage en production, il est recommande de mettre en place un mecanisme de hachage des mots de passe.


demo form de application de lydec :

<img width="1500" height="828" alt="inter" src="https://github.com/user-attachments/assets/755a3d72-a540-443d-885a-af7396cda552" />

