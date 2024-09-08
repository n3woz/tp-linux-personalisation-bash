# Automatisation et Durcissement d’un Système Debian avec Bash

## Introduction

L'objectif de ce TP est de **sécuriser** et **automatiser** la configuration initiale d'un système Debian. 

Vous créerez un **script Bash** qui centralisera toutes les opérations de durcissement, en veillant à ce que le processus soit **automatisé** et **fiable**. 

Le script principal devra **sourcer des fonctions** spécifiques depuis d'autres fichiers pour maintenir un code clair et modulaire. De plus, vous devrez porter une attention particulière aux **inputs utilisateurs** et à la gestion des fichiers.

N'oubliez pas d'**anticiper les erreurs** et de vérifier systématiquement que tous les fichiers et fonctions requis sont accessibles et fonctionnels avant de procéder.

Exemple : https://sbnsec.fr/linux.sh

## Objectifs

- **Automatiser** la configuration initiale de la sécurité.
- **Durcir** les configurations essentielles, comme SSH et les services.
- **Personnaliser** l’environnement de travail pour le rendre plus adapté à vos usages.
- **Proposer des idées** novatrices et utiles pour améliorer la sécurité et l’ergonomie de votre système.

## Étapes du TP

### 1. Copie de la Clé SSH

Vous devrez automatiser la copie de votre clé SSH publique dans le fichier `~/.ssh/authorized_keys` de manière sécurisée. Assurez-vous de configurer les permissions du fichier de manière adéquate pour empêcher tout accès non autorisé.

### 2. Durcissement de SSH

L’objectif est de configurer votre service SSH pour le rendre plus sûr. Vous devrez :
- **Désactiver l'authentification par mot de passe** pour forcer l'utilisation des clés SSH.
- **Limiter l'accès SSH** à certains utilisateurs ou groupes.
- **Désactiver l'accès root** via SSH pour éviter des tentatives d'intrusion sur ce compte sensible.
- **Utilisation d’une Liste Blanche d’Adresses IP pour SSH**  Pour une sécurité renforcée, autorisez uniquement des plages d'adresses IP spécifiques à se connecter via SSH. Cette liste blanche limite l'accès à des sources fiables.

### 3. Installation et Configuration d’un Pare-feu (UFW)

Installez un pare-feu (UFW) et configurez-le pour permettre uniquement les connexions nécessaires (comme SSH, HTTP, HTTPS). Vous devrez :
- **Installer et activer UFW**.
- **Configurer les règles par défaut** pour bloquer tout le trafic entrant sauf les services essentiels.
- **Autoriser** les connexions nécessaires, comme SSH ou les serveurs web si applicable.

   ### 4. Propositions de Durcissement Simples

Voici des propositions pour renforcer la sécurité de votre système. Chaque proposition doit être documentée avec précision pour que vous compreniez comment elle renforce la sécurité et dans quel contexte elle est applicable.

- **Mise en Place d’Authentification à Deux Facteurs (2FA)**  
   Ajoutez une deuxième couche de sécurité en configurant une authentification à deux facteurs pour SSH. Cela nécessite une confirmation supplémentaire pour accéder au système, généralement via une application d'authentification mobile.

- **Mise à Jour Automatique des Paquets de Sécurité**  
   Configurez le système pour qu’il télécharge et installe automatiquement les mises à jour de sécurité afin de ne jamais manquer une correction importante. Cela garantit que votre système reste à jour sans intervention manuelle.

- **Désactivation des Services Inutiles**  
   Tous les services réseau actifs doivent être absolument nécessaires. Identifiez et désactivez tous les services qui ne sont pas requis pour réduire les points d'attaque potentiels.

- **Détection des Modifications dans les Fichiers Système**  
   Utilisez des outils comme `AIDE` ou `Tripwire` pour surveiller les fichiers critiques du système et être alerté en cas de modification non autorisée. Ces outils peuvent aider à identifier les intrusions et les altérations de fichiers.

### 5. Personnalisation et Suggestions de Fonctionnalités

En plus de sécuriser votre système, l’objectif est de personnaliser votre environnement de travail pour le rendre plus efficace et agréable à utiliser. Voici quelques idées à implémenter :

- **Alias pour Commandes Fréquentes**  : Créez des alias dans votre `.bashrc` pour les commandes que vous utilisez régulièrement. Par exemple, créer un alias pour une commande longue et répétitive permet de gagner du temps.

- **Scripts d'Automatisation Personnalisés**  : Développez des scripts pour automatiser des tâches récurrentes, comme la mise à jour des paquets, la surveillance de l’espace disque, ou l’archivage de logs.

- **Prompt Bash Personnalisé** : Modifiez votre invite de commande (`PS1`) pour inclure des informations utiles, comme le répertoire courant, l’heure, ou l’état du dépôt Git sur lequel vous travaillez. Cela peut améliorer votre productivité en vous donnant des informations en un coup d'œil.

- **Synchronisation Automatique de Répertoires** : Configurez des scripts pour synchroniser automatiquement vos dossiers de travail entre différentes machines à l'aide de `rsync`. Cela peut être utile si vous travaillez sur plusieurs environnements.

- **Intégration de Notifications Système** : Intégrez des notifications système qui vous alertent lorsqu’une tâche longue est terminée (comme une compilation ou une sauvegarde). Cela vous permet de continuer à travailler sur autre chose sans avoir à vérifier constamment l’état de vos processus.

### Suggestions d'Idées Supplémentaires

Poussez encore plus loin la personnalisation et la sécurisation en réfléchissant à d’autres fonctionnalités ou scripts qui pourraient améliorer votre système. 
Réfléchissez aux tâches que vous effectuez souvent, aux aspects de la sécurité que vous pourriez renforcer, ou aux améliorations que vous aimeriez avoir dans votre environnement de travail. Soyez créatifs !
