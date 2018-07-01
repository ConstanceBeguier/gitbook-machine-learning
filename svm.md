# Support Vector Machine SVM

SVM consiste à trouver l'**hyperplan** qui sépare l'espace tout en respectant les deux catégories des données en entrée. Le meilleur hyperplan est celui avec la **marge maximale**. Si c'est donnée ne sont pas linéairement séparables, nous pouvons soit utiliser des **noyaux** pour les projeter dans un espace à grande dimension, soit **autoriser quelques erreurs**.

  - **Problème à résoudre**: $$\min_{\theta} \frac{1}{2} \parallel \theta \parallel ^2$$ tel que $$y_i (\theta ^T X_i + b) \geq 1$$
  - **Avec erreurs possibles**: $$\min_{\theta} \frac{1}{2} \parallel \theta \parallel ^2 + C \sum_k \zeta_k$$ tel que $$y_i (\theta ^T X_i + b) \geq 1 - \zeta_i $$ et $$\forall k, \zeta_k \geq 0$$
  - **Méthode**: optimisation quadratique (en temps polynomial)
  - **Dual**: $$\max_{\alpha} \sum_k \alpha_k - \frac{1}{2} \sum _{i,j} \alpha_i \alpha_j y_i y_j X_i^T X_j$$ tel que $$\alpha_k \geq 0$$ et $$\sum_k \alpha_k y_k = 0$$. Notons $$\alpha^*$$ les $$\alpha$$ qui maximisent cette équation. L'équation de l'hyperplan séparateur est $$h(X) = \sum _k \alpha_k^* y_k (X^T X_k)+ b$$
  - **Kernels**: $$K(X,Y) = \Phi(X) \Phi(Y) = X^T Y$$
	  - Noyau linéaire: $$K(X,Y) = X ^T Y$$
	  - Noyau polynomial: $$K(X,Y) = (1 + X ^T Y)^p$$
	  - Noyau Gaussien (RBF): $$K(X,Y) = exp ( -\frac{\parallel X-Y \parallel^2}{2 \sigma ^2} )$$  
	  - Noyau tangente hyperbolique: $$K(X,Y) = \tanh (\kappa X ^T Y + c)$$

Le kernel polynomial correspond à transformer une entrée $$X=(x_1, x_2, x_3)$$ en une entrée $$\phi(X) = (1, \sqrt{2} x_1, \sqrt{2} x_2, \sqrt{2} x_3, x_1 ^2, x_2 ^2, x_3 ^2, \sqrt{2} x_1 x_2, \sqrt{2} x_1 x_3, \sqrt{2} x_2 x_3)$$. Nous avons alors $$\phi(X)^T \phi(Y) = K(X,Y) = (1 + X ^T Y)^2$$. Dans les calculs, nous évaluons jamais $$\phi(X)$$ seul mais toujours $$\phi(X) ^T \phi(Y)$$, ce qui est beaucoup moins couteux (kernel trick).

Si nous voulons faire une $$N$$ classification, il suffit de faire $$N$$  SVM qui classifie une classe contre toutes les autres. Puis lors de la classification d'un nouvel élément, nous prenons la classe qui donne le meilleur résultat (pour laquelle l'élément à classifier est le plus loin de la margin).

**SVM régression**

Le problème consiste à trouver un hyperplan pour lequel toutes les données se situent dans un hyper-cylindre centré sur cet hyperplan et de rayon $$\epsilon$$. Par conséquent, les maximisations et minimisations du problème précédent sont inversées mais la logique reste identique.
