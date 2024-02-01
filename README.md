# TP7_SQL

# Création des Tables
```bash
CREATE TABLE Realisateurs (
  r_id serial PRIMARY KEY,
  r_nom varchar(255) NOT NULL,
  r_prenom varchar(255) NOT NULL,
  r_cree_a timestamp DEFAULT current_timestamp
);

CREATE TABLE Acteurs (
  a_id serial PRIMARY KEY,
  a_nom varchar(255) NOT NULL,
  a_prenom varchar(255) NOT NULL,
  a_role varchar(255) NOT NULL,
  a_importance varchar(255) NOT NULL,
  a_date_naissance date NOT NULL,
  a_cree_a timestamp DEFAULT current_timestamp
);

CREATE TABLE Utilisateurs (
  u_nom varchar(255) NOT NULL,
  u_prenom varchar(255) NOT NULL,
  u_email varchar(255) PRIMARY KEY,
  u_mdp varchar(255) NOT NULL,
  u_cree_a timestamp DEFAULT current_timestamp
);

CREATE TABLE Films (
  f_id serial PRIMARY KEY,
  f_titre varchar(255) UNIQUE NOT NULL,
  f_duree integer,
  f_annee_sortie integer,
  f_cree_a timestamp DEFAULT current_timestamp
);

CREATE TABLE Joue_dans (
  film_id serial,
  acteur_id serial,
  PRIMARY KEY (film_id, acteur_id),
  FOREIGN KEY (film_id) REFERENCES Films(f_id) ON DELETE CASCADE,
  FOREIGN KEY (acteur_id) REFERENCES Acteurs(a_id) ON DELETE CASCADE,
  j_cree_a timestamp DEFAULT current_timestamp
);

CREATE TABLE Realise_par (
  film_id serial,
  realisateur_id serial,
  PRIMARY KEY (film_id),
  FOREIGN KEY (film_id) REFERENCES Films(f_id) ON DELETE CASCADE,
  FOREIGN KEY (realisateur_id) REFERENCES Realisateurs(r_id) ON DELETE CASCADE,
  r_cree_a timestamp DEFAULT current_timestamp
);

CREATE TABLE Prefere_par (
  utilisateur_email varchar(255),
  film_id serial,
  acteur_id serial,
  PRIMARY KEY (utilisateur_email),
  FOREIGN KEY (utilisateur_email) REFERENCES Utilisateurs(u_email) ON DELETE CASCADE,
  FOREIGN KEY (film_id) REFERENCES Films(f_id) ON DELETE CASCADE,
  FOREIGN KEY (acteur_id) REFERENCES Acteurs(a_id) ON DELETE CASCADE,
  p_cree_a timestamp DEFAULT current_timestamp
);
```
# Jeux de données
```bash
INSERT INTO Realisateurs (r_nom, r_prenom) VALUES
('Spielberg', 'Steven'),
('Nolan', 'Christopher'),
('Tarantino', 'Quentin');

-- Insert sample data into Acteurs Table
INSERT INTO Acteurs (a_nom, a_prenom, a_role, a_importance, a_date_naissance) VALUES
('Reeves', 'Keanu', 'Neo', 'Principale', '1964-09-02'),
('DiCaprio', 'Leonardo', 'Jack Dawson', 'Principale', '1974-11-11'),
('Hamill', 'Mark', 'Darth Vader', 'Secondaire', '1951-09-25');

-- Insert sample data into Utilisateurs Table
INSERT INTO Utilisateurs (u_nom, u_prenom, u_email, u_mdp) VALUES
('Smith', 'John', 'john.smith@email.com', 'password123'),
('Doe', 'Jane', 'jane.doe@email.com', 'secret456'),
('White', 'Walter', 'walter.white@email.com', 'blueSky');

-- Insert sample data into Films Table
INSERT INTO Films (f_titre, f_duree, f_annee_sortie) VALUES
('The Matrix', 136, 1999),
('Titanic', 195, 1997),
('Pulp Fiction', 154, 1994);

-- Insert sample data into Joue_dans Table
INSERT INTO Joue_dans (film_id, acteur_id) VALUES
(1, 1),
(2, 2),
(3, 3);

-- Insert sample data into Realise_par Table
INSERT INTO Realise_par (film_id, realisateur_id) VALUES
(1, 1),
(2, 2),
(3, 3);

-- Insert sample data into Prefere_par Table
INSERT INTO Prefere_par (utilisateur_email, film_id, acteur_id) VALUES
('john.smith@email.com', 1, 1),
('jane.doe@email.com', 2, 2),
('walter.white@email.com', 3, 3);
```

# Tâches
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
SELECT a_nom, a_prenom, a_importance
FROM Acteurs
JOIN Joue_dans ON Acteurs.a_id = Joue_dans.acteur_id
JOIN Films ON Joue_dans.film_id = Films.f_id
WHERE Films.f_titre = 'The Matrix'
AND a_importance = 'Principale'
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
```bash
SELECT COUNT(*) AS nombre_de_films
FROM Films
WHERE f_annee_sortie = 1990;
```
13)	Faire la somme de tous les acteurs ayant joué dans un film
```bash
SELECT COUNT(DISTINCT acteur_id) AS somme_acteurs
FROM Joue_dans;
```
