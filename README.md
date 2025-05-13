# Flop Holdem Poker - Algorithme CFR

## Description du projet
Ce projet implémente l'algorithme Counterfactual Regret Minimization (CFR) pour une variante simplifiée de Texas Hold’em, appelée Flop Hold’em. Le jeu comporte deux cartes privées (pocket cards), trois cartes communes (community cards) et deux tours d’enchères. L’objectif est de gérer efficacement le grand nombre de combinaisons possibles grâce à CFR+ (stratégie moyenne, élagage, regret alterné).

## Fonctionnalités
- Classe `FlopHoldemGame` pour modéliser le jeu et gérer les phases de mise.
- Classe `Node` pour représenter les états du jeu et calculer les regrets.
- Implémentation de CFR+ avec enregistrement des stratégies moyennes.
- Visualisation de l’évolution des regrets et des stratégies (via matplotlib).
- Estimation de la valeur des mains, tri des cartes et évaluation du gagnant.
- Progression du calcul affichée avec `tqdm` et `alive_progress`.
- Support pour le calcul parallèle via `joblib`.

## Installation
Installez les dépendances requises :
```bash
pip install numpy matplotlib networkx scipy tqdm alive_progress joblib
```

## Utilisation
1. Lancez l’entraînement de l’algorithme depuis le notebook Jupyter :
   ```python
   from flop_holdem_poker import FlopHoldemGame
   trainer = FlopHoldemGame()
   path_trained_dataset = 'flop_holdem_poker_stratModel_bis.json'
   trainer.train(path_dataset=path_trained_dataset, n_iterations=10000, clean_dataset=True)
   ```
2. Affichez les résultats :
   ```python
   trainer.get_trainingEvolution()
   trainer.display_results_detailed(min_num_updates=10)
   ```

## Structure du projet
- `Flop Holdem Poker Algo.ipynb` : notebook principal contenant tout le code et la documentation.
- `flop_holdem_poker_stratModel_bis.json` : modèle de stratégie sauvegardé après entraînement.
- `README.md` : documentation du projet.

## Détails de l’algorithme
- **CFR+** : amélioration de l’algorithme CFR avec prises en compte des regrets alternés et élagage des branches peu pertinentes.
- **Stratégie moyenne** : calcul et enregistrement de la stratégie moyenne pour garantir convergence vers l’équilibre de Nash.
- **Élagage** : suppression des états peu probables pour réduire la complexité.
- **Regret alterné** : variation du calcul de regret pour accélérer la convergence.

## Fonctions utilitaires
- `estimate_hand_value(hole_cards, community_cards)` : calcule la force d’une main.
- `sort_cards(cards)` : trie et formate les cartes pour l’affichage.
- `test_winner(hands, community_cards)` : détermine la main gagnante parmi plusieurs joueurs.
- Visualisation en temps réel avec `matplotlib` et barre de progression.

## Résultats
Après 1 000 000 d’itérations, l’algorithme atteint environ 1 062 934 nœuds théoriques explorés en ~9 minutes (expérience 1).

## Travaux futurs
- Optimisation des fonctions de regret avec Parametric ReLU et IA d’estimation de paramètres.
- Entraînement d’un modèle Deep CFR pour Flop Hold’em.
- Extension à "Rhode Island Poker" (1 carte privée, 4 cartes communes, 3 tours d’enchères).
- Augmentation du nombre de mises par tour.

## Contribution
Les contributions sont les bienvenues ! Merci de soumettre vos pull requests et vos rapports de bugs.

## Auteur
- CUZOU Alexandre

## Licence
Ce projet est sous licence MIT.
