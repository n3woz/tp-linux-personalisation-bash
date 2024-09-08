# Grille de Notation pour le TP : Automatisation et Durcissement d’un Système Debian

## Obligatoire (Total : 15 points)

### 1. **Copie de la Clé SSH** (5 points)
- Automatisation correcte et sécurisée de la copie de la clé SSH publique.
- Gestion appropriée des permissions des fichiers.
- Bonne gestion des erreurs en cas d’échec ou d’entrée utilisateur incorrecte.

### 2. **Durcissement de SSH** (5 points)
- Désactivation de l'authentification par mot de passe.
- Limitation de l'accès SSH à des utilisateurs spécifiques.
- Désactivation de l'accès root via SSH.
- Utilisation d'une liste blanche d'adresses IP.

### 3. **Installation et Configuration d’un Pare-feu (UFW)** (5 points)
- Installation correcte de UFW.
- Configuration des règles par défaut pour bloquer le trafic non autorisé.
- Autorisation des connexions nécessaires (SSH, HTTP, HTTPS si applicable).
- Gestion appropriée des erreurs et des permissions.

## Au Choix (Total : 10 points - minimum un point à choisir)

### 4. **Propositions de Durcissement Simples** (jusqu’à 10 points)
- Mise en place de l'authentification à deux facteurs (2FA).
- Mise à jour automatique des paquets de sécurité.
- Désactivation des services inutiles.
- Surveillance des fichiers critiques avec AIDE ou Tripwire.

### 5. **Personnalisation et Suggestions de Fonctionnalités** (jusqu’à 10 points)
- Création d'alias pour des commandes fréquentes.
- Développement de scripts d'automatisation personnalisés.
- Personnalisation du prompt Bash.
- Synchronisation automatique des répertoires.
- Intégration de notifications système.

## Bonus (jusqu’à 5 points)

### **Suggestions d'Idées Supplémentaires**
- Implémentation d’idées créatives supplémentaires en lien avec la sécurité ou l’automatisation.
- Innovations qui montrent une réflexion personnelle et avancée dans la personnalisation ou la sécurité du système.

## Critères de Réussite

- **Respect des bonnes pratiques** : clarté du code, commentaires, modularité avec le sourçage des fonctions.
- **Gestion des erreurs** : traitement des erreurs d’exécution, gestion des entrées utilisateur.
- **Originalité et innovation** : capacité à proposer des solutions originales et adaptées aux besoins des utilisateurs.
  
## Barème Total

| Critère                                   | Points Disponibles |
| ----------------------------------------- | ------------------ |
| Obligatoire (1, 2, 3)                     | 15                 |
| Au choix (4, 5)                           | 10                 |
| Bonus                                     | 5                  |
| **Total**                                 | **30**             |
