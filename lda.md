# Analyse discriminante linéaire

Uniquement pour résoudre les problèmes linéairement séparables: possibilité de trouver un hyperplan qui sépare les deux classes de sorties.  

**Perceptron** (réseau de neurones basique): il permet uniquement de classifier des données linéairement séparables: 
  - **Entrées**: couples $$(X,y)$$ avec $$y \in \{0,1\}$$
  - **Objectif**: Trouver $$W$$ et $$b$$ tel que $$h_{W,b}(X) = W^T X + b \geq 0$$ si $$y=1$$ et $$h_{W,b}(X) = W^T X + b < 0$$ si $$y=0$$
  - **Solution** basée sur une descente de gradient: $$w_i = w_i - \alpha(s - y)x_i$$ avec 
$$s = \begin{cases} 0 & \text{ si } h_{W,b}(X)<0 \\ 1 & \text{ si } h_{W,b}(X) \geq 0 \end{cases}$$ et $$h_{W,b}(X) = W^T X + b$$
  - **Astuces** pour améliorer ou accélérer l'apprentissage
	  - Learning rate: $$0.1 < \alpha < 0.4$$
	  - Ajout d'un biais: ajout d'une coordonnée égale à -1 à chaque vecteur d'entrées X (et de son poids associés $$w_0$$). Cela permet de faire varier le seuil.
	  -  Normaliser les entrées (avant la séparation de la BDD en apprentissage, validation, test) afin d'avoir une moyenne à zéro et une variance à 1 sur chaque coordonnée
	  - Sélection des features: en apprenant sur toutes les features sauf 1 et en comparant les performances du classifieur ou en faisant une réduction de dimension (par exemple, PCA)

**Régression linéaire** La grande différence par rapport au perceptron est le format de la sortie. Avec le perceptron, la sortie est une catégorie appartenant à un espace fini et dans le cas de la régression, la sortie est un réel. 
    - **Entrées**: couples $$(X,y)$$ avec $$y \in \mathbb{R}$$
    - **Objectif**: Trouver $$\beta$$ tel que pour une nouvelle donnée $$X$$, nous avons la sortie $$y=X \beta$$
    - **Erreur**: least square error: $$E = (y-X\beta)(y-X\beta)^T$$
    - **Solution**: $$\frac{\partial E}{\partial \beta} = X^T(y-X\beta)=0$$ soit $$\beta = (X^T X)^{-1} X^T y$$

Pour résoudre des problèmes non linéairement séparables avec une analyse discriminante linaire, il faut soit projeter les entrées dans un autre espace (similaire à l'utilisation de kernels pour les SVM), soit ajouter des variables non linéaires (par exemple, $$x_1 \times x_2$$).

