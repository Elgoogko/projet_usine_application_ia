# Projet Usine

---

## 📋 Table des matières

- Vue d'ensemble
- Stack technique & prérequis
- Structure du projet
- Installation & mise en place
- Déroulement du pipeline
  - 1. Préparation des données
  - 2. Entraînement des modèles
  - 3. Évaluation & métriques
  - 4. Inférence & optimisation
  - 5. Tests
- Qualité du code & linting
- Licence

---

## 📌 Vue d'ensemble

Ce projet vise à détecter et classer les défauts de surface des tôles d'aciérie à partir d'images, à l'aide de techniques de Deep Learning (CNN et modèles de détection type YOLO/Ultralytics). Le pipeline couvre :
- Téléchargement et prétraitement des jeux de données (NEU-DET : six types de défauts annotés ; SKAB pour le volet maintenance des pompes).
- Découpage unique entraînement/validation/test via `tp.decoupage_neu()`, normalisation et augmentation de données.
- Construction et entraînement d'une référence sans deep learning (réglée sérieusement) et de modèles de deep learning, dont un volet au choix : défauts rares (un type réduit à 15 images d'entraînement) ou maintenance prédictive (SKAB).
- Suivi des métriques d'entraînement avec TensorBoard.
- Mesure du temps d'inférence sur CPU (cadence : une image par seconde) et optimisation (quantification, export ONNX ou distillation).
- Plan de suivi en service, tests automatisés et validation du code.

---

## 🛠 Stack technique & prérequis

- **Python** : `>= 3.14`
- **Gestionnaire de paquets & d'environnements** : [`uv`](https://docs.astral.sh/uv/) (installateur et résolveur de paquets Python rapide)
- **Frameworks Deep Learning** : PyTorch, torchvision, Ultralytics (YOLO)
- **Vision par ordinateur & traitement d'images** : OpenCV (`opencv-python-headless`), Pillow
- **Analyse de données & visualisation** : NumPy, Pandas, Scikit-Learn, Matplotlib, Seaborn
- **Notebooks** : Marimo (notebooks du projet dans `projet/`)
- **Développement & tests** : Pytest, Ruff, Pre-commit

---

## 📂 Structure du projet

```text
usine-4.0/
├── README.md                  # Objectif, démarrage rapide, plan du dépôt
├── CONTRIBUTING.md            # Conventions de contribution
├── LICENSE
├── pyproject.toml             # Dépendances + config des outils (ruff, pytest, mypy) par uv
├── .gitignore
├── .gitattributes             # Motifs Git LFS / DVC pour les fichiers lourds
├── .pre-commit-config.yaml
├── .github/
│   └── workflows/ci.yml       # Lint + tests unitaires sur chaque PR
│
├── src/                    # Livrables principaux (versionnés)
│   └── projet_usine/            # scripts
│
├── data/                   # Jamais versionnées brutes : à télécharger manuellement
│   ├── README.md              # Provenance des données, licences, comment les obtenir
│   ├── raw                # Données brutes
│   ├── interim              # données en cours de traitement
│   └── processed              # données finales
│
├── tds/                    # les TDs fait précédemment
|
├── tools/
│   └── tp_utils.py            # Fonctions utilitaires réutilisables dans projet/
│
├── modeles/                   # Non versionné : cache, poids intermédiaires
│
├── notebooks/                 # Exploration uniquement, aucune logique métier
│   └── 01_exploration_donnees.py
│
├── tests/
│   ├── test_donnees.py        # Le découpage train/val/test doit être stable et sans fuite
│   ├── test_modeles.py
│   └── test_inference.py      # Test de fumée sur un petit échantillon
│
└── docs/
    ├── architecture.md
    ├── format_donnees.md      # Classes de défauts, conventions d'annotation
    └── suivi/                 # Notes des réunions hebdomadaires avec l'enseignant
```

---

## 🚀 Installation & mise en place

### 1. Installer `uv`
Si `uv` n'est pas encore installé, installez-le via l'installateur officiel :

- **Windows (PowerShell) :**
  ```powershell
  powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
  ```
