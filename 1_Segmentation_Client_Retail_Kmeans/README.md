# Clustering : Segmentation Client Retail 
***69% du chiffre d'affaires généré par 18% des clients — ce projet identifie ces segments et propose des stratégies marketing concrètes pour chacun***

## Vue d'ensemble
Ce projet réalise une **segmentation de la base clients** basée sur l'analyse **RFM (Récence, Fréquence, Montant)** combinée à un clustering K-Means.   
L'objectif est d'identifier et de caractériser différents segments de clients pour adapter les stratégies marketing.

## Dataset 
- **Source** : Online Retail Dataset (UK, 2010–2011), disponible [ici](https://archive.ics.uci.edu/dataset/352/online%2Bretail?)
- **Période** : 1er décembre 2010 – 9 décembre 2011
- **Contexte** : Transactions e-commerce d'une boutique britannique spécialisée dans les cadeaux
- **Base client** : Particuliers et grossistes
- **Nombre de transactions** : 541 909 (397 884 après nettoyage)
- **Variables** : 8 (InvoiceNo, StockCode, Description, Quantity, InvoiceDate, UnitPrice, CustomerID, Country)

## Métriques RFM 

L'analyse construit trois indicateurs clés par client :

| Métrique | Définition | Interprétation |
|----------|-----------|-----------------|
| **Récence (R)** | Nombre de jours depuis le dernier achat | Fraîcheur de l'engagement client |
| **Fréquence (F)** | Nombre de factures distinctes | Fréquence d'achat |
| **Montant (M)** | Total des dépenses (£) | Valeur totale générée |

### Traitement des données
1. **Nettoyage** :
   - Suppression des transactions annulées (InvoiceNo commençant par "C")
   - Suppression des quantités/prix invalides (≤ 0)
   - Garde uniquement les clients identifiés (CustomerID présent)
   - Suppression des lignes avec dates invalides

2. **Transformation** :
   - Application d'une transformation logarithmique (`log1p`) pour gérer les distributions asymétriques
   - Standardisation des features avec StandardScaler pour K-Means

## Résultats du Clustering 

### Trois segments de clients identifiés :

#### **Cluster 2 : Clients VIP Hyper-Actifs** 
- **Taille** : 769 clients (17,7%)
- **Récence** : 9 jours (achats très récents)
- **Fréquence** : 10 achats
- **Montant moyen** : 3 707 £
- **Part du CA** : **68,25%** du chiffre d'affaires total
- **Stratégie** : Programmes de fidélisation premium, offres exclusives, support VIP

#### **Cluster 1 : Clients Loyaux Réguliers** 
- **Taille** : 1 697 clients (39,1%)
- **Récence** : 30 jours (activité récente)
- **Fréquence** : 3 achats
- **Montant moyen** : 979 £
- **Part du CA** : **24,13%** du chiffre d'affaires total
- **Stratégie** : Campagnes d'engagement, récompenses de fidélité, cross-selling

#### **Cluster 0 : Clients À Risque Inactifs** 
- **Taille** : 1 872 clients (43,2%)
- **Récence** : 158 jours (inactifs depuis des mois)
- **Fréquence** : 1 achat
- **Montant moyen** : 298 £
- **Part du CA** : **7,62%** du chiffre d'affaires total
- **Stratégie** : Campagnes de réactivation, offres de retour, collecte de feedback

## Recommandations Marketing 

| Segment | Action primaire | Action secondaire |
|---------|---|---|
| **VIP (2)** | Maximiser la rétention | Vente additionnelle de produits premium |
| **Loyaux (1)** | Maintenir l'engagement | Augmenter la fréquence d'achat |
| **Inactifs (0)** | Réactiver | Comprendre les raisons du désengagement |
 
## Visualisations
![Distribution](https://github.com/Soilah98/Clustering-Segmentation/tree/main/1_Segmentation_Client_Retail_Kmeans/notebooks/image/Distribution.png)
![Profil des segments](https://github.com/Soilah98/Clustering-Segmentation/tree/main/1_Segmentation_Client_Retail_Kmeans/notebooks/image/cluster.png)

## Structure du projet 
```
├── README.md
├── data
│   └── Online_Retail.xlsx       # Dataset source
├── notebooks
│   └── projet_retail.ipynb      # Notebook d'analyse principal
├── poetry.lock
├── pyproject.toml
├── src
│   └── retail
│       └── __init__.py
└── tests
    └── __init__.py

```

## Technologies utilisées 
- **Python 3.x**
- **pandas** : Manipulation de données
- **numpy** : Opérations numériques
- **scikit-learn** : Clustering K-Means, StandardScaler
- **matplotlib** : Visualisation des données

## Fichiers clés
- `projet_retail.ipynb` : Pipeline d'analyse complet
  - Chargement et nettoyage des données
  - Feature engineering RFM
  - Analyse des distributions avec transformations logarithmiques
  - Clustering K-Means (k=3)
  - Profilage clients et insights marketing

## Installation & Utilisation 

```bash
# Cloner le repository
git clone https://github.com/Soilah98/Clustering.git
cd Clustering/1_Segmentation_Client_Retail_Kmeans

# Installer les dépendances
pip install pandas numpy scikit-learn matplotlib openpyxl

# Lancer le notebook
jupyter notebook notebooks/projet_retail.ipynb
```

## Insights clés 
✅ ** 69% du chiffre d'affaires** provient de seulement **18% des clients** (Cluster 2)  
✅ Les clients inactifs (Cluster 0) représentent **43% de la base** mais seulement **8% du CA**  
✅ Une **différenciation claire** entre segments permet des stratégies ciblées  
✅ La transformation logarithmique a amélioré la robustesse du modèle en normalisant les distributions asymétriques  

## Méthodologie

1. **Nettoyage des données** : Suppression des anomalies, commandes annulées et transactions invalides
2. **Feature Engineering** : Calcul des métriques RFM par client
3. **Prétraitement** : Transformation logarithmique + standardisation
4. **Clustering** : K-Means avec k=3
5. **Profilage** : Analyse des caractéristiques des clusters et implications commerciales
6. **Stratégie** : Développement de recommandations marketing par segment

## Prochaines étapes 
- [ ] Tester d'autres algorithmes de clustering (Hiérarchique, DBSCAN)
- [ ] Modélisation prédictive de l'appartenance aux clusters
- [ ] Tests A/B des stratégies marketing par segment

## Auteur
**Soilah98**

## Contexte académique/professionnel
Projet de segmentation client basé sur une analyse RFM approfondie avec application de techniques d'apprentissage non supervisé.
