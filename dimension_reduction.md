# Réduction de dimension

- **Objectifs**: décrire/visualiser des données, les décorréler, les débruiter, améliorer les performances d'un apprentissage
- **Méthodes**: feature  selection (garder les features qui sont le plus correlés à la target), feature  derivation (créer des nouvelles features), clustering (regrouper ensemble des données similaires)

Dans la suite, X est une matrice contenant l'ensemble des données dont chaque ligne correspond à une donnée.

## Linear Discriminant Analysis  LDA

  - Calculer le vecteur moyen pour chacune des classes noté $$\mu_c$$ et le vecteur moyen pour toutes les classes noté $$\mu$$
  - Mesurer l'éparpillement (scatter) des données: 
    - scatter  matrix pour la classe $$i$$: $$S_i = \sum_{x \in C_i} (x-\mu_i)(x-\mu_i)^T$$
    - within-class  scatter: $$S_W = mean(S_i)$$
    - between classes scatter: $$S_B = \sum_i (\mu_c - \mu) ( \mu_c - \mu)^T$$
  - Objectif: trouver la projection $$W$$ qui permet d'avoir le quotient $$(W^T S_B W)/(W^T S_W W)$$ aussi grand que possible 
  - Méthode (spectral decomposition): 
	 - si $$w$$ est un vecteur propre de $$S_W^{-1} S_B$$, le quotient sera égal à sa valeur propre
	 - Calculer les vecteurs propres et valeurs propres de $$S_W^{-1} S_B$$
	 - Conserver uniquement les vecteurs propres des valeurs propres les plus grandes pour construire la matrice de projection $$W$$ (chaque ligne est un vecteur propre)
  - Appliquer la réduction à un vecteur $$X$$: $$T = W x$$

## Principal Component  Analysis  PCA

Similaire à LDA mais pour des données non labellisées

  - Centrer et réduire les entrées (moyenne à 0 et variance à 1)
  - Objectif: trouver la projection $$W$$ qui permet de maximiser l'éparpillement des données: scatter  matrix  $$S = \sum_{x} W^T x^T x W$$
  - Méthode;
	  - Calculer les vecteurs propres et valeurs propres de $$X^T X$$
	  - Conserver uniquement les vecteurs propres des valeurs propres les plus grandes pour construire la matrice de projection $$W$$
  - Appliquer la réduction à un vecteur $$x$$: $$T = W x$$

Afin d'effectuer une transformation non linéaire lors de la réduction de dimension, un kernel peut être utilisé (similaire à l'utilisation de kernels pour les SVM).

## Independent  Component  Analysis  ICA

Dans l'algorithme PCA, les composantes de la projection sont orthogonales $$b_i \cdot b_j = 0$$ et non corrélées $$cov(b_i, b_j) = 0$$. Dans ICA, il est de plus imposé que les composantes de la projection soient indépendantes entre elles: $$E[b_i, b_j] = E[b_i]E[b_j]$$

