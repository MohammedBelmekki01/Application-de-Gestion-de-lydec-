# Application de Gestion de Lydec

## Description
Cette application est un système de gestion complet développé pour Lydec, permettant de gérer efficacement les équipes, les projets, les ressources et les clients.

## Fonctionnalités Principales

### Gestion des Employés
- Suivi détaillé des informations personnelles
- Gestion des rôles et permissions
- Suivi des affectations aux projets
- Historique des performances

### Gestion des Projets
- Création et suivi des projets
- Attribution des ressources
- Gestion des budgets
- Suivi de l'avancement
- Gestion des délais

### Gestion des Ressources
- Inventaire du matériel
- Suivi de l'utilisation
- Maintenance préventive
- Allocation aux projets

### Gestion des Chantiers
- Suivi des chantiers en temps réel
- Gestion des équipes sur site
- Suivi des matériaux utilisés
- Rapports de progression

### Gestion Géographique
- Localisation des chantiers
- Visualisation sur carte
- Gestion des zones d'intervention

### Gestion Clientèle
- Base de données clients
- Historique des services
- Gestion des contrats
- Suivi des paiements

### Gestion des Documents
- Stockage centralisé
- Classification par projet/client
- Contrôle d'accès
- Versioning

### Rapports et Analyses
- Tableaux de bord personnalisés
- Génération de rapports automatiques
- Statistiques en temps réel
- Export des données

## Technologies Utilisées

### Backend
- **Framework**: Laravel 10
- **Base de données**: MySQL
- **API**: RESTful

### Frontend
- **CSS Framework**: Bootstrap 5
- **JavaScript**: Vanilla JS
- **Icons**: Font Awesome

### Outils de Développement
- **Version Control**: Git
- **Package Manager**: Composer, npm

## Structure de la Base de Données

### Tables Principales
- `employees` - Informations des employés
- `projects` - Données des projets
- `resources` - Matériel et équipements
- `sites` - Chantiers
- `wilayas` - Divisions géographiques
- `clients` - Informations clients
- `contracts` - Contrats
- `documents` - Documents associés
- `payments` - Historique des paiements

## Installation

### Prérequis
- PHP >= 8.1
- Composer
- MySQL >= 5.7
- Node.js & npm

### Étapes d'installation

Cloner le repository
```bash
git clone [url-du-repo]
cd Application-de-Gestion-de-lydec-
```

Installer les dépendances PHP
```bash
composer install
```

Installer les dépendances JavaScript
```bash
npm install
```

Configurer l'environnement
```bash
cp .env.example .env
php artisan key:generate
```

Configurer la base de données dans le fichier `.env`
```
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=lydec_db
DB_USERNAME=your_username
DB_PASSWORD=your_password
```

Exécuter les migrations
```bash
php artisan migrate
```

Lancer le serveur de développement
```bash
php artisan serve
```

## Utilisation

### Authentification
L'application dispose d'un système d'authentification sécurisé avec différents niveaux d'accès selon les rôles.

### Navigation
- **Dashboard**: Vue d'ensemble de toutes les activités
- **Employés**: Gestion complète du personnel
- **Projets**: Création et suivi des projets
- **Ressources**: Gestion du matériel
- **Chantiers**: Suivi des sites de travail
- **Clients**: Gestion de la base clients
- **Rapports**: Génération et consultation des rapports

## Sécurité
- Authentification robuste
- Protection CSRF
- Validation des données
- Contrôle d'accès basé sur les rôles
- Chiffrement des données sensibles

## Contribution

Les contributions sont les bienvenues ! Pour contribuer :
1. Fork le projet
2. Créer une branche pour votre fonctionnalité
3. Commit vos changements
4. Push vers la branche
5. Ouvrir une Pull Request

## Bonnes Pratiques
- Suivre les conventions de code Laravel
- Écrire des tests pour les nouvelles fonctionnalités
- Documenter les changements importants
- Respecter les principes SOLID

## Améliorations Futures
- Intégration d'un système de notifications en temps réel
- Application mobile complémentaire
- Tableaux de bord plus avancés avec graphiques interactifs
- Intégration avec d'autres systèmes de Lydec
- Module de gestion de la maintenance prédictive

## Support et Documentation
Pour toute question ou problème, veuillez consulter la documentation complète ou contacter l'équipe de développement.

## Auteur
Mohammed Belmekki

## Remerciements
Merci à l'équipe Lydec pour leur confiance et leur collaboration tout au long du développement de cette application.

## Statut du Projet
En développement actif

---
Développé avec passion pour Lydec