# Script PostgreSQL

Ce script **SQL** crée et configure les tables nécessaires à notre système de gestion de formations.  
Les tables couvrent divers aspects du système, incluant les utilisateurs, les rôles, les adresses, les instructeurs, les formations, les modules, les leçons, les statuts de publication et les tags.  
Chaque table est définie avec des contraintes primaires et étrangères pour garantir l’intégrité référentielle des données. Des index sont également créés pour optimiser les performances des requêtes fréquentes.  
Le script exploite des fonctionnalités spécifiques de PostgreSQL, comme l’utilisation de UUIDs et l’extension “uuid-ossp”, pour améliorer la gestion des identifiants uniques.

## Dépendance

Ce script nécessite l'activation de l'extension "uuid-ossp" pour la génération des UUID (identifiants uniques non séquentiels).

## Script PostgreSQL

```sql
------------------------------------------------------------
--        Script Postgre
------------------------------------------------------------
------------------------------------------------------------
-- Extension "uuid-ossp"
------------------------------------------------------------
CREATE EXTENSION IF NOT EXISTS "uuid-ossp";


------------------------------------------------------------
-- Table: Role
------------------------------------------------------------
CREATE TABLE public.Roles(
	roleId     SERIAL NOT NULL UNIQUE ,
	nameRole   VARCHAR (50) NOT NULL UNIQUE ,
	CONSTRAINT Roles_PK PRIMARY KEY (roleId)
);


------------------------------------------------------------
-- Table: Publication_Status
------------------------------------------------------------
CREATE TABLE public.PublicationStatus(
	publicationStatusId     SERIAL NOT NULL UNIQUE ,
	typePublicationStatus   VARCHAR (50) NOT NULL UNIQUE ,
	CONSTRAINT PublicationStatus_PK PRIMARY KEY (publicationStatusId)
);

------------------------------------------------------------
-- Table: Addresses
------------------------------------------------------------
CREATE TABLE public.Addresses(
	addressId         SERIAL NOT NULL UNIQUE ,
	addressNumber     VARCHAR (50) NOT NULL ,
	addressStreet     VARCHAR (100) NOT NULL ,
	addressPostcode   VARCHAR (20) NOT NULL ,
	addressCity       VARCHAR (50) NOT NULL ,
	addressCountry    VARCHAR (50) NOT NULL ,
	CONSTRAINT Addresses_PK PRIMARY KEY (addressId)
);

------------------------------------------------------------
-- Table: User
------------------------------------------------------------
CREATE TABLE public.Users(
	userUuid    VARCHAR (36) NOT NULL UNIQUE DEFAULT uuid_generate_v4(),
	firstname   VARCHAR (50) NOT NULL ,
	lastname    VARCHAR (50) NOT NULL ,
	birthdate   DATE NOT NULL ,
	email       VARCHAR (50) NOT NULL UNIQUE ,
	password    VARCHAR (50) NOT NULL ,
	userType    VARCHAR (50) NOT NULL ,
	addressId   INT  NOT NULL  ,
	CONSTRAINT Users_PK PRIMARY KEY (userUuid)

	,CONSTRAINT Users_Addresses_FK FOREIGN KEY (addressId) REFERENCES public.Addresses(addressId)
);

CREATE INDEX idx_userEmail ON public.Users(email);
------------------------------------------------------------
-- Table: Instructor
------------------------------------------------------------
CREATE TABLE public.Instructors(
	instructorUuid   VARCHAR (36) NOT NULL UNIQUE DEFAULT uuid_generate_v4(),
	instructorCode   VARCHAR (50) NOT NULL UNIQUE ,
	userUuid         VARCHAR (36) NOT NULL UNIQUE ,
	CONSTRAINT Instructors_PK PRIMARY KEY (instructorUuid)

	,CONSTRAINT Instructors_Users_FK FOREIGN KEY (userUuid) REFERENCES public.Users(userUuid)
	,CONSTRAINT Instructors_Users_AK UNIQUE (userUuid)
);

CREATE INDEX idx_instructorCode ON public.Instructors(instructorCode);
------------------------------------------------------------
-- Table: Formation
------------------------------------------------------------
CREATE TABLE public.Formations(
	formationId                  SERIAL NOT NULL UNIQUE ,
	titleFormation               VARCHAR (50) NOT NULL ,
	description                  TEXT NOT NULL ,
	publicationStatusFormation   VARCHAR (50) NOT NULL CHECK (Publication_Status__Formation IN ('Brouillon', 'Publié', 'Archivé')),
	isValidated                  BOOL NOT NULL DEFAULT FALSE,
	isPublic                     BOOL NOT NULL DEFAULT TRUE;
	instructorUuid               VARCHAR (36) NOT NULL ,
	CONSTRAINT Formations_PK PRIMARY KEY (formationId)

	,CONSTRAINT Formations_Instructors_FK FOREIGN KEY (instructorUuid) REFERENCES public.Instructors(instructorUuid)
);

CREATE INDEX idx_formationStatus ON public.Formations(publicationStatusFormation);
------------------------------------------------------------
-- Table: Module
------------------------------------------------------------
CREATE TABLE public.Modules(
	moduleId                  SERIAL NOT NULL UNIQUE ,
	titleModule               VARCHAR (50) NOT NULL ,
	contentModule             TEXT NOT NULL ,
	version                   VARCHAR (50) NOT NULL ,
	objectif                  TEXT NOT NULL ,
	publicationStatusModule   VARCHAR (50) NOT NULL CHECK (Publication_Status_Module IN ('Brouillon', 'Publié', 'Archivé')),
	isValidated               BOOL NOT NULL DEFAULT FALSE,
	instructorUuid            VARCHAR (36) NOT NULL  ,
	CONSTRAINT Modules_PK PRIMARY KEY (moduleId)

	,CONSTRAINT Modules_Instructors_FK FOREIGN KEY (instructorUuid) REFERENCES public.Instructors(instructorUuid)
);

------------------------------------------------------------
-- Table: Lesson
------------------------------------------------------------
CREATE TABLE public.Lessons(
	lessonId                  SERIAL NOT NULL UNIQUE ,
	titleLesson               VARCHAR (50) NOT NULL ,
	contentLesson             TEXT NOT NULL ,
	videoUrl                  TEXT NOT NULL ,
	imageUrl                  TEXT NOT NULL ,
	publicationStatusLesson   VARCHAR (50) NOT NULL CHECK (Publication_Status_Lesson IN ('Brouillon', 'Publié', 'Archivé')),
	instructorUuid            VARCHAR (36) NOT NULL  ,
	CONSTRAINT Lessons_PK PRIMARY KEY (lessonId)

	,CONSTRAINT Lessons_Instructors_FK FOREIGN KEY (instructorUuid) REFERENCES public.Instructors(instructorUuid)
);
------------------------------------------------------------
-- Table: Tag
------------------------------------------------------------
CREATE TABLE public.Tags(
	titleTagId   SERIAL NOT NULL UNIQUE ,
	CONSTRAINT Tags_PK PRIMARY KEY (titleTagId)
);

------------------------------------------------------------
-- Table: User_Formation_Registration
------------------------------------------------------------
CREATE TABLE public.UserFormationRegistration(
	formationId         INT  NOT NULL ,
	userUuid            VARCHAR (36) NOT NULL ,
	inscriptionDate     DATE ,
	isActive            BOOL NOT NULL DEFAULT TRUE,
	endDate             DATE  NOT NULL  ,
	CONSTRAINT UserFormationRegistration_PK PRIMARY KEY (formationId,userUuid)

	,CONSTRAINT UserFormationRegistration_Formations_FK FOREIGN KEY (formationId) REFERENCES public.Formations(formationId)
	,CONSTRAINT UserFormationRegistration_Users0_FK FOREIGN KEY (userUuid) REFERENCES public.Users(userUuid)
)

------------------------------------------------------------
-- Table: Module_Formation
------------------------------------------------------------
CREATE TABLE public.ModuleFormation(
	moduleId      INT  NOT NULL ,
	formationId   INT  NOT NULL  ,
	CONSTRAINT ModuleFormation_PK PRIMARY KEY (moduleId,formationId)

	,CONSTRAINT ModuleFormation_Modules_FK FOREIGN KEY (moduleId) REFERENCES public.Modules(moduleId)
	,CONSTRAINT ModuleFormation_Formations0_FK FOREIGN KEY (formationId) REFERENCES public.Formations(formationId)
);

------------------------------------------------------------
-- Table: Lesson_Module
------------------------------------------------------------
CREATE TABLE public.LessonModule(
	moduleId   INT  NOT NULL ,
	lessonId   INT  NOT NULL  ,
	CONSTRAINT LessonModule_PK PRIMARY KEY (moduleId,lessonId)

	,CONSTRAINT LessonModule_Modules_FK FOREIGN KEY (moduleId) REFERENCES public.Modules(moduleId)
	,CONSTRAINT LessonModule_Lessons0_FK FOREIGN KEY (lessonId) REFERENCES public.Lessons(lessonId)
);


------------------------------------------------------------
-- Table: User_Role
------------------------------------------------------------
CREATE TABLE public.UserRole(
	roleId     INT  NOT NULL ,
	userUuid   VARCHAR (36) NOT NULL  ,
	CONSTRAINT UserRole_PK PRIMARY KEY (roleId,userUuid)

	,CONSTRAINT UserRole_Roles_FK FOREIGN KEY (roleId) REFERENCES public.Roles(roleId)
	,CONSTRAINT UserRole_Users0_FK FOREIGN KEY (userUuid) REFERENCES public.Users(userUuid)
);

------------------------------------------------------------
-- Table: Lesson_Validation
------------------------------------------------------------
CREATE TABLE public.LessonValidation(
	lessonId       INT  NOT NULL ,
	userUuid       VARCHAR (36) NOT NULL ,
	validateDate   DATE  NOT NULL ,
	isCompleted    BOOL NOT NULL DEFAULT FALSE,
	CONSTRAINT LessonValidation_PK PRIMARY KEY (lessonId,userUuid)

	,CONSTRAINT LessonValidation_Lessons_FK FOREIGN KEY (lessonId) REFERENCES public.Lessons(lessonId)
	,CONSTRAINT LessonValidation_Users0_FK FOREIGN KEY (userUuid) REFERENCES public.Users(userUuid)
);

------------------------------------------------------------
-- Table: Publication_Status_Attribution
------------------------------------------------------------
CREATE TABLE public.PublicationStatusAttribution(
	formationId           INT  NOT NULL ,
	moduleId              INT  NOT NULL ,
	lessonId              INT  NOT NULL ,
	publicationStatusId   INT  NOT NULL  ,
	CONSTRAINT PublicationStatusAttribution_PK PRIMARY KEY (formationId,moduleId,lessonId,publicationStatusId)

	,CONSTRAINT PublicationStatusAttribution_Formations_FK FOREIGN KEY (formationId) REFERENCES public.Formations(formationId)
	,CONSTRAINT PublicationStatusAttribution_Modules0_FK FOREIGN KEY (moduleId) REFERENCES public.Modules(moduleId)
	,CONSTRAINT PublicationStatusAttribution_Lessons1_FK FOREIGN KEY (lessonId) REFERENCES public.Lessons(lessonId)
	,CONSTRAINT PublicationStatusAttribution_PublicationStatus2_FK FOREIGN KEY (publicationStatusId) REFERENCES public.PublicationStatus(publicationStatusId)
);

------------------------------------------------------------
-- Table: Formation_Tag
------------------------------------------------------------
CREATE TABLE public.FormationTag(
	titleTagId    INT  NOT NULL ,
	formationId   INT  NOT NULL  ,
	CONSTRAINT FormationTag_PK PRIMARY KEY (titleTagId,formationId)

	,CONSTRAINT FormationTag_Tags_FK FOREIGN KEY (titleTagId) REFERENCES public.Tags(titleTagId)
	,CONSTRAINT FormationTag_Formations0_FK FOREIGN KEY (formationId) REFERENCES public.Formations(formationId)
);
```

[🔝 Retour à la Table des matières](../../README.md#table-des-matieres)
