# Hidden Markov Models

## Définitions

**Modèle de Markov:**
  - Le système est dans un état à chaque instant
  - Le temps est discret
  - Matrice de transition: $$a_{i,j}$$: probabilité d'être dans l'état $$j$$ sachant que nous étions dans l'état $$i$$ à l'étape précédente
  - Matrice d'émission: $$b_{i,k}$$: probabilité d'observer $$k$$ sachant que nous sommes dans l'état $$i$$

Dans un HMM, les états ne sont pas observables, seulement les observations/émissions sont observables.

Trois problème pour les HMMs:
  - **Problème 1**:Quelle est la proba d'une séquence d'observations donnée ?
  - **Problème 2**: Quelle est la séquence d'états la plus probable étant donné une séquence d'observations ?
  - **Problème 3**: Comment estimer la matrice de transition $$A$$ et la matrice d'émission $$B$$ à partir de plusieurs séquences d'observations ?

Dans les problèmes 1 et 2, nous connaissons $$A$$ et $$B$$.

## Forward and backward algorithm (problème 1)

**Forward algorithm**

  - **Idée**: calculer $$\alpha _{s,t}$$ : probabilité d'être dans l'état $$s$$ à $$t$$ et d'avoir observé $$o_{1}, o_{2}, ..., o_{t}$$
  - **Algorithme**:
	  - Initialilsation: $$\alpha _{s,1} = b_{s,o_{1}} \pi _{s}$$ avec $$pi_{s}$$ la probabilité de partir de l'état $$s$$
	  - Récursion: $$\alpha _{s,t} = b_{s,o_{t}} \sum_{i} a_{i,s} \alpha _{i,t-1}$$
	  - Terminaison: $$P(o_{1},...,o_{T}|A,B) = \sum_{i} \alpha _{i,T}$$

**Backward algorithm**

C'est un algo alternatif calculant à partir de la fin de la séquence.

$$\beta _{s,t}$$: probabilité d'être dans l'état s à t et d'observer par la suite $$o_{t+1}, o_{t+2},..., o_{T}$$

 ## Viterbi algorithm (problème 2)

  - **Idée**: calculer $$v_{s,t}$$: probabilité du chemin le plus probable qui se termine à l'état $$s$$ à $$t$$
  - **Algorithme**:
	  - Initialisation: $$v_{s,1} = b_{s,o_{1}} \pi _{s}$$
	  - Forward calculs: $$v_{s,t} = b_{s,o_{t}} max_{i} v_{i,t-1} a_{i,s}$$
	  - Backward calculs: Suivre le chemin ayant le plus grand $$v_{s,T}$$

## Baum Welch Algorithm (problème 3)

  - **Principe**: Expectation-Maximization (EM) méthode pour adapter les paramètres du modèle $$(a_{i,j},b_{i,k})$$ à partir d'un grand nombre de séquences d'observations $$(o_{1},o_{2},...,o_{T})$$
	  - Expectation: Utiliser alternativement les algorithmes forward et backward pour estimer les probabilités de transitions et d'émissions
	  - Maximization: Utiliser ces transitions et émissions pour mettre à jour le modèle
  - **Idée**: calculer $$\gamma _{i,j,t}$$: probabilité qu'à $$t$$ nous suivons la transition de $$i$$ à $$j$$: $$\gamma _{i,j,t} = \frac{\alpha _{i,t} a_{i,j} b_{j,o_{t+1}} \beta_{j,t+1}}{\sum_{i,j} \alpha _{i,t} a_{i,j} b_{i,o_{k}} \beta_{j,t+1}}$$
  - **Mise à jour des paramètres**: 
$$a_{i,j} = \frac{\sum_{t} \gamma _{i,j,t}}{\sum_{t,m} \gamma _{i,m,t}}$$
$$b_{i,k} = \frac{\sum_{t,o_{t}=k} \sum_{m} \gamma _{i,m,t}}{\sum_{t,m} \gamma _{i,m,t}}$$

