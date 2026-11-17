# Réflexion — TP2 : GIT
1. Quel est le meilleur des 3 modèles ? Peut-on le prouver ?
-> Oui — git log montre les 3 commits distincts, chacun avec son
message explicite
2. Peut-on redonner exactement le modèle de l'Essai 1 ?
-> Oui — git checkout <commit> -- churn_model.ipynb :
3. Un camarade peut-il reproduire notre travail sur une autre machine ?
-> Oui — git clone donne une copie identique du code et des données

# Réflexion — TP3 : MLflow
1. Quel est le meilleur modèle ? Peux-tu le
prouver ?
Oui : je trie les runs par f1 avec l’interface MLflow ou search_runs. Le résultat est daté et conservé, donc la preuve reste disponible à tout moment.
2. Peux-tu redonner exactement le modèle de
l'Essai 1 ?
->Oui — mlflow.sklearn.load_model("runs:/<id>/model") recharge le
modèle d'un run précis
3. Un camarade peut-il reproduire ton travail sur
une autre machine ?
-> En partie — le code (Git), les paramètres et les versions de
bibliothèques (requirements.txt du run) sont connus ; Mais rien ne garantit qu’il aura exactement le même environnement d’exécution (même système, mêmes versions installées) — ce problème sera résolu plus tard avec Docker.

# Réflexion — TP4 : registry de modeles et API FastAPI
1. Comment désigner officiellement le modèle à utiliser ?
Je pose un alias (champion) sur la version voulue dans le Registry. Le code appelle models:/churn-model@champion, et pour changer de modèle, je déplace juste l’alias.
2. Comment une application peut-elle utiliser le modèle ?
Via l’API : une requête POST à /predict avec un JSON, et la réponse contient la prédiction .
3. Que se passe-t-il quand on change de champion ?
Je déplace l’alias vers la nouvelle version et je redémarre l’API. Le code de l’API et des applications clientes ne change pas.