# Echantillonnage à partir de distribution de probabilités

## Distribution normale

  - **Générateur congruentiel linéaire**: $$x_{n+1} = (a \cdot x_n +c) \mod m$$ avec $$x_0$$ le seed et par exemple $$m=2^{32}$$, $$a=1\,664\,525$$ et $$c =1\,013\,904\,223$$.
  - **Mersenne Twister**: générateur de nombres pseudo-aléatoires basé sur un TGSFR (twisted generalised shift feedback register, un type particulier de registre à décalage à rétroaction). Il est très utilisé dans l'industrie à l'exception du domaine de la cryptographie car les algorithmes tels que Berlekamp-Massey ou Reed-Sloane permettent d’en prédire le comportement

## Distribution Gaussienne

  - **Méthode de Box-Muller**: génération de paires de nombres aléatoires à distribution normale centrée réduite, à partir d'une source de nombres aléatoires de loi uniforme.
	  - $$U_1, U_2$$ deux nombre aléatoires selon une loi uniforme
	  - Soit $$\theta = 2 \pi U_1$$ et $$r = \sqrt{-2 \ln (U_2)}$$
	  - $$x=r \cos \theta$$ et $$y = r \sin \theta$$ des variables aléatoires indépendantes suivant une loi Gaussienne de moyenne 0 et de variance 1.

## Distribution de probabilités

**Méthodes de Monte Carlo par chaines de Markov**: classe de méthodes d'échantillonnage à partir de distributions de probabilité. Ces méthodes de Monte-Carlo se basent sur le parcours de chaînes de Markov qui ont pour lois stationnaires les distributions à échantillonner.Certaines méthodes utilisent des marches aléatoires sur les chaînes de Markov (algorithme de Metropolis-Hastings, échantillonnage de Gibbs), alors que d'autres algorithmes, plus complexes, introduisent des contraintes sur les parcours pour essayer d'accélérer la convergence (Monte Carlo Hybride, Surrelaxation successive).

Principe: On se place dans un espace vectoriel $$\epsilon $$ de dimension finie $$n$$. On veut générer aléatoirement des vecteurs $$x$$ suivant une distribution de probabilité $$\pi$$. On veut donc avoir une suite de $$N$$ vecteurs $$(x_{0},x_{1}, ... ,x_{N-1})$$ telle que la distribution des $$x_{i}$$ approche $$\pi$$.

Les méthodes de Monte-Carlo par chaînes de Markov consistent à générer un vecteur $$x_{i}$$ uniquement à partir de la donnée du vecteur $$x_{i-1}$$ ; c'est donc un processus sans mémoire, ce qui caractérise les chaînes de Markov. Il faut donc trouver un générateur aléatoire avec une distribution de probabilité $$q_{x_{i-1}}$$ qui permette de générer $$x_{i}$$ à partir de $$x_{i-1}$$. On remplace ainsi le problème de génération avec une distribution $$\pi$$ par $$N$$ problèmes de génération avec des distributions $$q_{x_{i}}$$, que l'on espère plus simples.
