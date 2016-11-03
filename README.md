# System-de-recommandation-en-Python
Projet dans le cadre du module Data Science à l'ENSIIE en 3A. Le projet consiste à la mise en place d'un système de recommandation qui se base sur les algorithmes Collaborative filtering en python.
# Introduction:
L'objectif de ce projet était la création d’un système de recommandation performant et scalable. On a mesuré la performance avec les indice d’évaluation tels que le RMSE (Root mean square error) et la scalabilité par la possibilité d’appliquer nos algorithmes sur un jeu de données de 10 millions d’observations. 
Pour le faire, on a utilisé des modèles qui se basent sur la similarité (Memory Based) et des modèles qui se basent sur la factorisation des matrices (Model Based). 
On a appliqué ces algorithmes sur une partie de notre jeu de données, mais en montant dans les dimensions, Python n’a pas accepté une matrice  de 7636 lignes et 1264 colonnes. 
Notre solution était de passer des matrices aux tuples. Une solution qui a été efficace et qui retourne des résultats avec un bon temps d'exécution et un petit taux d’erreur.
# Modélisation:
Il existe deux type de système de recommandation:
-Le Content Based: qui se base sur les caractéristiques des users/items (on va pas l’utiliser vu qu’on n’a pas ces données.)
Le Collaboratif Filtering: qui se base sur seulement la note attribué par l'utilisateur sur l'item. 
 
Il existe deux type de recommandation Collaboratif Filtering:
Memory Based
Model Based
# CF: Memory Based:
Les modèles Memory based se base sur la similarité calculé par les différentes métriques d’évaluation. Pour nous, on a utilisé le Cosine similar et le citybloc.
Il existe deux type de Memory Model:
User-Item based : cet algorithme va prendre un utilisateur, trouve les utilisateur les plus similaires à lui, Puis recommande les items aimé par ces utilisateurs (ça prend un user et retourne des items). En général on l’utilise pour dire "Les utilisateurs qui sont similaires à vous, ont aimé aussi ..."
Item-Based : prend un item, cherche les utilisateurs qui ont aimé cet item et recommande les items aimé par ces utilisateurs (ça prend un item et retourne une liste des items). En général on l’utilise pour dire "Les utilisateurs qui ont aimé ça, ont aimé aussi ..."

# CF:Model Based:
Les Model Based se basent sur la multiplication de matrices ou Matrix Factorisation (MF) : Méthode d'apprentissage non supervisé de décomposition et de réduction de dimensionnalité en utilisant les caractères latents (k : espace des caractères cachés)


Le but de ces algorithmes est de trouver les préférences latentes des utilisateurs ( sous forme d’une matrice P) et des items (sous forme d’une matrice Q) à partir des notes attribués. Puis, la multiplication de ces deux matrices de structure de faible rang donne la matrice de prédiction.  


Une fois c’est fait, selon la méthode qu’on va utiliser, on améliore P et Q pour avoir un produit qui est conforme à la matrice des notes originale. Voilà les différentes méthodes qu’on a utilisé:
SVD Singular Vector Decomposition: X=U x S x V.T pour le faire on a utilisé la librairy scipy.sparse.linalg. U présente la matrice User-Latent et V.T la matrice Item-Latent 
 NMF Non-Negative Matrix Factorisation: On construit le modèle, on lui fait l’apprentissage avec la base train (pour obtenir P et Q). On a utilisé cet algorithme avec la library sklearn.decomposition

ALS Alternating Least Squares & SGD Stochastic Gradient Descent : qui présentent deux manières pour minimiser l’erreur de régularisation carré. Le principe est de prendre aléatoirement P et Q et appliquant selon le cas une formule mathématique pour rendre le produit le plus proche de la matrice originale.
# Conclusion:
Pour résoudre notre problème on a utilisé tous les modèles qu’on a trouvé pour comparer et valider les résultats théoriques.
Pour les Memory Based:
les modèles sont facile à implémenter, ils génèrent des bonnes résultats mais ils ne résolvent pas les problèmes de Cold Start(pas d’informations sur les users & items), de sparsity(rareté des données) et de scalability (monter dans les dimensions). 
Pour les Model Based:
Ils ont résolu le problème de sparsity.  Et chaque algorithme a ces points faibles et ces points forts.
Pour l’utilisation de la matrice de factorisation finale: 
On a résolu le problème de scalability et de sparsity. 
Mais on a pas exploité la variable date_ratings pour que nos tests soient plus significatifs

