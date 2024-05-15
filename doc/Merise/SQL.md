# Script SQL

Inclure une section pour le script SQL de la base de données. Expliquer comment ce script permet de créer les tables, les relations, et les contraintes définies dans les sections précédentes.

```sql
------------------------------------------------------------
--        Script Postgre
------------------------------------------------------------



------------------------------------------------------------
-- Table: Role
------------------------------------------------------------
CREATE TABLE public.Role(
	ID_Role     SERIAL NOT NULL ,
	Name_Role   VARCHAR (50) NOT NULL  ,
	CONSTRAINT Role_PK PRIMARY KEY (ID_Role)
) ;


------------------------------------------------------------
-- Table: Formation
------------------------------------------------------------
CREATE TABLE public.Formation(
	ID_Formation       SERIAL NOT NULL ,
	Title_Formation    VARCHAR (50) NOT NULL ,
	Description        VARCHAR (2000)  NOT NULL ,
	Status_Formation   VARCHAR (50) NOT NULL ,
	IsValidated        BOOL  NOT NULL  ,
	CONSTRAINT Formation_PK PRIMARY KEY (ID_Formation)
) ;


------------------------------------------------------------
-- Table: Module
------------------------------------------------------------
CREATE TABLE public.Module(
	ID_Module        SERIAL NOT NULL ,
	Title_Module     VARCHAR (50) NOT NULL ,
	Content_Module   VARCHAR (2000)  NOT NULL ,
	Version          VARCHAR (50) NOT NULL ,
	Objectif         VARCHAR (2000)  NOT NULL ,
	Status_Module    VARCHAR (50) NOT NULL ,
	IsValidated      BOOL  NOT NULL  ,
	CONSTRAINT Module_PK PRIMARY KEY (ID_Module)
) ;


------------------------------------------------------------
-- Table: Status
------------------------------------------------------------
CREATE TABLE public.Status(
	ID_Status     SERIAL NOT NULL ,
	Type_Status   VARCHAR (50) NOT NULL  ,
	CONSTRAINT Status_PK PRIMARY KEY (ID_Status)
) ;


------------------------------------------------------------
-- Table: Address
------------------------------------------------------------
CREATE TABLE public.Address(
	ID_Address         SERIAL NOT NULL ,
	Address_Number     VARCHAR (50) NOT NULL ,
	Address_Street     VARCHAR (100) NOT NULL ,
	Address_Postcode   VARCHAR (20) NOT NULL ,
	Address_City       VARCHAR (50) NOT NULL  ,
	CONSTRAINT Address_PK PRIMARY KEY (ID_Address)
) ;


------------------------------------------------------------
-- Table: User
------------------------------------------------------------
CREATE TABLE public.User(
	ID_User      SERIAL NOT NULL ,
	Firstname    VARCHAR (50) NOT NULL ,
	Lastname     VARCHAR (50) NOT NULL ,
	Birthdate    DATE  NOT NULL ,
	Email        VARCHAR (50) NOT NULL ,
	Password     VARCHAR (50) NOT NULL ,
	User_Type    VARCHAR (50) NOT NULL ,
	ID_Address   INT  NOT NULL  ,
	CONSTRAINT User_PK PRIMARY KEY (ID_User)

	,CONSTRAINT User_Address_FK FOREIGN KEY (ID_Address) REFERENCES public.Address(ID_Address)
) ;


------------------------------------------------------------
-- Table: Instructor
------------------------------------------------------------
CREATE TABLE public.Instructor(
	ID_Instructor     SERIAL NOT NULL ,
	Instructor_Code   VARCHAR (50) NOT NULL ,
	ID_User           INT  NOT NULL  ,
	CONSTRAINT Instructor_PK PRIMARY KEY (ID_Instructor)

	,CONSTRAINT Instructor_User_FK FOREIGN KEY (ID_User) REFERENCES public.User(ID_User)
	,CONSTRAINT Instructor_User_AK UNIQUE (ID_User)
) ;


------------------------------------------------------------
-- Table: Lesson
------------------------------------------------------------
CREATE TABLE public.Lesson(
	ID_Lesson        SERIAL NOT NULL ,
	Title_Lesson     VARCHAR (50) NOT NULL ,
	Content_Lesson   VARCHAR (2000)  NOT NULL ,
	Video            VARCHAR (2000)  NOT NULL ,
	Image            VARCHAR (2000)  NOT NULL ,
	Tag              VARCHAR (50) NOT NULL ,
	Status_Lesson    VARCHAR (50) NOT NULL ,
	ID_Module        INT  NOT NULL ,
	ID_Instructor    INT  NOT NULL  ,
	CONSTRAINT Lesson_PK PRIMARY KEY (ID_Lesson)

	,CONSTRAINT Lesson_Module_FK FOREIGN KEY (ID_Module) REFERENCES public.Module(ID_Module)
	,CONSTRAINT Lesson_Instructor0_FK FOREIGN KEY (ID_Instructor) REFERENCES public.Instructor(ID_Instructor)
) ;


------------------------------------------------------------
-- Table: Register
------------------------------------------------------------
CREATE TABLE public.Register(
	ID_Formation      INT  NOT NULL ,
	ID_User           INT  NOT NULL ,
	Inscrition_Date   DATE  NOT NULL ,
	Is_Active         BOOL  NOT NULL ,
	End_Date          DATE  NOT NULL  ,
	CONSTRAINT Register_PK PRIMARY KEY (ID_Formation,ID_User)

	,CONSTRAINT Register_Formation_FK FOREIGN KEY (ID_Formation) REFERENCES public.Formation(ID_Formation)
	,CONSTRAINT Register_User0_FK FOREIGN KEY (ID_User) REFERENCES public.User(ID_User)
) ;


------------------------------------------------------------
-- Table: Compose
------------------------------------------------------------
CREATE TABLE public.Compose(
	ID_Module      INT  NOT NULL ,
	ID_Formation   INT  NOT NULL  ,
	CONSTRAINT Compose_PK PRIMARY KEY (ID_Module,ID_Formation)

	,CONSTRAINT Compose_Module_FK FOREIGN KEY (ID_Module) REFERENCES public.Module(ID_Module)
	,CONSTRAINT Compose_Formation0_FK FOREIGN KEY (ID_Formation) REFERENCES public.Formation(ID_Formation)
) ;


------------------------------------------------------------
-- Table: Have
------------------------------------------------------------
CREATE TABLE public.Have(
	ID_Role   INT  NOT NULL ,
	ID_User   INT  NOT NULL  ,
	CONSTRAINT Have_PK PRIMARY KEY (ID_Role,ID_User)

	,CONSTRAINT Have_Role_FK FOREIGN KEY (ID_Role) REFERENCES public.Role(ID_Role)
	,CONSTRAINT Have_User0_FK FOREIGN KEY (ID_User) REFERENCES public.User(ID_User)
) ;


------------------------------------------------------------
-- Table: Validate
------------------------------------------------------------
CREATE TABLE public.Validate(
	ID_Lesson       INT  NOT NULL ,
	ID_User         INT  NOT NULL ,
	Validate_Date   DATE  NOT NULL ,
	IsCompleted     BOOL  NOT NULL  ,
	CONSTRAINT Validate_PK PRIMARY KEY (ID_Lesson,ID_User)

	,CONSTRAINT Validate_Lesson_FK FOREIGN KEY (ID_Lesson) REFERENCES public.Lesson(ID_Lesson)
	,CONSTRAINT Validate_User0_FK FOREIGN KEY (ID_User) REFERENCES public.User(ID_User)
) ;


------------------------------------------------------------
-- Table: Give
------------------------------------------------------------
CREATE TABLE public.Give(
	ID_Formation   INT  NOT NULL ,
	ID_Module      INT  NOT NULL ,
	ID_Lesson      INT  NOT NULL ,
	ID_Status      INT  NOT NULL  ,
	CONSTRAINT Give_PK PRIMARY KEY (ID_Formation,ID_Module,ID_Lesson,ID_Status)

	,CONSTRAINT Give_Formation_FK FOREIGN KEY (ID_Formation) REFERENCES public.Formation(ID_Formation)
	,CONSTRAINT Give_Module0_FK FOREIGN KEY (ID_Module) REFERENCES public.Module(ID_Module)
	,CONSTRAINT Give_Lesson1_FK FOREIGN KEY (ID_Lesson) REFERENCES public.Lesson(ID_Lesson)
	,CONSTRAINT Give_Status2_FK FOREIGN KEY (ID_Status) REFERENCES public.Status(ID_Status)
);

```

[🔝 Retour à la Table des matières](../../README.md#table-des-matieres)
