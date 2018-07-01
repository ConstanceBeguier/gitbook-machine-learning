# Apprentissage non supervisé

## k-means

  - **Problème**: étant donné des points $$(x_1, ..., x_n)$$, on veut les partitionner en $$k$$ ensemble $$(S_1,..., S_k)$$ en minimisant la distance entre les points appartenant à un même ensemble. Mathématiquement $$argmin _S \sum _i \sum _{x_j \in S_i} dist(x_j, \mu_i)$$ où $$\mu _i $$ est la moyenne des points dans $$S_i$$.
  - **Initialisation**
	  - Choisir un nombre de clusters $$k$$
	  - Choisir aléatoirement $$k$$ points $$m_1, ..., m_k$$
  - **Apprentissage**
	  - Répéter jusqu'à convergence:
		  - Effectuer une partition de Voronoi selon les moyennes:
$$S_i = \{ x_p : dist(x_p, m_i) \leq dist(x_p, m_j), \forall 1 \leq j \leq k \}$$
		  - Mettre à jour la moyenne de chaque cluster: $$\forall i, m_i = \frac{1}{|S_i|} \sum_{x_j \in S_i} x_j$$
  - **Classification**
	  - Calculer la distance ente $$x$$ et chacun des centres $$m_i$$
	  - Assigner à $$x$$ le cluster pour lequel la distance à son centre est minimal

Attention cet algorithme est sensible aux minima locaux. Il peut être utile de le lancer plusieurs fois avec des initialisations différentes et de conserver l'apprentissage qui a une erreur globale minimale (somme de la distance de chacun des points de la base d'apprentissage à son centre le plus proche).

Cet algorithme est aussi utilisé pour réduire le bruit dans un ensemble de données en remplaçant chaque donnée en entrée par son centre le plus proche.
