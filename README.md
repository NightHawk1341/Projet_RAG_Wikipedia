## Système de Génération Augmentée par Récupération (RAG) basé sur corpus Wikipédia
Ce projet implémente un système complet de RAG (Retrieval-Augmented Generation) permettant d'interroger une base de connaissances constituée d'articles Wikipédia sur des villes. Le système combine une base de données vectorielle pour la recherche d'informations et un grand modèle de langage (LLM) pour la génération de réponses.

## Fonctionnalités

**Préparation des données :** Chargement, nettoyage et découpage (chunking) d'articles Wikipédia.

**Indexation vectorielle :** Création d'un index FAISS local pour permettre une recherche sémantique rapide.

**Récupération (Retrieval) :** Utilisation du modèle d'embedding thenlper/gte-small pour trouver les documents les plus pertinents par rapport à une question.

**Génération :** Utilisation du modèle Qwen/Qwen2.5-72B-Instruct (via l'API Hugging Face) pour synthétiser une réponse basée sur le contexte retrouvé.

**Interface interactive :** Une boucle de discussion en ligne de commande permettant de poser des questions en continu.

## Prérequis

1. Un compte Hugging Face avec un token d'accès (API Token) valide.

2. Un environnement supportant l'exécution de Notebooks (Jupyter, Google Colab).

3. Un GPU est recommandé pour l'accélération FAISS, mais on peut utiliser également CPU.

## Installation
Pour exécuter ce projet, installez les dépendances nécessaires à l'aide de la commande suivante :
```
pip install -U langchain-community
pip install faiss-gpu-cu12*
pip install datasets*
pip install langchain-text-splitters
pip install sentence-transformers
pip install faiss-cpu
pip install gdown
pip install smolagents
```

## Configuration
Avant de lancer le script, vous devez configurer votre accès à l'API Hugging Face.

1. Ouvrez le notebook.

2. Trouvez la cellule contenant la variable api_token.

3. Remplacez la valeur par défaut par votre propre token.

## Structure du Projet
Le notebook suit les étapes suivantes :

**Importation et Configuration :** Mise en place de l'environnement et des outils de logging.

**Traitement des Données :**

Téléchargement d'un échantillon du jeu de données Sketched33/Cities_Wikipedia_Information.

Découpage des textes en segments de 500 caractères avec chevauchement.

**Gestion de la Base Vectorielle :**

Démonstration de la création d'un index FAISS sur un petit échantillon.

Téléchargement automatique et chargement d'un index pré-calculé contenant environ 3000 articles pour assurer la performance du système final.

**Initialisation du LLM :** Configuration du client d'inférence pour le modèle Qwen-72B.

**Boucle RAG :** Lancement de l'interface utilisateur qui exécute la chaîne : Question -> Recherche Vectorielle -> Augmentation du Prompt -> Génération de la Réponse.

## Utilisation
Une fois les cellules exécutées, le système vous invitera à poser une question:

**Exemple d'interaction :**

**User** : *How many people live in Paris?*

**Assistant** : *[Réponse générée basée sur les documents fournis avec citation des sources]*

Pour quitter le programme, tapez **Exit**.

## Ressources
**LLM** : Qwen/Qwen2.5-72B-Instruct

**Embeddings** : thenlper/gte-small

**Dataset** : Sketched33/Cities_Wikipedia_Information

**Bibliothèques** : LangChain, FAISS, Transformers, Smolagents
