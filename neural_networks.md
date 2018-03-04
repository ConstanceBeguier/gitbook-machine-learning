# Réseau de neurones

Rappel: le perceptron permet uniquement de classifier des données linéairement séparables: $$h_{W,B}(X) = \begin{cases} 0 & \text{ si } W^T X + B < 0 \\ 1 & \text{ si } W^T X + B \geq 0 \end{cases}$$

## Multi-Layer Perceptron  MLP

Afin de résoudre des problèmes non linéairement séparables, combinaison de plusieurs perceptrons en série et introduction d'une fonction non linéaire appelée fonction d'activation (ReLU: $$f(x) = \max(0,x)$$ ou sigmoid: $$f(x) = (1 + e^{-x})^{-1}$$). Cette fonction est appliquée à la sortie de chaque perceptron  $$f(W^T X + B)$$. La dernière couche contient autant de neurones que de classes. Par exemple, si nous voulons reconnaître les chiffres de 0 à 9, la dernière couche contient 10 classes. L'indice du neurone le plus grand de la dernière couche indique la catégorie/classe de sortie. Afin d'interpréter les neurones de sortie par des probabilités, la fonction softmax est souvent ajouté après la dernière couche: $$f(x_i) = \frac{e^{x_i}}{\sum _j e^{x_j}}$$. Avec la fonction softmax, l'erreur est parfois calculée à l'aide de la cross-entropy: $$- \sum_k y_k \cdot ln(f(x_k))$$.

Apprentissage des poids:
  - **Méthode** : 
	  - Forward step: Evaluation de la prédiction pour toutes les entrées dans la base d'apprentissage
	  - Calcul de l'erreur moyenne (Mean squared error MSE):   $$\frac{1}{m} \sum _{i,j} (h(x_i)_j - y_{i,j})^2$$
	  - Backward step: Descente de gradient pour améliorer les poids
  - **Batchs**: 
	  - Batch algorithm: mise à jour des poids après avoir évalué l'erreur sur toutes les entrées
	  - Sequential algorithm: mise à jour des poids après avoir évalué l'erreur sur une seule entrée
	  - Minibatch: séparer la base d'apprentissage en batch et effectuer la descente de gradient batch par batch (un epoch est une itération sur la base d'apprentissage toute entière)
	  - Stochastic Gradient Descent  SGD: similaire à sequential algorithm mais en prenant une entrée aléatoire à chaque itération
  - **Astuces** supplémentaires par rapport au perceptron :
	  - Initialiser les poids avec des valeurs aléatoires entre $$\pm 1/\sqrt{n}$$ avec $$n$$ le nombre de neurones sur la couche d'entrées
	  - Dérivées en chaine: $$\frac{dz}{dx} = \frac{dz}{dy}\frac{dy}{dx}$$
	  - Learning rate diminuant au cours des itérations: exponential  decay: $$\alpha = \alpha _0 \cdot e^{-kt}$$ où $$t$$ est le nombre d'itérations, $$\alpha_0$$ est le learning rate initial et $$k$$ un paramètre
	  - Dropout: sélectionner aléatoirement certains poids et biais lors de l'apprentissage
	  - Momentum  $$m$$ (souvent $$m=0.9$$): $$w = w - \alpha \cdot \frac{\partial J}{\partial w} - m \Delta w$$ où $$\Delta w$$ est égale à la variation de poids lors de l'itération précédente
	  - Décider quand arrêter l'apprentissage en s'aidant d'un courbe de l'erreur (pour la base d'apprentissage et celle de validation) en fonction du nombre d'epochs: s'arrêter d'apprendre quand l'erreur sur la courbe d'apprentissage ne diminue plus (après nous sommes en zone de sur-apprentissage)
	  - Utiliser la dérivée première et seconde dans la descente de gradient

Pour la plupart des problèmes, deux couches cachées suffisent amplement car nous pouvons approximer toutes les fonctions lisses (smooth) par un réseau à deux couches cachées. Le nombre de neurones par couche s'obtient par expérimentation. Il est conseillé de faire une dizaine d'apprentissage par architecture et faire la moyenne des performances obtenues afin de ne pas se tromper à cause d'une initialisation des poids chanceuses. Il est souvent nécessaire d'avoir au moins 10 fois plus de données que de poids dans le réseau à apprendre.

Un MLP peut aussi être utilisé pour faire de la compression (auto-encoder). Pour cela, il suffit que l'entrée soit identique à la sortie et que la couche juste avant la sortie contienne moins de neurones que la couche de sortie. Il faut alors apprendre le réseau et la donnée compressée correspond à la dernière couche cachée. Si nous utilisons une activation linéaire, alors cette méthode est équivalente à une PCA.

## Convolutional Neural Network  CNN

Modifications par rapport au MLP
  - Remplacement des couches linéaires par des couches de convolution inspirée des filtres en traitement d'images. Cela permet de réduire significativement le nombre de poids à apprendre.
  - Ajout de couches de pooling (max ou average) afin de réduire la couche actuelle et de réduire le bruit
  - Architecture classique: $$[(Conv -> Act)^n -> Pool]^m -> FC^2$$ où $$FC$$ représente une couche complètement connectée (étape linéaire dont tous les neurones d'une couche sont reliés à tous les neurones de la couche suivante)
  - (Facultatif) Ajout de couches de batch  normalization avant chaque couche d'activation afin d'avoir une distribution stable en entrée des couches d'activation et ainsi d'accélérer l'apprentissage

