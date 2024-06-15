# Diagramme de séquence - Authentification basée sur OAuth

Ce diagramme illustre l’emploi du protocole d’autorisation **OAuth** pour renforcer la sécurité de l’accès aux ressources de notre application. Les redirections HTTPS, ainsi que l’échange de codes d’autorisation et de jetons, font partis des processus **OAuth**.

![Représentation UML-Diagramme de séquence - authentification](../Assets/Images/AuthentificationSequenceDiagram.png)

<details>
<summary>Version textualisée de ce diagramme</summary>

### Participants

- **Utilisateur** : La personne qui souhaite accéder à l'application.
- **Navigateur Web** : Le programme utilisé par l'utilisateur pour interagir avec l'application.
- **Application** : Le logiciel que l'utilisateur cherche à utiliser.
- **Serveur d'Autorisation** : Le système qui vérifie si l'utilisateur a le droit d'accéder à certaines parties de l'application et qui accorde ces accès.
- **Serveur de Contenu** : Le système qui stocke les informations auxquelles l'utilisateur essaie d'accéder.

### Flux du Processus

1. **Point de départ** : Là où l'utilisateur commence son action.
2. **Demander des ressources** : L'utilisateur demande, via son navigateur, à accéder aux contenus de l'application.
3. **Demande d'accès à l'application** : Le navigateur envoie une demande pour accéder à l'application.
4. **Redirection sécurisée** : L'application redirige le navigateur vers le serveur qui gère les autorisations.
5. **Autorisation** : Le serveur qui gère les autorisations reçoit la demande.
6. **Formulaire de permission** : Ce serveur envoie un formulaire pour demander la permission de l'utilisateur.
7. **Affichage du formulaire** : Le formulaire est montré à l'utilisateur.
8. **Donner la permission** : L'utilisateur donne son accord via le formulaire.

### Gestion des Alternatives

- **Traitement de la permission** :

  - **Si l'accord est donné, le processus continue**

    9. **Traitement de la permission** : Le serveur traite l'accord donné par l'utilisateur.
    10. **Redirection sécurisée** : Le navigateur est redirigé vers l'application avec un code spécial d'autorisation.
    11. **Code d'autorisation de l'application** : L'application reçoit ce code.
    12. **Envoi du code d'autorisation au serveur** : L'application envoie ce code au serveur d'autorisation.
    13. **Jeton d'accès** : Le serveur envoie un jeton qui permet d'accéder aux informations protégées.
    14. **Accès aux informations protégées** : L'application utilise ce jeton pour demander l'accès aux informations protégées stockées sur le serveur de contenu.
    15. **Ressources protégées de l'utilisateur** : Le serveur de contenu envoie les informations protégées à l'application.
    16. **Livraison des informations protégées** : Les informations sont fournies à l'utilisateur.
    17. **Ressources de l'utilisateur protégées et délivrées** : Les ressources protégées sont finalement rendues accessibles à l'utilisateur.

  - **Si l'accord n'est pas donné, le processus échoue** :

    18. **Aucune permission accordée** : L'accès n'est pas autorisé.
    19. **Ressource non disponible** : L'application indique que la ressource demandée n'est pas accessible.
    20. **Affichage de la ressource non disponible** : Le navigateur affiche un message indiquant que la ressource n'est pas accessible.

21. **Fin du processus** : Le processus se termine, que l'utilisateur ait ou non obtenu l'accès.
</details>