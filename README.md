# tp7_sql
1)	Les titres et dates de sortie des films du plus récent au plus ancien
```bash
SELECT f_titre, f_annee_sortie 
FROM Films
ORDER BY f_annee_sortie DESC;
```
2)	Les noms, prénoms et âges des acteurs/actrices de plus de 30 ans dans l'ordre alphabétique
```bash
SELECT a_nom, a_prenom, EXTRACT(YEAR FROM AGE(NOW(), a_date_naissance)) AS age
FROM Acteurs
WHERE EXTRACT(YEAR FROM AGE(NOW(), a_date_naissance)) > 30
ORDER BY a_nom, a_prenom;
```
3)	La liste des acteurs/actrices principaux pour un film donné
```bash
SELECT a_nom, a_prenom
FROM Acteurs
JOIN Joue_dans ON Acteurs.a_id = Joue_dans.acteur_id
JOIN Films ON Joue_dans.film_id = Films.f_id
WHERE Films.f_titre = 'Pulp Fiction'
AND a_role = 'Principal'
```
4)	La liste des films pour un acteur/actrice donné
```bash
SELECT f_titre, f_annee_sortie
FROM Films
JOIN Joue_dans ON Films.f_id = Joue_dans.film_id
JOIN Acteurs ON Joue_dans.acteur_id = Acteurs.a_id
WHERE Acteurs.a_id = 3;
```
5)	Ajouter un film
```bash
INSERT INTO Films (f_titre, f_duree, f_annee_sortie)
VALUES ('Iron Man', 120, 2008);
```
6)	Ajouter un acteur/actrice
```bash
INSERT INTO Acteurs (a_nom, a_prenom, a_role, a_date_naissance)
VALUES ('Robert ', 'Downey jr', 'Principal', '1965-01-01');
```
7)	Modifier un film
```bash
UPDATE Films
SET f_titre = 'DeadPool', f_duree = 120, f_annee_sortie = 2022
WHERE f_id = 1;
```
8)	Supprimer un acteur/actrice
```bash
DELETE FROM Acteurs
WHERE a_id = 2
```
9)	Afficher les 3 derniers acteurs/actrices ajouté(e)s
```bash
SELECT *
FROM Acteurs
ORDER BY a_cree_a DESC
LIMIT 3;
```
10)	Afficher le film le plus ancien
```bash
SELECT *
FROM Films
ORDER BY f_annee_sortie
LIMIT 1;
```
11)	Afficher l’acteur le plus jeune
```bash
SELECT *
FROM Acteurs
ORDER BY a_date_naissance DESC
LIMIT 1;
```
12)	Compter le nombre de films réalisés en 1990
13)	Faire la somme de tous les acteurs ayant joué dans un film
