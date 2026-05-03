
# 🏨 Optimisation des Prix Hôteliers — Allocation Budgétaire par Clustering

![Python](https://img.shields.io/badge/Python-3.x-blue)
![Scikit-learn](https://img.shields.io/badge/Scikit--learn-Clustering-orange)
![Status](https://img.shields.io/badge/Status-Terminé-green)

> **Un budget de 2 millions de dollars à allouer intelligemment. Ce projet identifie les segments hôteliers les plus rentables par clustering K-Means et propose une répartition optimale basée sur des KPIs d'efficacité mesurables.**

---

## 🎯 Contexte & Problème Business

L'équipe de stratégie tarifaire dispose d'un **budget supplémentaire de 2 M$** pour le Q1 2025, destiné à offrir des remises clients sur des segments ciblés du secteur hôtelier.

**La question centrale :** Comment allouer ce budget pour maximiser la valeur des réservations générées ?

Les segments analysés combinent 3 dimensions :
- 🌍 **Super-région hôtelière** : NORAM (Amérique du Nord), LATAM (Amérique du Sud et Amérique Centrale), APAC (Asie Pacifique) , EMEA (Europe et Moyen-Orient)  
- 📱 **Type d'appareil** : Mobile ou Desktop
- ⭐ **Catégorie d'étoiles** : Low (1-2★), Mid (3★), High (4-5★)

---

## 📊 Dataset

| Variable | Description |
|---|---|
| `Spend` | Remise tarifaire offerte aux clients (USD/jour) |
| `NBV A` | Valeur des réservations — groupe témoin (sans remise, 30% du trafic) |
| `NBV B` | Valeur des réservations — groupe test (avec remise) |
| `Date` | Date des métriques (données journalières) |
| `HotelSuperRegion` | Région géographique de l'hôtel |
| `Device` | Appareil de réservation (Mobile / Desktop) |
| `StarRating` | Catégorie d'étoiles de l'hôtel |

- **Hotel Super region** : Localisation de l'hôtel réservé.
    + NORAM = Amérique du Nord
    + LATAM = Amérique du Sud et Amérique Centrale
    + APAC = Asie & Pacifique
    + EMEA = Europe et Moyen-Orient
- **Device** : Type d'appareil (mobile ou ordinateur) utilisé pour réserver l'hôtel.
- **StarRating** : Catégorie d'étoiles de l'hôtel réservé.  
   • Low : hôtels économiques (1 à 2 étoiles)   
   • Mid : hôtels de milieu de gamme (3 étoiles)  
   • High : hôtels haut de gamme ou de luxe (4 à 5 étoiles)

---

## 🔬 Méthodologie

### 1. Analyse exploratoire (EDA)

**Statistiques univariées :**
- Remise tarifaire moyenne pour les 3 segements de notre jeu de données est : ~10 500 $ avec un écart-type de ~3 000 $

**Statistiques bivariées — insights clés :**    
![Distributions](https://github.com/Soilah98/Clustering-Segmentation/tree/main/4_Optimisation_des_prix_h%C3%B4teliers/output/distribution_spend_vs_region_hotel.png)  
*Distribution des remises tarifaires par region, catégorie d'etoile et type d'appareil*

| Dimension | Observation |
|---|---|
| **NORAM** | Médiane la plus haute (~12 500$), spend stable et mature |
| **APAC** | Médiane basse (~6 500$), spend très variable — segment sous-investi |
| **Mid ★** | Spend le plus stable, médiane la plus haute |
| **Mobile vs Desktop** | Distributions très proches (~12 000$ de médiane) |
 
---

### 2. Construction des KPIs

Deux indicateurs créés pour mesurer la performance des remises :

| KPI | Formule | Interprétation |
|---|---|---|
| **Incrémentalité** | `NBV B − NBV A` | Valeur supplémentaire générée par la remise |
| **Return on Spend (RoS)** | `Incrémentalité / Spend` | $ de réservations générés pour chaque $ de remise |

> *Pour 1$ de remise offert, combien de dollars de réservations supplémentaires est-ce que je génère ?*

---

### 3. Clustering K-Means

**Variables de clustering :** `Spend`, `Incrémentalité`, `Spend_Efficiency`

**Sélection du k optimal :**  
![choix_cluster](https://github.com/Soilah98/Clustering-Segmentation/tree/main/4_Optimisation_des_prix_h%C3%B4teliers/output/choix_de_cluster.png)  
| Méthode | Résultat |
|---|---|
| Méthode du coude | Cassure nette à k=3 (inertie : 2300 → ~950) |
| Score de silhouette | Pic à k=2 (0.79), compromis choisi à k=3 |

**→ k=3 retenu** pour plus de granularité dans l'analyse des segments.

---

## 💡 Résultats & Recommandations d'allocation  
![Recommandation](https://github.com/Soilah98/Clustering-Segmentation/tree/main/4_Optimisation_des_prix_h%C3%B4teliers/output/Recommandation.png)  
### Segments identifiés par efficacité

| Cluster | Profil | RoS moyen | Spend actuel |
|---|---|---|---|
| 🟢 **Haute efficacité** | APAC Mobile (Mid, Low, High) | > 1 120 | Très faible — sous-investi |
| 🟡 **Efficacité solide** | NORAM Mobile + Desktop (toutes étoiles) | 35 – 38 | Significatif |
| 🔴 **Efficacité modérée** | LATAM & EMEA (toutes combinaisons) | 18 – 20 | Comparable à NORAM |

---

### 💰 Proposition de répartition du budget 2 M$

| Segment | Efficacité | Allocation | Montant |
|---|---|---|---|
| **APAC Mobile** (Mid, Low, High) | RoS > 1 120 | 40% | **800 000 $** |
| **NORAM** (Mobile + Desktop, toutes ★) | RoS 35–38 | 30% | **600 000 $** |
| **LATAM** (Mobile + Desktop, toutes ★) | RoS 19–20 | 20% | **400 000 $** |
| **EMEA** (Desktop + Mobile, toutes ★) | RoS 18–20 | 10% | **200 000 $** |

> **Insight clé :** APAC Mobile est massivement sous-investi avec une incrémentalité de 8,6M$ à 17M$ pour un spend actuel de 460K$ à 910K$ seulement — c'est le levier de croissance prioritaire.

---

## 🏗️ Structure du projet

```
├── README.md
├── data/
│   └── Pricing.xlsx                # Dataset source
├── notebook/
│   └── pricing.ipynb               # Notebook d'analyse complet
├── src/
│   └── visualisation.py            # Fonctions de visualisation réutilisables
├── requirements.txt
└── pyproject.toml
```

---

## 🛠️ Stack technique

- **Python** · Pandas · NumPy
- **Scikit-learn** : KMeans, StandardScaler, PCA, silhouette_score
- **Scipy** : Clustering hiérarchique (dendrogramme)
- **Matplotlib / Seaborn** : Visualisation (boxplots, coude, silhouette)

---

## 🚀 Installation & Utilisation

```bash
# Cloner le repository
git clone https://github.com/Soilah98/Clustering.git
cd Clustering/4_Optimisation_des_prix_hoteliers

# Installer les dépendances
pip install -r requirements.txt

# Lancer le notebook
jupyter notebook notebook/pricing.ipynb
```

---

## ✅ Insights clés

- ✅ **APAC Mobile** est le segment le plus rentable avec un RoS > 1 120 — largement sous-exploité
- ✅ **2 KPIs métiers créés** (Incrémentalité + Return on Spend) pour objectiver l'efficacité des remises
- ✅ Le clustering K-Means permet de **passer de 72 combinaisons de segments à 3 groupes actionnables**
- ✅ La répartition proposée est **data-driven** : chaque allocation est justifiée par un score d'efficacité mesurable
- ✅ Approche reproductible et adaptable à d'autres trimestres ou budgets

---

## 📌 Ce qui différencie ce projet

Ce projet va au-delà du clustering : il **traduit les résultats statistiques en décision business concrète**. La proposition d'allocation budgétaire est directement exploitable par une équipe de stratégie tarifaire, sans intermédiaire.

---

## Auteur

**Ibrahim Soilah** · [GitHub](https://github.com/Soilah98) · [LinkedIn](https://www.linkedin.com/in/soilah-5a166225b/) · [Malt](https://www.malt.fr/profile/ibrahimsoilahoudine)
