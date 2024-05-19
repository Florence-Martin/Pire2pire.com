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
-- Table: Role
------------------------------------------------------------
CREATE TABLE public.Role(
	ID_Role     SERIAL NOT NULL UNIQUE ,
	Name_Role   VARCHAR (50) NOT NULL UNIQUE ,
	CONSTRAINT Role_PK PRIMARY KEY (ID_Role)
);


------------------------------------------------------------
-- Table: Publication_Status
------------------------------------------------------------
CREATE TABLE public.Publication_Status(
	ID_Publication_Status     SERIAL NOT NULL UNIQUE ,
	Type_Publication_Status   VARCHAR (50) NOT NULL UNIQUE ,
	CONSTRAINT Publication_Status_PK PRIMARY KEY (ID_Publication_Status)
);


------------------------------------------------------------
-- Table: Address
------------------------------------------------------------
CREATE TABLE public.Address(
	ID_Address         SERIAL NOT NULL UNIQUE ,
	Address_Number     VARCHAR (50) NOT NULL ,
	Address_Street     VARCHAR (100) NOT NULL ,
	Address_Postcode   VARCHAR (20) NOT NULL ,
	Address_City       VARCHAR (50) NOT NULL ,
	Address_Country    VARCHAR (50) NOT NULL  ,
	CONSTRAINT Address_PK PRIMARY KEY (ID_Address)
);


------------------------------------------------------------
-- Table: User
------------------------------------------------------------
CREATE TABLE public.User(
	ID_User      UUID NOT NULL UNIQUE DEFAULT uuid_generate_v4(),
	Firstname    VARCHAR (50) NOT NULL ,
	Lastname     VARCHAR (50) NOT NULL ,
	Birthdate    DATE  NOT NULL ,
	Email        VARCHAR (50) NOT NULL UNIQUE ,
	Password     VARCHAR (50) NOT NULL ,
	User_Type    VARCHAR (50) NOT NULL ,
	ID_Address   INT  NOT NULL  ,
	CONSTRAINT User_PK PRIMARY KEY (ID_User)

	,CONSTRAINT User_Address_FK FOREIGN KEY (ID_Address) REFERENCES public.Address(ID_Address)
);

CREATE INDEX idx_user_email ON public.User(Email);
------------------------------------------------------------
-- Table: Instructor
------------------------------------------------------------
CREATE TABLE public.Instructor(
	ID_Instructor     UUID NOT NULL UNIQUE DEFAULT uuid_generate_v4(),
	Instructor_Code   VARCHAR (50) NOT NULL UNIQUE ,
	ID_User           UUID  NOT NULL UNIQUE ,
	CONSTRAINT Instructor_PK PRIMARY KEY (ID_Instructor)

	,CONSTRAINT Instructor_User_FK FOREIGN KEY (ID_User) REFERENCES public.User(ID_User)
	,CONSTRAINT Instructor_User_AK UNIQUE (ID_User)
);

CREATE INDEX idx_instructor_code ON public.Instructor(Instructor_Code);
------------------------------------------------------------
-- Table: Formation
------------------------------------------------------------
CREATE TABLE public.Formation(
	ID_Formation                   SERIAL NOT NULL UNIQUE ,
	Title_Formation                VARCHAR (50) NOT NULL ,
	Description                    TEXT NOT NULL,
	Publication_Status_Formation   VARCHAR(50) NOT NULL CHECK (Publication_Status__Formation IN ('Brouillon', 'Publié', 'Archivé')),
	IsValidated                    BOOL NOT NULL DEFAULT FALSE,
	ID_Instructor                  UUID  NOT NULL ,
	CONSTRAINT Formation_PK PRIMARY KEY (ID_Formation)

	,CONSTRAINT Formation_Instructor_FK FOREIGN KEY (ID_Instructor) REFERENCES public.Instructor(ID_Instructor)
);

CREATE INDEX idx_formation_status ON public.Formation(Publication_Status_Formation);
------------------------------------------------------------
-- Table: Module
------------------------------------------------------------
CREATE TABLE public.Module(
	ID_Module                   SERIAL NOT NULL UNIQUE ,
	Title_Module                VARCHAR (50) NOT NULL ,
	Content_Module              TEXT NOT NULL ,
	Version                     VARCHAR (50) NOT NULL ,
	Objectif                    TEXT NOT NULL ,
	Publication_Status_Module   VARCHAR(50) NOT NULL CHECK (Publication_Status_Module IN ('Brouillon', 'Publié', 'Archivé')),
	IsValidated                 BOOL NOT NULL DEFAULT FALSE,
	ID_Instructor               UUID  NOT NULL ,
	CONSTRAINT Module_PK PRIMARY KEY (ID_Module)

	,CONSTRAINT Module_Instructor_FK FOREIGN KEY (ID_Instructor) REFERENCES public.Instructor(ID_Instructor)
);


------------------------------------------------------------
-- Table: Lesson
------------------------------------------------------------
CREATE TABLE public.Lesson(
	ID_Lesson                   SERIAL NOT NULL UNIQUE ,
	Title_Lesson                VARCHAR (50) NOT NULL ,
	Content_Lesson              TEXT NOT NULL ,
	Video_URL                   TEXT NOT NULL ,
	Image_URL                   TEXT NOT NULL ,
	Publication_Status_Lesson   VARCHAR(50) NOT NULL CHECK (Publication_Status_Lesson IN ('Brouillon', 'Publié', 'Archivé')),
	ID_Instructor               UUID NOT NULL ,
	CONSTRAINT Lesson_PK PRIMARY KEY (ID_Lesson)

	,CONSTRAINT Lesson_Instructor_FK FOREIGN KEY (ID_Instructor) REFERENCES public.Instructor(ID_Instructor)
);


