# Apprentissage avec des arbres

## Un arbre de décision

  - **Construction de l'arbre**
	  - Choisir l'attribut qui sépare le mieux la base de données (minimise la diversité)
	  - Séparer la base d'apprentissage en fonction de cet attribut
	  - Continuer récursivement en construisant un sous-arbre avec chacune de ces sous-bases
  - **Méthode pour sélectionner l'attribut**
	  - Indice de diversité de Gini (CART): fréquence qu'un élément aléatoire de l'ensemble soit mal classé si son étiquette était sélectionnée aléatoirement depuis la distribution des étiquettes dans le sous-ensemble. Mathématiquement si la classe prend une valeur aléatoire dans $$1, ..., m$$ et si $$p_i$$ est la probabilité qu'un item avec le label $$i$$ soit choisi alors $$I_G(f)=\sum_{i=1}^m p_i (1 - p_i) = 1 - \sum_i p_i^2$$
	  - Gain d'information (ID3, C4.5): basé sur le concept d'entropie de Shanon: $$I_E(p) = - \sum_{i \in E} p_i \log_2 p_i$$

## Ensemble learning

  - **AdaBoost**
	  - **Objectif** créer un ensemble de classificateurs faibles sur différentes versions de la BDD. Puis un vote majoritaire avec poids est calculé pour décider le la classification finale
	  - **Méthode** Le premier classifieur est appris sur la BDD initiale et on attribue à chaque donnée pour l'apprentissage un poids de $$1/N$$ ($$N$$ est le nombre d'entrées dans la base d'apprentissage). Pour la construction du deuxième classifieur, on augmente le poids des données ayant été mal classifiées par le classifieur précédent et on diminue le poids des données ayant été bien classifiées. Et ainsi de suite pour les classifieurs suivants. Par conséquent, les entrées les plus dures à classifier ont de plus en plus d'influence lors de la construction des classifieurs.
  - **Bagging**
	  - **Objectif** créer un ensemble de classificateurs faibles sur différentes versions de la BDD. Puis un vote majoritaire avec poids est calculé pour décider le la classification finale
	  - **Méthode** Pour chaque arbre, créer une nouvelle base d'apprentissage en prenant au hasard avec remise (doublons autorisés) des données de la base d'apprentissage. Utiliser un algorithme simple pour construire un arbre à partir de chacune des nouvelles bases de données.

Exemple: **random forest**: bagging dont la construction de l'arbre est effectuée en prenant aléatoirement pour chaque nouveau noeud un sous-ensemble des features restantes , puis en sélectionnant la meilleure feature dans ce sous-ensemble à l'aide de l'entropie ou de l'indice de Gini

