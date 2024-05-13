![Dictionnaire de données](../doc/Assets/Images/datas-dictionary.jpeg)

# Dictionnaire de données

Un dictionnaire de données est un outil crucial pour la gestion des données qui décrit minutieusement la structure des bases de données. Il fournit des détails précis sur les tables, colonnes, types de données et contraintes, garantissant ainsi une standardisation et une cohérence des données dans l'application.

Il sert de référence essentielle pour les développeurs, les administrateurs de bases de données et les analystes, aidant à préserver l'intégrité des données, à faciliter les modifications structurelles et à assurer la conformité réglementaire.

### Dictionnaire de Données avec Exemples

| **Entité**     | **Attribut**     | **Type de Données** | **Longueur** | **Contraintes**                       | **Description**                                      | **Exemple**                                  |
| -------------- | ---------------- | ------------------- | ------------ | ------------------------------------- | ---------------------------------------------------- | -------------------------------------------- |
| **User**       | ID_User          | UUID                |              | PRIMARY KEY, NOT NULL                 | Identifiant unique pour chaque utilisateur           | "a0eebc99-9c0b-4ef8-bb6d-6bb9bd380a11"       |
|                | Firstname        | VARCHAR             | 60           | NOT NULL                              | Prénom de l'utilisateur                              | "Emmy"                                       |
|                | Lastname         | VARCHAR             | 60           | NOT NULL                              | Nom de famille de l'utilisateur                      | "Durand"                                     |
|                | Birthdate        | DATE                |              | NOT NULL                              | Date de naissance de l'utilisateur                   | "1990-05-15"                                 |
|                | Email            | VARCHAR             | 60           | NOT NULL                              | Adresse email de l'utilisateur                       | "emmy.durand@example.com"                    |
|                | Password         | VARCHAR             | 60           | NOT NULL                              | Mot de passe de l'utilisateur                        | "s3cureP@ss!"                                |
|                | User_Type        | VARCHAR             | 60           | NOT NULL                              | Type de l'utilisateur                                | "Instructor"                                 |
|                | ID_Address       | INT                 |              | NOT NULL, FOREIGN KEY                 | Clé étrangère référençant l'adresse de l'utilisateur | 102                                          |
| **Address**    | ID_Address       | INT                 |              | AUTO-INCREMENT, PRIMARY KEY, NOT NULL | Identifiant unique pour chaque adresse               | 102                                          |
|                | Address_Number   | VARCHAR             | 50           | NOT NULL                              | Numéro de bâtiment ou de maison                      | "42"                                         |
|                | Address_Street   | VARCHAR             | 100          | NOT NULL                              | Nom de la rue                                        | "rue Belfort"                                |
|                | Address_Postcode | VARCHAR             | 20           | NOT NULL                              | Code postal de l'adresse                             | "69004"                                      |
|                | Address_City     | VARCHAR             | 50           | NOT NULL                              | Ville de l'adresse                                   | "Lyon"                                       |
| **Role**       | ID_Role          | INT                 |              | AUTO-INCREMENT, PRIMARY KEY, NOT NULL | Identifiant unique pour chaque rôle                  | 1                                            |
|                | Name_Role        | VARCHAR             | 50           | NOT NULL                              | Nom du rôle                                          | "Administrator"                              |
| **Instructor** | ID_Instructor    | UUID                |              | PRIMARY KEY, NOT NULL                 | Identifiant unique pour chaque instructeur           | "c0eebc99-9c0b-4ef8-bb6d-6bb9bd380a12"       |
|                | Instructor_Code  | VARCHAR             | 50           | NOT NULL                              | Code unique de l'instructeur                         | "INST001"                                    |
|                | ID_User          | UUID                |              | NOT NULL, FOREIGN KEY                 | Clé étrangère référençant l'utilisateur              | "a0eebc99-9c0b-4ef8-bb6d-6bb9bd380a11"       |
| **Formation**  | ID_Formation     | INT                 |              | AUTO-INCREMENT, PRIMARY KEY, NOT NULL | Identifiant unique pour chaque formation             | 10                                           |
|                | Title_Formation  | VARCHAR             | 60           | NOT NULL                              | Titre de la formation                                | "Introduction à SQL"                         |
|                | Description      | TEXT                |              | NOT NULL                              | Description détaillée de la formation                | "Covers basic SQL commands and operations."  |
|                | Status_Formation | VARCHAR             | 50           | NOT NULL                              | Statut actuel de la formation                        | "Active"                                     |
| **Module**     | ID_Module        | INT                 |              | AUTO-INCREMENT, PRIMARY KEY, NOT NULL | Identifiant unique pour chaque module                | 5                                            |
|                | Title_Module     | VARCHAR             | 60           | NOT NULL                              | Titre du module                                      | "Database Basics"                            |
|                | Content_Module   | TEXT                |              | NOT NULL                              | Contenu du module                                    | "Fundamentals of database structures."       |
|                | Objectif         | TEXT                |              | NOT NULL                              | Objectifs pédagogiques du module                     | "Understand core database concepts."         |
|                | Status_Module    | VARCHAR             | 50           | NOT NULL                              | Statut actuel du module                              | "In Development"                             |
| **Lesson**     | ID_Lesson        | INT                 |              | AUTO-INCREMENT, PRIMARY KEY, NOT NULL | Identifiant unique pour chaque leçon                 | 30                                           |
|                | Title_Lesson     | VARCHAR             | 60           | NOT NULL                              | Titre de la leçon                                    | "SQL Joins"                                  |
|                | Content_Lesson   | TEXT                |              | NOT NULL                              | Contenu textuel de la leçon                          | "Explains how to use SQL joins effectively." |
|                | Video            | VARCHAR             | 200          | NOT NULL                              | URL de la vidéo associée                             | "http://example.com/sql-joins-video"         |
|                | Image            | VARCHAR             | 200          | NOT NULL                              | URL de l'image associée                              | "http://example.com/sql-joins-image"         |
|                | Tag              | VARCHAR             | 50           | NOT NULL                              | Tag pour catégoriser la leçon                        | "Intermediate"                               |
|                | Status_Lesson    | VARCHAR             | 50           | NOT NULL                              | Statut actuel de la leçon                            | "Active"                                     |

[🔝 Retour à la Table des matières](../README.md#table-des-matieres)
