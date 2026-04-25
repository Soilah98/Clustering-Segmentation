## Projet 
[Voir le projet](https://colab.research.google.com/drive/1GGR-IX1p2b-oLkXX0SogG-6KtpJajEUu#scrollTo=enwB_Rcs9wJS)
1. ## Contexte 
L'équipe de stratégie de tarification a obtenu un budget supplémentaire de 2 millions de dollars pour le premier trimestre 2025 afin d'offrir des réductions aux clients sur des segments ciblés dans le secteur de l'hôtellerie.  

2. ## Objectif du projet  
**L’objectif de ce projet est d’optimiser l’allocation d’un budget de 2 millions de dollars destiné aux remises dans le secteur hôtelier, afin de maximiser la valeur des réservations.**

L'équipe a sélectionné les dimensions suivantes pour l'optimisation : **super-région hôtelière**, **type d'appareil** et **classification par étoiles des hôtels**.

3. ## Dictionnaire des données 
    * **Spend** : Remise tarifaire offerte aux clients à une date donnée, pour une super-région, un type d'appareil et une catégorie d'étoiles d'hôtel (en USD).
    * **NBV A** : Valeur totale des réservations générée à une date donnée, pour une super-région, un type d'appareil et une catégorie d'étoiles d'hôtel, dans le groupe de test de tarification A (en USD).
    * **NBV B** : Valeur totale des réservations générée à une date donnée, pour une super-région, un type d'appareil et une catégorie d'étoiles d'hôtel, dans le groupe de test de tarification B (en USD).
    * **Date** : Date à laquelle les métriques sont reportées (données journalières).
    * **Hotel Super region** : Localisation de l'hôtel réservé.
         - **NORAM** = Amérique du Nord
         - **LATAM** = Amérique du Sud et Amérique Centrale
         - **APAC** = Asie & Pacifique
         - **EMEA** = Europe et Moyen-Orient
    * **Device** : Type d'appareil (mobile ou ordinateur) utilisé pour réserver l'hôtel.
    * **StarRating** : Catégorie d'étoiles de l'hôtel réservé.
         - "Low" correspond aux hôtels économiques
         - Mid
         - "High" correspond aux hôtels de luxe
4. ## Mission  
Vous êtes chargé de formuler une recommandation sur l'allocation de ce budget entre ces trois segments.
Nous vous demandons d'analyser les données contenues dans le fichier Excel et de préparer une présentation de 15 minutes comprenant :

   - **L'impact attendu et la répartition budgétaire recommandée.**
   - **Des arguments quantitatifs et qualitatifs pour étayer votre recommandation.**

5. ## Informations supplémentaires :
L’équipe de tarification évalue la performance des programmes de réduction grâce à un groupe témoin constant (30 % du trafic) sur lequel aucune remise n’est appliquée ("groupe A").
Au cours du quatrième trimestre (Q4), l’équipe a progressivement augmenté les dépenses sur l’ensemble des segments d’environ 10 %.

6. ## Indication 
- Commencez par une analyse exploratoire des données pour identifier les faits les plus marquants. 
- Soyez proactif dans le nettoyage des données.
- Pouvez-vous définir un KPI pour mesurer l’incrementality ($) générée par la tarification ?
- Pouvez-vous définir un KPI pour évaluer l'efficacité des dépenses ?
- Pouvez-vous penser à une notion économique reliant prix et demande ?
- Comment pourriez-vous adapter cette notion pour analyser l’effet de l’augmentation de 10 % des dépenses sur Q4 ?
- Comment dessineriez-vous (qualitativement) la relation entre dépenses et incrémentalité ?
- N’oubliez pas d’estimer l’impact de votre recommandation.
- Une estimation basée sur des hypothèses solides vaut mieux que de ne rien fournir !
