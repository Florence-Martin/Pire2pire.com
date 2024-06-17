# Diagramme de séquence - Inscription à une formation

Ce diagramme décrit les interactions détaillées entre l’utilisateur, l’interface web, le contrôleur et la base de données pour le processus d’inscription à un cours de formation.

![Représentation UML-Diagramme de séquence - inscription](../../Assets/Images/registrationCourse.png)

<details>
<summary>Version textualisée de ce diagramme</summary>
	
- 1.	User:
	- •	Action: login()
	- •	Suit les étapes pour se connecter au système.
- 2.	User à WebInterface:
	- •	Action: request for list of training courses
	- •	L’utilisateur demande la liste des cours de formation disponibles.
- 3.	WebInterface à Controller:
	- •	Action: get list of training courses
	- •	L’interface web demande au contrôleur la liste des cours de formation.
- 4.	Controller à Database:
	- •	Action: get list of training courses
	- •	Le contrôleur demande à la base de données la liste des cours de formation.
- 5.	Database à Controller:
	- •	Action: return list of training courses
	- •	La base de données retourne la liste des cours de formation au contrôleur.
- 6.	Controller à WebInterface:
	- •	Action: display list of training courses
	- •	Le contrôleur envoie la liste des cours de formation à l’interface web pour affichage.
- 7.	User à WebInterface:
	- •	Action: choose a course
	- •	L’utilisateur choisit un cours dans la liste affichée.
- 8.	User à WebInterface:
	- •	Action: select a course
	- •	L’utilisateur sélectionne un cours spécifique.
- 9.	WebInterface à Controller:
	- •	Action: check available course
	- •	L’interface web vérifie auprès du contrôleur la disponibilité du cours sélectionné.
- 10.	Controller à Database:
	- •	Action: check available course
	- •	Le contrôleur demande à la base de données de vérifier la disponibilité du cours.
- 11.	Database à Controller:
	- •	Action: return available course
	- •	La base de données retourne l’information sur la disponibilité du cours au contrôleur.
- 12.	Controller à WebInterface:
	- •	Action: display available course
	- •	Le contrôleur envoie l’information de disponibilité du cours à l’interface web pour affichage.
- 13.	User à WebInterface:
	- •	Action: registration to be confirmed
	- •	La WebInterface indique que l’inscription doit être confirmée.
- 14.	User à WebInterface:
	- •	Action: confirm registration
	- •	L’utilisateur confirme l’inscription au cours.
- 15.	WebInterface à Controller:
	- •	Action: post to database
	- •	L’interface web envoie la demande d’inscription au contrôleur pour l’enregistrer dans la base de données.
- 16.	Controller à Database:
	- •	Action: post to database
	- •	Le contrôleur envoie la demande d’inscription à la base de données.
- 17.	Database à Controller:
	- •	Action: validate inscription
	- •	La base de données valide l’inscription.
- 18.	Controller à WebInterface:
	- •	Action: validate inscription
	- •	Le contrôleur informe l’interface web que l’inscription a été validée.
- 19.	WebInterface à User:
	- •	Action: confirm registration by message
	- •	L’interface web informe l’utilisateur que l’inscription a été confirmée par message.
	- •	Alt [Success]: Si l’inscription est réussie, l’utilisateur reçoit un message de confirmation.
	- •	Alt [Failed]: Si l’inscription échoue, l’utilisateur reçoit un message de refus.
- 20.	Controller à Database:
	- •	Action: reject the request for registration
	- •	En cas d’échec, le contrôleur envoie une demande de rejet d’inscription à la base de données.
- 21.	WebInterface à User:
	- •	Action: refuse registration by message
	- •	L’interface web informe l’utilisateur que l’inscription a été refusée par message.
</details>

[🔝 Retour à la Table des matières](../../../README.md#table-des-matieres)
