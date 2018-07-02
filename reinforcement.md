# Apprentissage par renforcement

  - **Objectif**: maximiser la récompense totale des étapes successives
  - **Méthode**
	  - A chaque étape, l'algorithme propose la prochaine action
	  - Il obtient une récompense pour cette action
	  - Il essaie d'en déduire qu'elles sont les bonnes et mauvaises actions à partir de chacun des états
	  - Afin de ne pas se retrouver dans un maximum local, l'algorithme renvoie de temps en temps une action aléatoire

## Q-learning

$$Q(s,a)$$ est une estimation de la récompense lorsque nous appliquons l'action $$a$$ à partir de l'état $$s$$.

  - **Initialisation**
    - Initialiser $$Q(s,a)$$ pour tout $$s$$ et tout $$a$$ par une petite valeur aléatoire
    - Choisir aléatoirement un état initial $$s$$
  - **Algorithme:** Répéter les étapes suivantes jusqu'à convergence
    - Sélectionner une action $$a$$ à l'aide d'un soft-max sur $$Q(s,a)$$ (le soft-max donne la probabilité de choisir chacune des actions $$a$$ possible à partir de l'état $$s$$)
    - Effectuer l'action $$a$$, obtenir la récompense $$r$$ et atteindre le nouvel état $$s'$$
    - Mise à jour de $$Q(s,a)$$: $$Q(s,a) = (1-\mu) Q(s,a) + \mu (r + \gamma max_{a'} Q(s', a'))$$ avec 
      - $$r$$ la récompense reçue
      - $$\mu$$ la vitesse d'apprentissage comprise entre 0 et 1
      - $$\gamma$$ le facteur d'actualisation
    - Nouvel état $$s = s'$$

## Sarsa algorithme

Identique au Q-learning sauf pour la mise à jour de $$Q(s,a)$$: 
$$Q(s,a) = (1 - \mu) Q(s,a) + \mu (r + \gamma Q(s', a'))$$ où $$a'$$ est l'action effectuée sur le prochain état en suivant la même méthode (soft-max)