- **macOS / Linux :**
  ```bash
  curl -LsSf https://astral.sh/uv/install.sh | sh
  ```

### 2. Cloner le dépôt
```bash
git clone https://github.com/<groupe>/usine-4.0.git
cd usine-4.0
```

### 3. Créer l'environnement virtuel & synchroniser les dépendances
Utilisez `uv` pour créer automatiquement un environnement virtuel avec Python 3.14 et installer toutes les dépendances épinglées depuis `pyproject.toml` / `uv.lock` :

```bash
# Créer l'environnement virtuel et synchroniser toutes les dépendances
uv sync
```

Pour activer l'environnement virtuel :
- **Windows (PowerShell) :**
  ```powershell
  .venv\Scripts\Activate.ps1
  ```
- **macOS / Linux :**
  ```bash
  source .venv/bin/activate
  ```

Alternativement, vous pouvez exécuter n'importe quelle commande directement dans l'environnement avec `uv run <commande>`.

---

### 4. Tests
Exécutez les suites de tests pour garantir l'intégrité du pipeline et la validité des composants :

```bash
uv run pytest tests/
```

---

## 🔄 Déroulement du pipeline

### 1. Préparation des données
- Télécharger NEU-DET sur Kaggle et le placer dans `donnees/NEU/`.
- Utiliser un **seul découpage** pour tout le projet : `tp.decoupage_neu()` (entraînement / validation / test), respecté par `tp.charger_neu()` et `tp.voc_vers_yolo(...)`.
- Ne pas réutiliser tel quel le jeu YOLO du TD 2 (découpage différent).
- Charger SKAB avec `tp.charger_skab()` pour le volet maintenance.

### 2. Entraînement des modèles
- Référence sans deep learning, réglée avec soin (servira de base de comparaison).
- Modèles de deep learning : classification puis détection, ou détecteur seul (au choix, à justifier).
- Volet au choix : défauts rares (un type réduit à **15 images d'entraînement**, validation et test intactes) ou maintenance prédictive sur SKAB (statistiques calculées uniquement sur la partie entraînement).
- Entraînements longs sur CPU : mettre au point sur un sous-ensemble ou à résolution réduite, lancer tôt, sauvegarder les poids.

### 3. Évaluation & métriques
- Tous les choix se font sur la **validation** ; le **test** ne sert qu'une fois, à la fin.
- Méthodes comparées sur les mêmes données, avec la même métrique.
- Résultats analysés **type par type** (une accuracy globale peut cacher un type jamais reconnu).
- Hypothèses de coût écrites (défaut non vu, fausse alerte) et seuils qui en découlent ; un seuil qui maximise le F1 n'est pas forcément le bon.

### 4. Inférence & optimisation
- Temps d'inférence mesuré image par image, sur plusieurs dizaines d'images, sans compter le premier passage, en précisant la machine (PC de la ligne, sans carte graphique).
- Optimisation appliquée (quantification, export ONNX ou distillation) : gain de temps **et** perte de qualité mesurés sur les mêmes images.
- Plan de suivi en service : grandeurs surveillées et seuils d'alerte.

### 5. Testing
- Avant de rendre : cloner le dépôt dans un dossier vide et tout relancer (moins de 15 minutes sur une machine de l'école, à partir des poids et résultats sauvegardés dans `projet/`).

---

## 🧹 Qualité du code & linting

Formater et vérifier le code avec `ruff` :

```bash
# Vérifier les problèmes de lint
uv run ruff check .

# Formater le code
uv run ruff format .
```

Mettre en place les hooks pre-commit :
```bash
uv run pre-commit install
```
---
## 📄 Licence

Ce projet est sous licence MIT - voir le fichier LICENSE pour plus de détails.

## Ressources

- [Modèle de Pull Request](https://gitmore.io/blog/github-pull-request-template)
- [Documentation Ruff](https://docs.astral.sh/ruff/)
- [Documentation Pre-commit](https://pre-commit.com/)
- [Jeu de données NEU-DET (Kaggle)](https://www.kaggle.com/datasets)