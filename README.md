# tp7_sql
1)	Les titres et dates de sortie des films du plus récent au plus ancien
```bash
SELECT f_titre, f_annee_sortie 
FROM Films
ORDER BY f_annee_sortie DESC;
```
2)	Les noms, prénoms et âges des acteurs/actrices de plus de 30 ans dans l'ordre alphabétique
3)	La liste des acteurs/actrices principaux pour un film donné
4)	La liste des films pour un acteur/actrice donné
5)	Ajouter un film
6)	Ajouter un acteur/actrice
7)	Modifier un film
8)	Supprimer un acteur/actrice
9)	Afficher les 3 derniers acteurs/actrices ajouté(e)s
10)	Afficher le film le plus ancien
11)	Afficher l’acteur le plus jeune
12)	Compter le nombre de films réalisés en 1990
13)	Faire la somme de tous les acteurs ayant joué dans un film
