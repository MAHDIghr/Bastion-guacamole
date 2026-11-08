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
