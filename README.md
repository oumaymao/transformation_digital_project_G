# Cartographie des tendances scientifiques émergentes (2021–2025)

##  Contexte académique

**Projet :** Transformation Digitale – Projet DE
**Encadrante :** Pr. Sara Ouald Chaib

**Réalisé par :**

* Ouhra Oumayma
* Rhouati Jihane
* Sabor Omar
* Haouhaou Mohamed

---

## Présentation du projet

Dans un contexte de surproduction scientifique mondiale (plus de 2,5 millions d’articles publiés par an), il devient essentiel de disposer d’outils automatisés capables d’identifier les **tendances scientifiques émergentes**.

Ce projet propose un **pipeline data-driven complet**, combinant **extraction de données à grande échelle**, **traitement NLP**, **modélisation thématique avancée (BERTopic)** et **visualisation interactive**, afin de cartographier l’évolution des thématiques scientifiques entre **2021 et 2025**.

---

## Objectifs

* Développer un pipeline automatisé d’extraction et d’analyse de publications scientifiques
* Identifier les thématiques de recherche émergentes entre 2021 et 2025
* Analyser l’évolution temporelle des tendances scientifiques
* Fournir des insights exploitables pour la prise de décision stratégique (R&D, recherche, politique scientifique)

---

##  Périmètre de l’étude

* **Période :** 2021 – 2025
* **Volume :** 2 000 publications les plus citées
* **Source :** Publications scientifiques internationales
* **Langue d’analyse :** Anglais
* **Disciplines :** Multidisciplinaire

---

##  Source de données

### OpenAlex

* **Site officiel :** [https://openalex.org](https://openalex.org)
* **API :** [https://api.openalex.org/works](https://api.openalex.org/works)

**Pourquoi OpenAlex ?**

* Données ouvertes et gratuites
* Métadonnées riches et bien structurées
* Adapté aux projets académiques et data science

### Données extraites

* **Métadonnées bibliographiques** : titre, résumé, date de publication, DOI, source
* **Indicateurs d’impact** : nombre de citations, open access
* **Entités associées** : auteurs, concepts scientifiques

---

##  Architecture du projet

### Pipeline global

1. **Extraction des données** (API OpenAlex)
2. **Stockage intermédiaire** (JSON → Pandas DataFrame → CSV)
3. **Prétraitement NLP**
4. **Génération d’embeddings sémantiques**
5. **Topic Modeling avec BERTopic**
6. **Analyse temporelle des tendances**
7. **Visualisation interactive**

---

## ⚙️ Collecte des données

### Paramètres principaux de l’API

```python
params = {
    "filter": "from_publication_date:2021-01-01,to_publication_date:2025-12-31",
    "per-page": 200,
    "sort": "cited_by_count:desc"
}
```

* Gestion de la pagination
* Gestion des erreurs HTTP
* Respect des limitations de requêtes

---

##  Prétraitement NLP

Les abstracts sont nettoyés et normalisés via **NLTK** :

1. Reconstruction de l’abstract (index inversé → texte)
2. Passage en minuscules
3. Suppression de la ponctuation et caractères spéciaux
4. Tokenisation
5. Lemmatisation (WordNet Lemmatizer)
6. Suppression des stopwords
7. Filtrage des mots courts (< 3 caractères)

---

## Représentation sémantique

### Sentence-BERT

* **Modèle :** `all-MiniLM-L6-v2`
* **Dimensions :** 384
* Capture le sens sémantique global des textes
* Plus performant que les approches TF-IDF classiques

---

## Topic Modeling

### BERTopic

BERTopic combine :

* **Embeddings BERT**
* **UMAP** pour la réduction de dimension
* **HDBSCAN** pour le clustering
* **c-TF-IDF** pour l’extraction de mots-clés

 Choisi pour la **cohérence sémantique élevée** des topics produits.

---

## Schéma des données finales

| Colonne        | Description          |
| -------------- | -------------------- |
| title          | Titre de l’article   |
| abstract       | Résumé complet       |
| year           | Année de publication |
| doi            | Identifiant DOI      |
| cited_by_count | Nombre de citations  |
| topic          | ID du topic          |
| topic_prob     | Probabilité du topic |
| authors        | Liste des auteurs    |
| open_access    | Accès libre          |

---

## Visualisation

Les résultats sont visualisés avec **Plotly** :

* Graphiques interactifs
* Évolution temporelle des topics
* Zoom, survol, export

---

## Résultats principaux

* **7 topics majeurs identifiés**
* Domination de l’IA et de la santé
* Déclin progressif des thématiques COVID-19
* Émergence marquée de l’IA générative (ChatGPT) à partir de 2023

---

## Contribution à la transformation digitale

Ce projet illustre concrètement :

* L’exploitation d’infrastructures cloud ouvertes (OpenAlex)
* L’automatisation du traitement de données scientifiques massives
* L’utilisation de modèles avancés d’IA (Transformers, BERTopic)
* Le remplacement des analyses manuelles par des pipelines intelligents

Il démontre comment la **data science** et l’**IA** transforment la veille scientifique et la prise de décision stratégique.

---

## Limites

* Sous-représentation des articles récents
* Biais lié au nombre de citations
* Nettoyage des abstracts incomplets
* Analyse limitée à l’anglais

---

## Améliorations futures

* Augmenter le corpus (5 000 – 10 000 articles)
* Équilibrer les publications par année
* Ajouter des filtres par domaine scientifique
* Support multilingue

---

## Technologies utilisées

* Python
* Pandas, NumPy
* NLTK
* Sentence-Transformers
* BERTopic
* Scikit-learn
* Plotly
* Jupyter Notebook

---

## Licence

Projet académique réalisé dans le cadre de la formation **Data Engineering – ENSAH**.

---

*Ce projet démontre la puissance des pipelines data et de l’IA pour anticiper les tendances scientifiques mondiales.*
