# Optimisation des 5 heures GPU gratuites sur Google Colab

Guide complet pour maximiser le temps GPU/TPU gratuit de Colab avec un outil de gestion automatique des sessions.

## Sommaire

- [Pourquoi optimiser ?](#pourquoi-optimiser)
- [Comment ça marche ?](#comment-ça-marche)
- [Installation](#installation)
- [Utilisation](#utilisation)
- [Fonctionnalités](#fonctionnalités)
- [Bonnes pratiques](#bonnes-pratiques)
- [Dépannage](#dépannage)

## Pourquoi optimiser ?

Google Colab offre 5 heures GPU gratuites par session. Une fois la session déconnectée ou inactive trop longtemps, le compteur repart à zéro. L'objectif est de :

- Utiliser le maximum des 5 heures sans gaspiller de temps
- Arrêter automatiquement les sessions inutilisées
- Reconnecter rapidement quand nécessaire
- Optimiser le coût et le temps de développement

## Comment ça marche ?

L'outil se compose de trois parties principales :

1. **Connexion** : Établit la connexion GPU/TPU avec le runtime Colab
2. **Inférence** : Exécute ton code d'entraînement ou d'inférence
3. **Arrêt** : Ferme la session dès que le travail est terminé ou en cas d'inactivité

Cela permet de libérer le quota GPU pour une prochaine utilisation.

## Installation

### Prérequis

- Un compte Google
- Un notebook Colab (`.ipynb`)
- Python 3.x

### Configuration

1. Ouvre un nouveau notebook sur [Google Colab](https://colab.research.google.com/)
2. Va dans `Runtime` > `Change runtime type`
3. Sélectionne `GPU` ou `TPU`
4. Clone ce repo dans ton notebook :

```python
!git clone https://github.com/jeanCodeUnMax/MonNouveauProjet.git
%cd MonNouveauProjet
```

## Utilisation

### Connexion automatique

```python
from colab_manager import connect_gpu

# Connexion au GPU
connect_gpu()
```

### Lancement de l'inférence

```python
from colab_manager import run_inference

# Exécute ton script d'inférence
run_inference("ton_script.py")
```

### Arrêt automatique

```python
from colab_manager import disconnect

# Arrête la session dès que le travail est fini
disconnect()
```

### Workflow complet

```python
# 1. Connexion
from colab_manager import connect_gpu, run_inference, disconnect

connect_gpu()                    # Connecte le GPU
run_inference("train_model.py")  # Lance ton code
disconnect()                     # Arrête et libère le quota
```

## Fonctionnalités

- Détection automatique du type de runtime (GPU/TPU/CPU)
- Arrêt automatique en fin de tâche
- Gestion du timeout d'inactivité
- Reconnexion rapide
- Logging du temps utilisé
- Notification de fin de session

## Bonnes pratiques

1. **Toujours déconnecter** en fin de travail pour libérer le quota
2. **Surveiller l'inactivité** : Colab déconnecte après ~90 minutes d'inactivité
3. **Sauvegarder régulièrement** tes modèles sur Google Drive ou GitHub
4. **Utiliser des checkpoints** pour reprendre l'entraînement si la session coupe
5. **Planifier les sessions** longues en plusieurs runs courts

## Dépannage

### Erreur "No GPU available"

Vérifie le type de runtime dans `Runtime` > `Change runtime type` > `GPU`.

### Session qui se déconnecte trop tôt

Ajoute des cellules actives régulièrement ou utilise `time.sleep()` avec un timer.

### Quota GPU épuisé

Attends 24h ou passe à Colab Pro pour plus de temps.

---

*Créé avec Ara - Optimise tes sessions Colab !*