# Segmentation de clients avec K-means

Projet de **clustering** (apprentissage non supervisé) : regrouper automatiquement les clients d'une boutique selon leur comportement d'achat, pour adapter la stratégie marketing à chaque profil.

![Clusters K-means et centroïdes](images/clusters.png)

## Objectif

La boutique ne connaît pas à l'avance les différents types de clients. L'objectif est de les **découvrir à partir des données** avec l'algorithme K-means, puis de proposer une action marketing adaptée à chaque groupe.

## Données

Fichier `boutique.csv` : **600 clients**, aucune valeur manquante.

| Colonne | Description |
|---|---|
| `client_id` | identifiant du client (non utilisé pour le clustering) |
| `visites` | nombre de visites du client (1 à 26) |
| `panier` | montant moyen du panier en € (6,59 à 313,82) |

## Méthode

1. **Exploration** : statistiques descriptives et nuage de points `visites` / `panier`. Le nuage ne montre pas de relation linéaire mais environ 4 groupes distincts.
2. **Standardisation** (`StandardScaler`) : les deux variables n'ont pas la même échelle. Sans mise à l'échelle, le panier dominerait le calcul des distances.
3. **Clustering K-means** : k = 4, `n_init=10` (10 initialisations, la meilleure est conservée), `random_state=42`.
4. **Évaluation** : inertie de **78,13**, soit une réduction d'environ **93 %** de la dispersion par rapport à un seul groupe.
5. **Visualisation** : nuage coloré par cluster, avec les centroïdes remis à l'échelle d'origine (`inverse_transform`).

## Résultats

K-means retrouve les 4 groupes identifiés visuellement :

| Profil | Centre (environ) | Description | Action marketing |
|---|---|---|---|
| **Gros acheteurs** | 3 visites, 240 € | Viennent peu mais dépensent beaucoup | Programme VIP, offres premium |
| **Réguliers** | 9 visites, 95 € | Visites et panier moyens | Programme de fidélité |
| **Occasionnels** | 2 visites, 28 € | Viennent peu et dépensent peu | Promotions pour les faire revenir |
| **Visiteurs fréquents** | 18 visites, 22 € | Viennent souvent mais achètent peu | Identifier les freins à l'achat, offres pour augmenter le panier |

## Pistes d'amélioration

- Confirmer le choix de k avec la **méthode du coude** et le **score de silhouette**
- Ajouter d'autres variables (ancienneté, catégories de produits, récence des achats)
- Tester d'autres algorithmes de clustering (DBSCAN, clustering hiérarchique)

## Structure du projet

```
customer-segmentation-kmeans/
├── README.md
├── segmentation_clients_kmeans.ipynb   # notebook complet et commenté
├── boutique.csv                        # jeu de données



## Outils

Python · pandas · matplotlib · scikit-learn · Jupyter

## Auteur

**Yanh Junior Makembi**, étudiant en Bachelor Développeur Data & IA à l'ECE Paris
