# Apprentissage probabilistique

## Modèle de mélange Gaussiens (Gaussian Mixture Models GMM)

  - **Entrées:** données non labellisées
  - **Objectif:** séparer les données en différentes classes en supposant que chaque classe peut être représentée par une gaussienne. L'objectif est de trouver les paramètres de ces gaussiennes. Si nous ne connaissons pas le nombre de classes, il faut tester différentes valeurs et voir ce qui donne le meilleur résultat. 
  - **Sortie** pour une entrée $$x$$: $$f(x) = \sum_c \alpha_c \phi(x; \mu_c, \sigma_c)$$ avec $$\sum_c \alpha_c = 1$$
  - **Probabilité d'appartenir à une classe:** $$P(x \in c) = \alpha_c \phi(x; \mu_c, \sigma_c) / f(x)$$
  - **Méthode:** utiliser l'algorithme EM
	  - Initialisation: choisir aléatoirement $$\alpha_c, \mu_c, \sigma_c$$
	  - E-step: calculer l'espérance: $$P(x \in c)$$
	  - M-step: trouver les paramètres qui maximisent l'espérance en la différenciant
	  - Répéter E-step et M-step jusqu'à convergence

## Recherche de plus proches voisins

  - **Entrées:** données labellisées $$(x_i, t_i)$$
  - **Objectif:** donner une classe à une donnée inconnue $$y$$
  - **Méthode:** trouver les $$k$$ plus proches voisins de $$y$$ parmi les $$x_i$$. Faire un vote majoritaire parmi ces voisins pour déterminer la classe de $$y$$
  - **Astuce:** $$KD-tree$$ est un algorithme efficace pour calculer les $$k$$ plus proches voisins

## KD-tree

  - **Objectif:** créer une structure de données de partitionnement de l'espace qui permet de stocker des points et de faire des recherches efficaces de plus proches voisins
  - **Construction** (par exemple en dimension 2): 
	  - trouver l'hyperplan orthogonal à (Ox) passant par une entrée (non encore incluse dans l'arbre) qui sépare l'ensemble des entrées en deux groupes équilibrés
	  - mettre l'entrée sélectionnée à la racine de l'arbre
	  - construire récursivement les deux sous-arbres avec les deux groupes créés et en prenant des hyperplans orthogonaux à (Oy)
	  - continuer de manière récursive jusqu'à ce que chaque entrée appartienne à un noeud de l'arbre

