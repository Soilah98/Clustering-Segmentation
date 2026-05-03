# 🌍 Notation Macroéconomique des Pays — Clustering Hiérarchique (IMF WEO)

![Python](https://img.shields.io/badge/Python-3.x-blue)
![Scikit-learn](https://img.shields.io/badge/Scikit--learn-Clustering-orange)
![Source](https://img.shields.io/badge/Source-IMF%20WEO%202024-green)
![Status](https://img.shields.io/badge/Status-Terminé-brightgreen)

> **191 pays notés A, B ou C sur la base de 6 indicateurs macroéconomiques clés (FMI 2024) — sans supervision, 100% data-driven.**

---

## Contexte & Problème

Comment comparer la santé économique de 191 pays à partir de données hétérogènes (PIB, inflation, dette, balance courante...) et produire une notation lisible et actionnable ?

Ce projet répond à cette question en combinant **clustering hiérarchique non supervisé** et **interprétation macroéconomique** : les groupes émergent des données, la notation découle ensuite de la performance agrégée de chaque groupe.

> Cas d'usage typique : due diligence pays pour investisseurs, scoring de risque souverain, analyse comparative pour cabinets de conseil ou institutions financières.

---

## 📊 Données

- **Source** : [FMI — World Economic Outlook (WEO), Avril 2024](https://www.imf.org/en/publications/weo/weo-database/2024/april)
- **Périmètre** : 191 pays (après nettoyage)

| Indicateur | Description |
|---|---|
| **PIB par habitant (USD)** | Niveau de richesse par habitant |
| **Croissance du PIB réel (%)** | Dynamisme économique |
| **Inflation moyenne (%)** | Stabilité des prix |
| **Dette publique brute (% PIB)** | Soutenabilité budgétaire |
| **Solde budgétaire (% PIB)** | Équilibre des finances publiques |
| **Compte courant (% PIB)** | Position extérieure nette |

---

## 🔬 Méthodologie

### 1. Nettoyage & Préparation
- Suppression de la variable `Unemployment` (trop de valeurs manquantes)
- Suppression des lignes incomplètes → **191 pays retenus**
- Séparation des identifiants pays (`Country`) des features numériques

### 2. Standardisation
- `StandardScaler` appliqué sur les 6 indicateurs
- Nécessaire pour éviter que le PIB (en milliers de $) domine les autres variables

### 3. Clustering Hiérarchique (Ward)
- Méthode de **Ward** : minimise la variance intra-cluster à chaque fusion
- **Dendrogramme** analysé visuellement → cassure nette à **k=3**
- Découpage en 3 clusters via `fcluster(criterion="maxclust", t=3)`
- [Dendrograme](https://github.com/Soilah98/Clustering-Segmentation/tree/main/3_Notation_macro%C3%A9conomique_pays/output/dendrograme.png)

### 4. Notation Data-Driven
Les clusters sont ordonnés selon leur **performance macroéconomique agrégée** (PIB/hab, inflation, dette) et une note est attribuée :

---

## Résultats — Les 3 notes macroéconomiques

| Note | Cluster | Nb de pays | Profil synthétique |
|---|---|---|---|
| 🟢 **A** | Cluster 2 | **31 pays** | Économies développées : PIB/hab élevé, inflation maîtrisée, dette soutenable |
| 🟡 **B** | Cluster 3 | **156 pays** | Économies émergentes : croissance soutenue, inflation modérée, dette moyenne |
| 🔴 **C** | Cluster 1 | **4 pays** | Économies en crise : croissance négative, inflation élevée, dette excessive |

### Interprétation

- **Groupe A (31 pays)** — Stabilité structurelle, accès facilité aux marchés financiers, faible risque souverain. Exemples typiques : pays d'Europe occidentale, Amérique du Nord, Japon, Australie.
- **Groupe B (156 pays)** — Potentiel de croissance mais vulnérabilités persistantes (inflation, déficits). Représente la majorité des pays du monde.
- **Groupe C (4 pays)** — Indicateurs macroéconomiques dégradés sur tous les axes : urgence de politiques de stabilisation.

---

## 🏗️ Structure du projet

```
├── README.md
├── data/
│   └── data.csv                    # Dataset IMF WEO 2024
├── notebooks/
│   └── pays.ipynb                  # Notebook d'analyse complet
├── requirements.txt
└── pyproject.toml
```

---

## 🛠️ Stack technique

- **Python** · Pandas · NumPy
- **Scikit-learn** : StandardScaler
- **Scipy** : `linkage`, `dendrogram`, `fcluster` — clustering hiérarchique Ward
- **Matplotlib / Seaborn** : dendrogramme, visualisations par cluster

---

## Installation & Utilisation

```bash
# Cloner le repository
git clone https://github.com/Soilah98/Clustering.git
cd Clustering/3_Notation_macroeconomique_pays

# Installer les dépendances
pip install pandas numpy scikit-learn scipy matplotlib seaborn

# Lancer le notebook
jupyter notebook notebooks/pays.ipynb
```

---

## ✅ Insights clés

- ✅ **191 pays classés en 3 groupes** à partir de données FMI officielles — approche reproductible et actualisable chaque année
- ✅ **Seulement 4 pays en note C** — la crise économique sévère concerne une minorité mais avec des indicateurs extrêmes sur tous les axes
- ✅ **156 pays en note B** — la majorité mondiale est en développement, avec des profils très hétérogènes au sein du groupe
- ✅ La méthode **Ward + dendrogramme** permet une sélection objective du nombre de clusters sans hyperparamètre arbitraire
- ✅ Approche **100% non supervisée** : la notation émerge des données, sans biais de classification préalable

---

## 📌 Ce qui différencie ce projet

Ce projet applique une méthodologie de **notation souveraine data-driven** similaire à celle utilisée par les agences de rating (Moody's, S&P, Fitch) — mais de façon transparente, reproductible et sans jugement subjectif. Il démontre une capacité à travailler sur des données institutionnelles réelles et à produire des livrables directement exploitables par des équipes de conseil, finance ou stratégie.

---

## 🔄 Prochaines étapes

- [ ] Actualisation annuelle avec le WEO le plus récent
- [ ] Ajout d'indicateurs : chômage, IDH, risque politique
- [ ] Visualisation cartographique interactive (Plotly / Folium)
- [ ] Comparaison avec les notations officielles S&P / Moody's

---

## Auteur

**Ibrahim Soilah** · [GitHub](https://github.com/Soilah98) · [LinkedIn](https://www.linkedin.com/in/soilah-5a166225b/) · [Malt](https://www.malt.fr/profile/ibrahimsoilahoudine)