------------------------------------------------------------
-- Table: Tag
------------------------------------------------------------
CREATE TABLE public.Tag(
	ID_Title_Tag   SERIAL NOT NULL UNIQUE ,
	CONSTRAINT Tag_PK PRIMARY KEY (ID_Title_Tag)
);


------------------------------------------------------------
-- Table: User_Formation_Registration
------------------------------------------------------------
CREATE TABLE public.User_Formation_Registration(
	ID_Formation       INT  NOT NULL ,
	ID_User            UUID NOT NULL ,
	Inscription_Date   DATE ,
	Is_Active          BOOL NOT NULL DEFAULT TRUE,
	End_Date           DATE ,
	CONSTRAINT User_Formation_Registration_PK PRIMARY KEY (ID_Formation,ID_User)

	,CONSTRAINT User_Formation_Registration_Formation_FK FOREIGN KEY (ID_Formation) REFERENCES public.Formation(ID_Formation)
	,CONSTRAINT User_Formation_Registration_User0_FK FOREIGN KEY (ID_User) REFERENCES public.User(ID_User)
);


------------------------------------------------------------
-- Table: Module_Formation
------------------------------------------------------------
CREATE TABLE public.Module_Formation(
	ID_Module      INT  NOT NULL ,
	ID_Formation   INT  NOT NULL ,
	CONSTRAINT Module_Formation_PK PRIMARY KEY (ID_Module,ID_Formation)

	,CONSTRAINT Module_Formation_Module_FK FOREIGN KEY (ID_Module) REFERENCES public.Module(ID_Module)
	,CONSTRAINT Module_Formation_Formation0_FK FOREIGN KEY (ID_Formation) REFERENCES public.Formation(ID_Formation)
);


------------------------------------------------------------
-- Table: Lesson_Module
------------------------------------------------------------
CREATE TABLE public.Lesson_Module(
	ID_Module   INT  NOT NULL ,
	ID_Lesson   INT  NOT NULL ,
	CONSTRAINT Lesson_Module_PK PRIMARY KEY (ID_Module,ID_Lesson)

	,CONSTRAINT Lesson_Module_Module_FK FOREIGN KEY (ID_Module) REFERENCES public.Module(ID_Module)
	,CONSTRAINT Lesson_Module_Lesson0_FK FOREIGN KEY (ID_Lesson) REFERENCES public.Lesson(ID_Lesson)
);


------------------------------------------------------------
-- Table: User_Role
------------------------------------------------------------
CREATE TABLE public.User_Role(
	ID_Role   INT  NOT NULL ,
	ID_User   UUID NOT NULL ,
	CONSTRAINT User_Role_PK PRIMARY KEY (ID_Role,ID_User)

	,CONSTRAINT User_Role_Role_FK FOREIGN KEY (ID_Role) REFERENCES public.Role(ID_Role)
	,CONSTRAINT User_Role_User0_FK FOREIGN KEY (ID_User) REFERENCES public.User(ID_User)
);


------------------------------------------------------------
-- Table: Lesson_Validation
------------------------------------------------------------
CREATE TABLE public.Lesson_Validation(
	ID_Lesson       INT  NOT NULL ,
	ID_User         UUID NOT NULL ,
	Validate_Date   DATE  NOT NULL ,
	IsCompleted     BOOL NOT NULL DEFAULT FALSE,
	CONSTRAINT Lesson_Validation_PK PRIMARY KEY (ID_Lesson,ID_User)

	,CONSTRAINT Lesson_Validation_Lesson_FK FOREIGN KEY (ID_Lesson) REFERENCES public.Lesson(ID_Lesson)
	,CONSTRAINT Lesson_Validation_User0_FK FOREIGN KEY (ID_User) REFERENCES public.User(ID_User)
);


------------------------------------------------------------
-- Table: Publication_Status_Attribution
------------------------------------------------------------
CREATE TABLE public.Publication_Status_Attribution(
	ID_Formation            INT  NOT NULL ,
	ID_Module               INT  NOT NULL ,
	ID_Lesson               INT  NOT NULL ,
	ID_Publication_Status   INT  NOT NULL ,
	CONSTRAINT Publication_Status_Attribution_PK PRIMARY KEY (ID_Formation,ID_Module,ID_Lesson,ID_Publication_Status)

	,CONSTRAINT Publication_Status_Attribution_Formation_FK FOREIGN KEY (ID_Formation) REFERENCES public.Formation(ID_Formation)
	,CONSTRAINT Publication_Status_Attribution_Module0_FK FOREIGN KEY (ID_Module) REFERENCES public.Module(ID_Module)
	,CONSTRAINT Publication_Status_Attribution_Lesson1_FK FOREIGN KEY (ID_Lesson) REFERENCES public.Lesson(ID_Lesson)
	,CONSTRAINT Publication_Status_Attribution_Publication_Status2_FK FOREIGN KEY (ID_Publication_Status) REFERENCES public.Publication_Status(ID_Publication_Status)
);


------------------------------------------------------------
-- Table: Formation_Tag
------------------------------------------------------------
CREATE TABLE public.Formation_Tag(
	ID_Title_Tag   INT  NOT NULL ,
	ID_Formation   INT  NOT NULL ,
	CONSTRAINT Formation_Tag_PK PRIMARY KEY (ID_Title_Tag,ID_Formation)

	,CONSTRAINT Formation_Tag_Tag_FK FOREIGN KEY (ID_Title_Tag) REFERENCES public.Tag(ID_Title_Tag)
	,CONSTRAINT Formation_Tag_Formation0_FK FOREIGN KEY (ID_Formation) REFERENCES public.Formation(ID_Formation)
);

```

[🔝 Retour à la Table des matières](../../README.md#table-des-matieres)
