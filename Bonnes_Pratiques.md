# Bonnes Pratiques pour les Scripts Bash

Avant de commencer à automatiser la configuration, voici un rappel des **bonnes pratiques** à suivre lors de la création de scripts Bash :

### 1. **Nommage des Variables et Fonctions**
   - Utilisez des noms explicites et en majuscules pour les variables d'environnement (ex. `CONFIG_FILE`).
   - Privilégiez les noms de fonctions qui décrivent clairement leur objectif (ex. `secure_ssh_config`).
   - Evitez d’utiliser des noms réservés par le shell ou des noms ambigus.

### 2. **Vérification des Entrées Utilisateur**
   - Validez toutes les **entrées utilisateur** avant de les utiliser dans le script pour éviter les erreurs ou les vulnérabilités.
   - Utilisez des messages d'erreur clairs et explicites si une entrée est incorrecte ou manquante.

### 3. **Utilisation de Fichiers Sourcés**
   - Placez les différentes fonctions dans des fichiers séparés pour maintenir une **modularité** et faciliter la maintenance du code.
   - Utilisez des commentaires clairs pour décrire l’objectif de chaque fonction.
   - Dans le script principal, **sourcez** les fichiers en vérifiant leur existence et leur accessibilité avant de les exécuter.

### 4. **Gestion des Permissions**
   - Assurez-vous que les fichiers et dossiers créés ont les **permissions appropriées**. Des permissions trop permissives peuvent être une faille de sécurité.
   - Vérifiez et ajustez les permissions des fichiers sensibles comme les clés SSH, les fichiers de configuration ou les journaux.

### 5. **Gestion des Erreurs**
   - Utilisez `set -e` pour arrêter le script en cas d’erreur non gérée.
   - Traitez les erreurs de manière explicite avec des messages clairs.
   - Chaque fonction doit renvoyer un statut de succès ou d’échec (`0` pour succès, `1` pour échec) et documenter ses points de sortie.

### 6. **Sécurisation du Script**
   - Évitez l'exécution de commandes avec des **entrées non vérifiées**.
   - Utilisez `$(...)` pour exécuter des commandes plutôt que des backticks `` `...` ``.
   - Réduisez les privilèges **root** au strict minimum. Évitez d'exécuter tout le script avec des privilèges administrateur si ce n'est pas nécessaire.

## Structure des Scripts : Sourcer des Fonctions

Pour maintenir un code **organisé** et **facile à maintenir**, le script principal devra **sourcer** plusieurs fichiers qui contiendront les différentes fonctions de configuration. Voici un schéma conceptuel de la structure à adopter :

### Schéma de la Gestion des Fichiers Sourcés

```
main_script.sh
  ├── functions/
  │   ├── ssh_hardening.sh       # Durcissement de SSH
  │   ├── firewall_setup.sh       # Installation et configuration du pare-feu UFW
  │   ├── user_management.sh      # Gestion des utilisateurs
  │   └── log_management.sh       # Configuration des logs de sécurité
  └── config/
      └── config_file.sh          # Fichier de configuration pour stocker les variables globales
```

### 1. **Script Principal** (`main_script.sh`)
   - Ce script sera l’entrée principale du projet. Il devra **sourcer** les fonctions nécessaires à partir des fichiers placés dans le dossier `functions/`.
   - Il vérifiera que tous les fichiers de configuration et de fonctions sont bien disponibles avant de les exécuter.

### 2. **Gestion des Fichiers Sourcés**
   - **Fonctions** : Chaque fichier dans le répertoire `functions/` contiendra une ou plusieurs fonctions spécifiques à une tâche précise (par exemple, durcir SSH, configurer UFW).
   - **Configuration** : Un fichier dans le dossier `config/` stockera les variables globales que vous pourrez réutiliser dans les différentes fonctions (exemple : chemins des fichiers de logs, utilisateurs autorisés à utiliser SSH).

### Exemple de Sourçage de Fichiers dans le Script Principal

```bash
#!/bin/bash

# Chargement des fonctions depuis les fichiers sourcés
source ./functions/ssh_hardening.sh || { echo "Erreur : Impossible de sourcer ssh_hardening.sh"; exit 1; }
source ./functions/firewall_setup.sh || { echo "Erreur : Impossible de sourcer firewall_setup.sh"; exit 1; }
source ./config/config_file.sh || { echo "Erreur : Impossible de charger le fichier de configuration"; exit 1; }

# Fonction principale qui appelle les différentes fonctions de durcissement
main(){
  echo "Démarrage du processus d'automatisation et de durcissement..."
  
  secure_ssh
  setup_firewall
  manage_users

  echo "Processus terminé avec succès."
}

# Appel de la fonction principale
main
```

### 3. **Gestion des Entrées Utilisateur**
   Lors de la configuration, vous devrez souvent demander des informations à l'utilisateur, comme son adresse IP ou son nom d'utilisateur pour SSH. Voici comment vous devrez gérer ces entrées :

- **Validation des entrées** : Assurez-vous que les informations fournies par l'utilisateur sont valides (par exemple, vérifier que l'adresse IP est bien formatée).
- **Valeurs par défaut** : Proposez des valeurs par défaut que l’utilisateur pourra accepter ou modifier.
- **Gestion des erreurs** : En cas d’erreur d’entrée, affichez un message d’aide expliquant comment corriger l’entrée.

### Exemple de Gestion d'Entrées Utilisateur

```bash
read -p "Entrez l'adresse IP autorisée pour SSH (ou laissez vide pour utiliser l'adresse par défaut) : " USER_IP
USER_IP=${USER_IP:-"192.168.0.1"}

# Vérification de l'adresse IP
if [[ ! "$USER_IP" =~ ^[0-9]+\.[0-9]+\.[0-9]+\.[0-9]+$ ]]; then
  echo "Erreur : Adresse IP non valide"
  exit 1
fi

echo "Adresse IP $USER_IP autorisée pour SSH"
```


