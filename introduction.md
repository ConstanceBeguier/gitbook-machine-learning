# Introduction

## Types de machine learning

**Apprentissage supervisé \(classification et régression\):** à partir d'une BDD d'apprentissage avec des données et leurs labels, il faut généraliser afin de donner un label à des données jamais vues

* CNN, SVM, arbres de décision \(ID3, C5, CART\), régression linéaire
* AdaBoost, Bagging

**Apprentissage non supervisé \(clustering\):** partitionner les données afin que les données dans une même partition soient proches entre elles \(aient quelque chose en commun\) et les données provenant de deux partitions différentes soient éloignées

* k-means, algorithme EM, regroupement hiérarchique \(arbre\)

**Apprentissage par renforcement:** apprentissage d'un bon comportement à partir d'observations/récompenses. A chaque étape, l'algorithme propose une action et le système donne un score à cette action \(indiquant si l'action est bénéfique ou pas\) sans indiquer comment améliorer ce score.

* Q-learning, Hidden Markov Model \(Viterbi et Baum Welch\)

**Apprentissage évolutionniste:** le principe s'inspire de la théorie de l'évolution pour résoudre des problèmes diverses. La théorie de l'évolution repose sur le fait que les organismes s'adaptent pour améliorer leur taux de survie et celui de leurs descendants

* algorithmes génétiques

**Réduction de dimension \(compression\):** réduire la dimension des entrées afin de réduire le stockage toute en gardant un maximum d'information

* Stratégies d'évolution, Programmation évolutionnaire, Algorithmes génétiques

**Système de recommandations:** filtrage de l'information visant à présenter les éléments d'information \(films, musique, livres, news, images, pages Web, etc\) qui sont susceptibles d'intéresser l'utilisateur

* collaborative filtering, content-based filtering, hybrid algorithm

## Machine learning process

* Récupération et nettoyage des données
* Création des features
* Choix de l’algorithme
* Détermination des paramètres de l’algorithme
* Apprentissage
* Evaluation

## Séparation de la base de données

* Base d’apprentissage : 60%
* Base de validation : 20%
* Base de test : 20%

Méthode de cross-validation : séparer la base d’apprentissage \(80%\) en K  
sous-ensembles : prendre le 1er sous-ensemble pour la validation et apprendre  
avec les autres sous-ensembles, puis prendre le 2e sous-ensemble pour la validation et apprendre avec les autres sous-ensembles, répéter cette étape K  
fois et conserver l’apprentissage qui a obtenu le meilleur score de validation

## Quelques métriques

* **Accuracy :** nombre d’entrées correctement classifiées sur le nombre total d’entrées
* **Matrice de confusion:** l’élément en position \(i, j\) de la matrice est égal au
  nombre d’entrées que l’algorithme place dans la catégorie j alors qu’ils
  appartiennent à la catégorie i. Par conséquent, les valeurs au niveau de
  la diagonale de la matrice représentent le nombre d’éléments correctement classifiés. L’accuracy est donc égale à la somme des valeurs de la
  diagonale divisée par la somme de tous les éléments.
* **Sensibilité \(recall\), Spécificité, Précision :** 
  {% math %}recall = TP/(TP + FN ){% endmath %}
  $$specificity = TN/(TN + FP )$$
  $$precision = TP/(TP + FP )$$
  avec $$TP$$ \(resp. $$TN$$ \) le nombre de vrais positifs \(resp. négatifs\), $$FP$$ \(resp. $$FN$$\) le nombre de faux positifs \(resp. négatifs\) 

![](/images/F1score_new.png)

* **F1-score :** $$2 \cdot precision \cdot recall/(precision + recall)$$
* **Courbe de ROC \(Receiver Operator Characteristic:** courbe du pourcentage de vrais positifs \(sur l’axe y\) par rapport au pourcentage de
  faux positifs \(sur l’axe x\). Cette courbe permet de comparer différents paramétrages d’un même classifieur ou de comparer différents classifieurs. L’aire sous la courbe ROC \(area under the curve AUC\) est une bonne métrique représentant le classifieur.
* **Minkowski metric:** $$L_k(x,y)=\sum _i (|x_i - y_i |^k)^{1/k}$$
  * k = 1 : distance de Manhattan
  * k = 2 : distance Euclidienne
  * Si $$average(X_1 , ..., X_n ) = argmin_Y \sum_i dist(X_i,Y)$$, alors cette valeur est la médiane dans pour k = 1 et la moyenne pour k = 2.

## Quelques rappels de probabilité

* **Bayes’ rule :** $$P (C_i |X_j ) = \frac{P(X_j | C_i) \cdot P(C_i)}{P(X_j)}$$ car $$P(X_j |C_i ) = P (X_j , C_i )/P (C_i )$$
* **Posterior probability:** $$P (C_i |X_j )$$
* **Prior probability:** $$P (C_i )$$
* **Class conditionnal probability:** $$P (X_j |C_i )$$
* **Maximum a posteriori \(MAP\):** $$argmax_i P(C_i |X)$$ : quelle est la classe la plus probable pour une entrée donnée \(vecteur de features\)
* **Naive Bayes’ Classifier:** MAP en suppossant Q que les features sont indépendantes entre elles. Donc $$P(X|C_i ) = \prod_j P(X_j |C_i )$$. Et donc $$argmax_i P(C_i | X) = argmax_i P(C_i)$$ et $$\prod_j P(X_j | C_i) / P(X) = argmax_i  P(C_i) \prod_j P(X_j | C_i)$$

## Quelques rappels de statistiques

* **Espérance \(expectation\) :** similaire à une moyenne en prenant en compte les probabilités : $$E[f (X)] = \sum_i f (X_i ) \cdot P (X_i )$$
* **Variance :** mesure de dispersion : $$var(X) = E[X-E[X]]^2 = E[X_{\mu}]^2$$ où $$\mu$$ est la moyenne/espérance de $$X$$
* **Ecart type \(standard deviation std\) :** $$\sigma = \sqrt{var(X)}$$
* **Covariance :** $$cov(X,Y)=E[(X-E[X])(Y-E[Y])]$$. Si $$X$$ et $$Y$$ sont indépendantes, $$cov(X, Y ) = 0$$.
* **Gaussienne ou distribution normale :** $$p(x) = \frac{1}{\sqrt{2 \pi \sigma}} exp( \frac{-(x-\mu)^2}{2 \sigma^2})$$
* **Central Limit Theorem :** convergence en loi de la somme d’une suite de variables aléatoires vers la loi normale



