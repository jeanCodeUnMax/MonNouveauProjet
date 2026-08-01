# Explication détaillée de chaque point

## 1. Création des notebooks Google Colab

Les notebooks Colab serviront de conteneurs principaux.  
Chaque notebook doit contenir :
- Les imports nécessaires
- Les scripts LamaCCP intégrés directement ou via fichiers
- Des cellules claires pour chaque étape (connexion, activation, exécution, arrêt)

Objectif : avoir un environnement prêt à l’emploi pour maximiser les 5 heures GPU gratuites.

## 2. Inclusion des scripts LamaCCP

LamaCCP regroupe le code de contrôle (Custom Control Prompt ou équivalent).  
Il gère :
- Le chargement des modèles
- Les prompts dynamiques
- Les manifests

Les scripts doivent être versionnés et appelables facilement depuis le notebook.

## 3. Activation

Fonction d’activation qui :
- Connecte le GPU/TPU
- Charge les manifests
- Initialise la mémoire unifiée
- Lance l’agent de supervision

Exemple attendu : `activate_lama_ccp()`

## 4. Désactivation

Fonction de désactivation qui :
- Sauvegarde l’état courant
- Libère les ressources GPU
- Ferme proprement la session
- Met à jour les manifests pour la prochaine session

Exemple attendu : `deactivate_lama_ccp()`

## 5. Création des manifests

Les manifests sont des fichiers de configuration (JSON ou YAML) qui :
- Décrivent l’état de la mémoire unifiée
- Stockent les checkpoints et contextes
- Permettent de reprendre exactement là où on s’est arrêté entre deux sessions

Ils doivent être persistés sur Google Drive ou dans le dépôt.

## 6. Mémoire unifiée entre sessions

Objectif : que le contexte, les variables et les états des modèles restent cohérents d’une session Colab à l’autre.  
Les manifests + sauvegarde Drive + rechargement automatique assurent cette continuité.

## 7. Optimisation GPU – Startup

Au démarrage :
- Détection rapide du runtime
- Chargement minimal des ressources nécessaires
- Initialisation différée des modèles lourds
- Vérification du quota restant

## 8. Optimisation GPU – Shutdown

À l’arrêt :
- Sauvegarde immédiate de l’état
- Libération complète du GPU
- Logging du temps consommé
- Préparation du prochain démarrage

---
*Document de référence pour le découpage en issues et sous-tâches*
