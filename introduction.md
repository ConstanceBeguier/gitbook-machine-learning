# Introduction

## Types de machine learning

**Apprentissage supervisé (classification et régression):** à partir d'une BDD d'apprentissage avec des données et leurs labels, il faut généraliser afin de donner un label à des données jamais vues
 - CNN, SVM, arbres de décision (ID3, C5, CART), régression linéaire
 - AdaBoost, Bagging
**Apprentissage non supervisé (clustering):** partitionner les données afin que les données dans une même partition soient proches entre elles (aient quelque chose en commun) et les données provenant de deux partitions différentes soient éloignées
  - k-means, algorithme EM, regroupement hiérarchique (arbre)
**Apprentissage par renforcement:** apprentissage d'un bon comportement à partir d'observations/récompenses. A chaque étape, l'algorithme propose une action et le système donne un score à cette action (indiquant si l'action est bénéfique ou pas) sans indiquer comment améliorer ce score.
  - Q-learning, Hidden Markov Model (Viterbi et ...)
**Apprentissage évolutionniste:** le principe s'inspire de la théorie de l'évolution pour résoudre des problèmes diverses. La théorie de l'évolution repose sur le fait que les organismes s'adaptent pour améliorer leur taux de survie et celui de leurs descendants
  - algorithmes génétiques
**Réduction de dimension (compression):** réduire la dimension des entrées afin de réduire le stockage toute en gardant un maximum d'information
  - Stratégies d'évolution, Programmation évolutionnaire, Algorithmes génétiques
**Système de recommandations:** filtrage de l'information visant à présenter les éléments d'information (films, musique, livres, news, images, pages Web, etc) qui sont susceptibles d'intéresser l'utilisateur
  - collaborative filtering, content-based filtering, hybrid algorithm

