![Python](https://img.shields.io/badge/Python-3.x-blue)
![Scikit-learn](https://img.shields.io/badge/Scikit--learn-ML-orange)
![Streamlit](https://img.shields.io/badge/Streamlit-Deployed-red)
![Status](https://img.shields.io/badge/Status-Terminé-green)

1. # Notation macroéconomique des pays par Clustering hiérarchique — IMF WEO

2. ## Contexte / Problématique
- **Contexte**
Les institutions économiques, investisseurs et organisations internationales ont besoin d’évaluer rapidement la santé macroéconomique des pays afin de guider leurs décisions (investissement, politiques publiques, gestion des risques).

Les données du Fonds Monétaire International (IMF – World Economic Outlook) offrent une base riche pour analyser ces dynamiques à l’échelle mondiale.
---
- **Problématique**
Peut-on regrouper les pays en profils macroéconomiques homogènes à partir d’indicateurs clés, afin de construire une notation synthétique et interprétable ?

- Objectif :  
Le but de ce projet est regrouper les pays selon des indicateurs macroéconomiques clés et leur attribuer une note.

3. ## Données
- Source : IMF — World Economic Outlook (WEO) depuis le [site du FMI](https://www.imf.org/en/publications/weo/weo-database/2024/april?utm_source=chatgpt.com)
- Type : Données macroéconomiques par pays
- Taille : 194 observations
- Granularité : annuelle
- Variables principale 
| **Indicateur**                              | **Description (EN)**                                                   |
|----------------------------------------|--------------------------------------------------------------------|
| **PIB par habitant (USD courants)**       | Gross domestic product per capita, current prices — U.S. dollars  |
| **Croissance du PIB réel (% chg)**         | Gross domestic product, constant prices — Percent change          |
| **Inflation moyenne (% chg)**              | Inflation, average consumer prices — Percent change               |
| **Dette publique brute (% du PIB)**        | General government gross debt — Percent of GDP                    |
| **Solde budgétaire (% du PIB)**            | General government net lending/borrowing — Percent of GDP         |
| **Compte courant (% du PIB)**              | Current account balance — Percent of GDP                          |

4. ## Analyse exploratoire

5. ## Methodologie 
* **Préprocessing**
   - Nettoyage des données 
   - Noramalisation (StandardScaler)
* **Modélisation : Clustering hierarchique (Ward)**
   - Methode : Clustering Ascendant Hiérarchique (CAH)
   - Distance : Euclidienne 
   - Méthode de liaison : Ward
   - Visualisation : dendrogramme 
Objectif : identifier des groupes de pays similaires sans hypothèse préalable

6. **Résultats met en evidence 3 clusters principaux** :
|Cluster| Note| Nombre de pays | Profil macroéconomique|
|-------|-----|----------------|-----------------------|
|2|A| 31 pays| Économies développées : PIB/hab élevé, inflation maîtrisée, dette soutenable|
|3 | B| 156 pays| Économies émergentes : croissance soutenue, inflation modérée|
|1|C|4 pays |Économies en crise : croissance négative, inflation élevée, dette excessive|
- * Les pays du groupe A affichent une stabilité structurelle, les B un potentiel de croissance et les C nécessite des politique de stabilité 
Les 4 pays du cluster C affichant une économie en crise sont : Argentine , Lebanon, Sudan, Zimbabwe
---
* **Ce type d’approche peut être utilisé pour** :
    - Scoring pays
    - anlyse de risque 
    - allocation d'inverstissement 

* **Limites** 
    -  Clustering non supervisé → pas de “vérité terrain”
    - Données statiques (pas de dynamique temporelle)

* **Améliorations possibles**
  - Intégrer des données temporelles (séries chronologiques)
  - Tester d’autres méthodes (K-Means, DBSCAN)
  - Réduction de dimension (ACP)
  - Déploiement d’un dashboard interactif (Power BI / Streamlit)
  - Ajout d’indicateurs géopolitiques

---- 
- **Stack technique**
   * Python 
   * Pandas 
   * Scikit-learn
   * Matplotlib / Seaborn
   * SciPy (clustering hiérarchique)
---
**Utilisation**


`
.
├── README.md
├── data
│   └── data.csv
├── notekooks
│   └── pays.ipynb
├── poetry.lock
├── pyproject.toml
└── requirements.txt
`