Contexte
Les administrateurs accèdent actuellement aux serveurs et aux différentes infrastructures au moyen de leurs connexions VPN, puis réalisent des connexions ou des rebonds directs vers les ressources à administrer, notamment en SSH.

Ce fonctionnement ne permet pas de centraliser suffisamment les accès administrateurs ni de disposer d’une traçabilité complète, homogène et facilement exploitable des opérations réalisées. Il existe également plusieurs possibilités de rebond latéral depuis certains outils ou serveurs techniques disposant eux-mêmes d’un accès aux infrastructures.

Objectif
Mettre en place un Bastion basé sur Apache Guacamole afin de centraliser, sécuriser et tracer les accès d’administration aux infrastructures.

Le périmètre initial couvre les accès SSH, RDP et Kubernetes. La solution vise également à limiter les accès directs et les possibilités de contournement du Bastion, tout en garantissant une gestion maîtrisée des habilitations et une traçabilité complète des connexions et des sessions.

But
Centraliser les connexions d’administration à travers un bastion sécurisé et rendre les accès directs ou les rebonds alternatifs non autorisés incompatibles avec le dispositif cible. La mise en place du Bastion Guacamole va également contribuer à répondre aux exigences de certification associées à GenIA-L 1.5

 

Une première version du DAS est également disponible : 
BASTIONXXX - Technical architecture 




Objectif du ticket

Finaliser et valider opérationnellement le POC, piloter la mise en place du Bastion Guacamole avec la création des environnements de PPD et PROD , tout en coordonnant les actions nécessaires pour sécuriser le parcours des accès d’administration et empêcher le contournement du bastion.


voici les sous taches que j'ai actuellement : 
<img width="342" height="332" alt="image" src="https://github.com/user-attachments/assets/84959c9c-de11-4936-b859-221dd8f4f4bc" />



voici le decoupage initial  : 

PBS

Projet : Bastion Apache Guacamole
│
├── Infrastructure pour chaque ENV (PPD/PROD) (ENV POC déjà réalisé) 
│   ├── Serveur Bastion - Aly
│   ├── Base de données - aly + qualea
│   ├── Réseau - équipe res
│   └── Certificats SSL
│   ├── Authentification - entra ID (Infra)
│   └ Archi pour les infra dispo sur le DAT 
          
│
├── Plateforme Guacamole
│   ├── Installation (Docker ….) a voir avec un intégrateur
│   ├── Configuration - Aly
│   └── Gestion des accès - Aly
│
├── Sécurité
│   ├── Journalisation - session - envoie vers un S3 (voir avec Dany si besoin)
│   ├── Traçabilité - 
│   └── Durcissement
│
├── Documentation
│   ├── DAT
│   ├── Procédures exploitation
│   └── Support utilisateur
│
└── Mise en production
    ├── Tests
    ├── Validation
    └── Go Live



WBS

1. Cadrage
   1.1 Recueil du besoin
   1.2 Identification des parties prenantes
   1.3 Définition du périmètre
   1.4 Passage ARB Gate 0

2. Conception
   2.1 Architecture cible
   2.2 Schémas d'infrastructure
   2.3 Analyse des risques
   2.4 Validation sécurité

3. Préparation environnement
   3.1 Provisionnement des serveurs
   3.2 Ouverture des flux réseau
   3.3 Certificats
   3.4 DNS

4. Déploiement Guacamole
   4.1 Installation
   4.2 Configuration
   4.3 Connexion AD/LDAP
   4.4 Configuration des profils

5. Sécurité
   5.1 Définition des groupes
   5.2 Gestion des habilitations
   5.3 Journalisation
   5.4 Audits

6. Tests
   6.1 Tests techniques
   6.2 Tests sécurité
   6.3 Recette utilisateur
   6.4 Corrections

7. Mise en production
   7.1 Validation GO
   7.2 Déploiement
   7.3 Vérifications
   7.4 Passage exploitation

8. Clôture
   8.1 Documentation finale
   8.2 Retour d'expérience
   8.3 Fermeture du projet






Tâche 1 :[BASTION] Finaliser le POC
Sous-tâches
Finaliser les tests SSH et RDP
Tester l’accès à Kubernetes (en cours) 
Organiser le point technique avec Aly DARWISH, Julien GANNIER et l’équipe Kubernetes
Déterminer si un serveur de rebond est nécessaire (fort possible)
Tester l’enregistrement des sessions
Tester l’export des sessions vers S3
Documenter les résultats du POC
Valider la fin du POC

Le sujet Kubernetes doit être validé pendant le POC, mais il ne doit pas bloquer le déploiement du bastion pour les accès aux VM.

Tâche 2 :[BASTION] Finaliser l’architecture et le DAT
Sous-tâches
Initialiser le DAT
Décrire l’architecture PPD et PROD
Définir les composants techniques
Compléter les informations VLAN et IP
Documenter les flux réseau
Documenter l’intégration Entra ID
Documenter le stockage S3
Documenter la solution Kubernetes retenue
Faire valider le DAT

Le DAT doit être initié au début du projet puis mis à jour progressivement avec les informations techniques et les décisions d’architecture.

