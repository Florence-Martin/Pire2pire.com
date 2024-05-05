![Dictionnaire de données](../doc/Assets/Images/datas-dictionary.jpeg)

# Dictionnaire de données

Un dictionnaire de données est un outil crucial pour la gestion des données qui décrit minutieusement la structure des bases de données. Il fournit des détails précis sur les tables, colonnes, types de données et contraintes, garantissant ainsi une standardisation et une cohérence des données dans l'application.

Il sert de référence essentielle pour les développeurs, les administrateurs de bases de données et les analystes, aidant à préserver l'intégrité des données, à faciliter les modifications structurelles et à assurer la conformité réglementaire.

| Entité     | Attribut         | Type de Données | Longueur | Contraintes                   | Description                                                   | Exemple                     |
| ---------- | ---------------- | --------------- | -------- | ----------------------------- | ------------------------------------------------------------- | --------------------------- |
| Role       | ID_Role          | SERIAL          |          | PRIMARY KEY, NOT NULL         | Identifiant unique pour chaque rôle                           | 1                           |
|            | Name_Role        | VARCHAR         | 50       | NOT NULL                      | Nom du rôle                                                   | "Administrator"             |
| Formation  | ID_Formation     | SERIAL          |          | PRIMARY KEY, NOT NULL         | Identifiant unique pour chaque formation                      | 10                          |
|            | Title_Formation  | VARCHAR         | 50       | NOT NULL                      | Titre de la formation                                         | "Introduction to SQL"       |
|            | Description      | VARCHAR         | 2000     | NOT NULL                      | Description détaillée de la formation                         | "Covers basic SQL commands" |
|            | Status_Formation | VARCHAR         | 50       | NOT NULL                      | Statut actuel de la formation                                 | "Published"                 |
| Module     | ID_Module        | SERIAL          |          | PRIMARY KEY, NOT NULL         | Identifiant unique pour chaque module                         | 5                           |
|            | Title_Module     | VARCHAR         | 50       | NOT NULL                      | Titre du module                                               | "Database Basics"           |
|            | Content_Module   | VARCHAR         | 2000     | NOT NULL                      | Contenu du module                                             | "Introduction to databases" |
|            | Version          | VARCHAR         | 50       | NOT NULL                      | Version du module                                             | "v1.2"                      |
|            | Objectif         | VARCHAR         | 2000     | NOT NULL                      | Objectif du module                                            | "Understand DB concepts"    |
|            | Status_Module    | VARCHAR         | 50       | NOT NULL                      | Statut actuel du module                                       | "Draft"                     |
| Lesson     | ID_Lesson        | SERIAL          |          | PRIMARY KEY, NOT NULL         | Identifiant unique pour chaque leçon                          | 30                          |
|            | Title_Lesson     | VARCHAR         | 50       | NOT NULL                      | Titre de la leçon                                             | "SQL Joins"                 |
|            | Content_Lesson   | VARCHAR         | 2000     | NOT NULL                      | Contenu textuel de la leçon                                   | "How to use SQL Joins"      |
|            | Video            | VARCHAR         | 2000     | NOT NULL                      | URL de la vidéo associée                                      | "http://example.com/video"  |
|            | Image            | VARCHAR         | 2000     | NOT NULL                      | URL de l'image associée                                       | "http://example.com/image"  |
|            | Tag              | VARCHAR         | 50       | NOT NULL                      | Tag pour catégoriser la leçon                                 | "Advanced"                  |
|            | Status_Lesson    | VARCHAR         | 50       | NOT NULL                      | Statut actuel de la leçon                                     | "Active"                    |
| Status     | ID_Status        | SERIAL          |          | PRIMARY KEY, NOT NULL         | Identifiant unique pour chaque statut                         | 2                           |
|            | Type_Status      | VARCHAR         | 50       | NOT NULL                      | Description du statut                                         | "Completed"                 |
| Address    | ID_Address       | SERIAL          |          | PRIMARY KEY, NOT NULL         | Identifiant unique pour chaque adresse                        | 15                          |
|            | Address_Number   | VARCHAR         | 50       | NOT NULL                      | Numéro de bâtiment ou de maison                               | "12"                        |
|            | Address_Street   | VARCHAR         | 100      | NOT NULL                      | Nom de la rue                                                 | "des Concepteurs"           |
|            | Address_Postcode | INT             |          | NOT NULL                      | Code postal de l'adresse                                      | 69004                       |
|            | Address_City     | VARCHAR         | 50       | NOT NULL                      | Ville de l'adresse                                            | "LYON"                      |
| User       | ID_User          | SERIAL          |          | PRIMARY KEY, NOT NULL         | Identifiant unique pour chaque utilisateur                    | 100                         |
|            | Firstname        | VARCHAR         | 50       | NOT NULL                      | Prénom de l'utilisateur                                       | "Emmy"                      |
|            | Lastname         | VARCHAR         | 50       | NOT NULL                      | Nom de famille de l'utilisateur                               | "Durand"                    |
|            | Birthdate        | DATE            |          | NOT NULL                      | Date de naissance de l'utilisateur                            | "2000-01-24"                |
|            | Email            | VARCHAR         | 50       | NOT NULL                      | Adresse email de l'utilisateur                                | "emmy-durand@example.com"   |
|            | Password         | VARCHAR         | 50       | NOT NULL                      | Mot de passe de l'utilisateur                                 | "password123"               |
|            | User_Type        | VARCHAR         | 50       | NOT NULL                      | Type de l'utilisateur                                         | "Apprenant"                 |
|            | ID_Address       | INT             |          | NOT NULL, FOREIGN KEY         | Clé étrangère référençant Address                             | 15                          |
| Instructor | ID_Instructor    | SERIAL          |          | PRIMARY KEY, NOT NULL         | Identifiant unique pour chaque instructeur                    | 20                          |
|            | Instructor_Code  | VARCHAR         | 50       | NOT NULL                      | Code unique de l'instructeur                                  | "INST001"                   |
|            | ID_User          | INT             |          | NOT NULL, UNIQUE, FOREIGN KEY | Clé étrangère référençant User                                | 100                         |
| Register   | ID_Formation     | INT             |          | NOT NULL, FOREIGN KEY         | Clé étrangère référençant Formation                           | 10                          |
|            | ID_User          | INT             |          | NOT NULL, FOREIGN KEY         | Clé étrangère référençant User                                | 100                         |
|            | Inscription_Date | DATE            |          | NOT NULL                      | Date à laquelle l'utilisateur s'inscrit à la formation        | "2023-05-14"                |
|            | Is_Active        | BOOL            |          | NOT NULL DEFAULT true         | Indique si l'inscription est active                           | true                        |
|            | End_Date         | DATE            |          | NOT NULL                      | Date de fin de l'inscription                                  | "2024-05-01"                |
| Consist    | ID_Module        | INT             |          | NOT NULL, FOREIGN KEY         | Clé étrangère référençant Module                              | 5                           |
|            | ID_Formation     | INT             |          | NOT NULL, FOREIGN KEY         | Clé étrangère référençant Formation                           | 10                          |
| Include    | ID_Module        | INT             |          | NOT NULL, FOREIGN KEY         | Clé étrangère référençant Module                              | 5                           |
|            | ID_Lesson        | INT             |          | NOT NULL, FOREIGN KEY         | Clé étrangère référençant Lesson                              | 30                          |
| Have       | ID_Role          | INT             |          | NOT NULL, FOREIGN KEY         | Clé étrangère référençant Role                                | 1                           |
|            | ID_User          | INT             |          | NOT NULL, FOREIGN KEY         | Clé étrangère référençant User                                | 100                         |
| Validate   | ID_Lesson        | INT             |          | NOT NULL, FOREIGN KEY         | Clé étrangère référençant Lesson                              | 30                          |
|            | ID_User          | INT             |          | NOT NULL, FOREIGN KEY         | Clé étrangère référençant User                                | 100                         |
|            | Completion_Date  | DATE            |          | NOT NULL                      | Date de validation de la leçon                                | "2023-05-15"                |
|            | IsCompleted      | BOOL            |          | NOT NULL DEFAULT true         | Indique si la leçon a été complétée                           | true                        |
| Progress   | ID_Formation     | INT             |          | NOT NULL, FOREIGN KEY         | Clé étrangère référençant Formation                           | 10                          |
|            | ID_User          | INT             |          | NOT NULL, FOREIGN KEY         | Clé étrangère référençant User                                | 100                         |
|            | Percentage       | INTEGER         |          | NOT NULL                      | Pourcentage de progression de l'utilisateur dans la formation | 75                          |
| Give       | ID_Formation     | INT             |          | NOT NULL, FOREIGN KEY         | Clé étrangère référençant Formation                           | 10                          |
|            | ID_Module        | INT             |          | NOT NULL, FOREIGN KEY         | Clé étrangère référençant Module                              | 5                           |
|            | ID_Lesson        | INT             |          | NOT NULL, FOREIGN KEY         | Clé étrangère référençant Lesson                              | 30                          |
|            | ID_Status        | INT             |          | NOT NULL, FOREIGN KEY         | Clé étrangère référençant Status                              | 2                           |

[🔝 Retour à la Table des matières](../README.md#table-des-matieres)
