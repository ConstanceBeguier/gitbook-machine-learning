# Algorithmes évolutionnistes

## Algorithme génétique

Voici les principales étapes des algorithmes génétiques:
  - Population d'individus
  - Variations pour créer des nouveaux individus
	  - Croisements: mélanger le contenu de plusieurs individus
	  - Mutations: quelques modifications aléatoires
  - Sélection des survivants
	  - Roulette: probabilité de survivre proportionnelle à un score
	  - Classement (avec une fonction de score par exemple soft-max)
	  - Tournois: des pairs aléatoires d'individus sont créées et le meilleur de chaque pair est conservé
  - Nouvelle génération créée de manière itérative

## Population-Based Incremental Learning (PBIL)

Similaire à l'algorithme génétique mais la population d'individus est remplacée par un vecteur de probabilité représentant l'individu idéal (un individu est représenté par un vecteur binaire)

  - Vecteur de probabilité représentant l'individu idéal
  - Création d'une population à l'aide du vecteur de probabilités
  - Appliquer une étape de l'algorithme génétique pour créer une nouvelle population
  - Mise à jour du vecteur de probabilités avec un learning rate de $$\eta$$
$$p = p \times (1 - \eta) + \eta \times mean (population)$$