Tâche 3 :[BASTION][PPD] Préparer l’infrastructure
Sous-tâches
Réserver les noms des machines
Réserver les adresses IP
Provisionner le serveur Bastion
Installer et configurer le système d’exploitation
Rattacher le serveur au VLAN approprié
Vérifier les ressources CPU, mémoire et stockage
Mettre à jour les informations dans le DAT

Responsable pressenti : Aly DARWISH

Tâche 4 :[BASTION][PPD] Mettre à disposition la base de données (bloquant)
Sous-tâches
Confirmer le moteur de base de données
Définir le dimensionnement
Demander le provisionnement à l’équipe Qualea
Créer la base Guacamole
Créer le compte de service
Configurer les droits
Tester la connexion depuis le serveur Bastion
Définir les sauvegardes

La base de données doit être traitée comme une dépendance externe, car l’équipe responsable préfère réaliser elle-même l’installation selon ses standards.

Tâche 5 :[BASTION][PPD] Configurer le réseau et les flux (non bloquant)
Sous-tâches
Recenser les flux entrants et sortants
Identifier les IP sources et destinations
Préparer les demandes d’ouverture de flux
Faire contrôler les demandes par l’architecte
Transmettre les demandes à l’équipe Réseau
Tester les flux ouverts
Mettre à jour la matrice des flux dans le DAT

Il faut disposer des machines ou, au minimum, des adresses IP réservées avant de demander l’ouverture des flux.

Tâche 6 :[BASTION][PPD] Configurer l’authentification Entra ID (bloquant)
Sous-tâches
Créer l’application Entra ID
Définir les URL de redirection
Générer les identifiants nécessaires
Configurer le SSO
Activer le MFA
Créer les groupes d’accès
Tester l’authentification
Documenter la configuration
Définir les profils d’utilisation
Créer les groupes dans Guacamole
Définir les rôles et les droits
Mapper les groupes Entra ID avec les groupes Guacamole
Associer les connexions aux groupes
Tester les droits avec plusieurs profils
Vérifier la séparation des accès

Cette configuration correspond à la partie infrastructure d’identité. Le mapping des groupes et des rôles dans Guacamole sera réalisé dans la tâche de configuration de la plateforme.

Tâche 7 :[BASTION][PPD] Installer et configurer Apache Guacamole
Sous-tâches
Valider le mode de déploiement avec l’équipe Intégration (Docker validé avec fehri )
Préparer le déploiement Docker 
Installer Apache Guacamole
Installer et configurer guacd
Connecter Guacamole à la base de données
Configurer la connexion à Entra ID
Configurer les paramètres de session
Configurer les connexions SSH
Configurer les connexions RDP
Tester le fonctionnement de la plateforme
Documenter l’installation

Le POC utilise Docker, mais le mode de déploiement cible doit être validé avec l’équipe Intégration.

Tâche 9 :[BASTION] Configurer la sécurité et la traçabilité
Sous-tâches
Activer les journaux techniques de Guacamole
Collecter les journaux du système
Envoyer les logs vers la plateforme d’observabilité



Tâche 9 :[BASTION] Configurer la sécurité et la traçabilité
Sous-tâches
Activer les journaux techniques de Guacamole
Collecter les journaux du système
Envoyer les logs vers la plateforme d’observabilité
Configurer le tableau de bord Grafana
Activer l’enregistrement des sessions
Configurer l’export des sessions vers S3 (Dany si besoin)
Définir la durée de conservation
Vérifier les droits d’accès aux enregistrements
Tracer les connexions et les échecs d’authentification

Il faut distinguer les journaux techniques, envoyés vers l’observabilité, des enregistrements des sessions, archivés dans S3.


Tâche 10 : [BASTION] Réaliser le durcissement (à terme) 
Sous-tâches
Appliquer le durcissement du système d’exploitation
Désactiver les comptes et services inutiles
Limiter les ports exposés
Sécuriser les comptes de service
Vérifier les versions des composants
Réaliser un scan de vulnérabilités
Corriger les vulnérabilités critiques et élevées
Documenter les exceptions
Faire valider le durcissement

Tâche 11 : [BASTION][PROD] Déployer la plateforme en production
Sous-tâches
Provisionner l’infrastructure PROD
Mettre à disposition la base PROD
Configurer les flux PROD
Configurer l’application Entra ID PROD
Configurer le certificat SSL
Installer Apache Guacamole
Configurer la plateforme
Configurer les groupes et les accès
Configurer la journalisation
Configurer l’enregistrement des sessions
Appliquer le durcissement
Réaliser les tests techniques en PROD

Tâche 12 : [BASTION] Réaliser la documentation
Sous-tâches
Finaliser le DAT
Rédiger la procédure d’installation
Rédiger la procédure d’exploitation
Rédiger la procédure de sauvegarde et restauration
Rédiger la procédure de mise à jour
Rédiger la procédure de rollback
Rédiger le support utilisateur
Préparer le transfert au RUN


Tâche 13 : [BASTION] Réaliser la recette et la mise en production
Sous-tâches
Préparer le cahier de recette
Tester l’authentification et le MFA
Tester les droits et les profils
Tester les connexions SSH et RDP
Tester la journalisation
Tester l’enregistrement des sessions
Corriger les anomalies
Obtenir la validation technique
Obtenir la validation sécurité
Organiser le Go/No Go
Réaliser le Go Live
Réaliser les tests post-déploiement
Démarrer la période de garantie




