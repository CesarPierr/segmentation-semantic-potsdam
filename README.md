# Segmentation sémantique d'images aériennes
## Pierre César & Bastien Gless

## Comment utiliser le notebook
Nous avon réutilisé le notebook fourni pour le projet.
Pour visualiser les résultats sans avoir à réentraîner le modèle entier, nous avons écrit la section "Test du dernier modèle enregistré". Elle utilise un modèle entraîné que nous avons enregistré auparavant.
Pour utiliser cette fonctionnalité, il faut avoir dans Drive le dossier "potsdam/models", contenant les fichiers "modele_.h5" (les données se situant dans le dossier "potsdam/Potsdam-data/Potsdam/30cm"). Un réglage de l'arborescence par l'utilisateur en fonction de sa propre arborescence pourrait être nécessaire.

## Choix de l'architecture de réseau
On utilise la structure de réseau de neurones U-net, dont la documentation se trouve ici : https://lmb.informatik.uni-freiburg.de/people/ronneber/u-net/ Ce réseau de convolution a été utilisé initialement pour des applications de segmentation sémantique dans le milieu biomédical. Il nous a paru sensé de prendre cette architecture existante pour notre réseau de neurones, car n'ayant pas d'expérience dans le domaine nous voulions opter pour une valeur sûre.

## Entraînement
L'entraînement du réseau prend entre 20min et une heure en fonction de la machine de l'utilisateur.
Par essais et erreurs, nous avons modifié les variables globales de l'entraînement (BATCH_SIZE, WINDOW_SIZE, OVERLAP, LENGTH_EPOCH), jusqu'à avoir un résultat satisfaisant.

## Analyse des résultats
### Performances
La précision du réseau sur l'ensemble de test est de _______
Ce résultat nous satisfait car les résultats pour le concours associé à la base de données sont d'environ 90% (même si les classes à détecter ne sont pas exactement les mêmes).
Analysons maintenant les erreurs de notre modèle

### Analyse des erreurs
La plupart des points où notre modèle se trompe correspondent à l'une des deux situations suivantes:
- Les frontières entre les zones de classes différentes, comme on pouvait s'en douter. Toutefois, ces frontières sont fines.
- Les zones classifiées en "autres". Sémantiquement, cette classe est différente des trois autres (bâtiments, routes, végétations), dans le sens où par définition elle ne porte pas de signification détectable et apprenable par le réseau. Il arrive donc que des zones de classe "autre" soient mal classifiées par notre modèle, et plus rarement que le modèle classifie certaines zones en "autre" alors qu'elles ne le sont pas.
Si notre modèle avait des applications réelles, nous pensons que ces erreurs seraient peu critiques : les routes et bâtiments sont bien détectés, cela ne poserait pas de problème pour des questions de sécurité.
