# sql-server-data-base

créer la base de donnée :
```sql
CREATE DATABASE team_builder
GO
```
créer les tables : 

CREATE TABLE [personnes] (
  [id] int PRIMARY KEY IDENTITY(1, 1),
  [prenom] varchar(50),
  [nom] varchar(50)
)
GO

CREATE TABLE [team] (
  [id] int PRIMARY KEY IDENTITY(1, 1),
  [nom] varchar(50),
  [projet] varchar(50),
  [personne_id] int
)
GO

CREATE TABLE [as_team] (
  [personne_id] int,
  [team_id] int,
  PRIMARY KEY ([personne_id], [team_id])
)
GO

ALTER TABLE [team] ADD FOREIGN KEY ([personne_id]) REFERENCES [personnes] ([id])
GO

ALTER TABLE [as_team] ADD FOREIGN KEY ([personne_id]) REFERENCES [personnes] ([id])
GO

ALTER TABLE [as_team] ADD FOREIGN KEY ([team_id]) REFERENCES [team] ([id])
GO

insérer les données :

INSERT INTO personnes (nom, prenom) VALUES
	('Bratt', 'Pitt'),
	('Bruce', 'Willis'),
	('Nicolas', 'Cage'),
	('Angelina', 'jolie'),
	('Tom', 'Cruise'),
	('Tom', 'Hanks'),
	('Bob', 'Dylan'),
	('Johnny', 'Cash'),
	('Jimmy', 'Hendrix');

INSERT INTO team (nom, projet, personne_id) VALUES
	('Team A', 'Projet site internet Mairie', 1),
	('Team B', 'Projet CRM', 4),
	('Team C', 'Projet ERP', 7);

INSERT INTO as_team (personne_id, team_id) VALUES 
	(1,1),
	(2,1),
	(3,1),
	(4,2),
	(5,2),
	(6,2),
	(7,3),
	(8,3),
	(9,3);

 requête pour afficher la team 1:
 SELECT p.*
FROM personnes p
JOIN as_team at ON p.id = at.personne_id
WHERE at.team_id = 1;


