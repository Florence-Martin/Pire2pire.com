# Diagramme de séquence - Authentification basée sur OAuth

Ce diagramme illustre l’emploi du protocole d’autorisation **OAuth** pour renforcer la sécurité de l’accès aux ressources de notre application. Les redirections HTTPS, ainsi que l’échange de codes d’autorisation et de jetons, font partis des processus **OAuth**.

![Représentation UML-Diagramme de séquence - authentification](../../Assets/Images/userAuthentification.png)

<details>
<summary>Version textualisée de ce diagramme</summary>

- 1. User à WebBrowser:
  - • Action: get application resources
  - • L’utilisateur demande à se connecter à l’application.
- 2. WebBrowser à Application:
  - • Action: request application access
  - • Le navigateur web demande l’accès à l’application.
- 3. Application à WebBrowser:
  - • Action: <<https redirect>>
  - • L’application redirige le navigateur web via HTTPS.
- 4. WebBrowser à ApplicationAuthorizationServer:
  - • Action: get authorization
  - • Le navigateur web demande l’autorisation au serveur d’autorisation de l’application.
- 5. ApplicationAuthorizationServer à Application:
  - • Action: request permission form
  - • Le serveur d’autorisation de l’application demande le formulaire de permission.
- 6. Application à WebBrowser:
  - • Action: request permission form
  - • L’application envoie la demande de formulaire de permission au navigateur web.
- 7. User à WebBrowser:
  - • Action: fill permission form
  - • L’utilisateur remplit le formulaire de permission.
- 8. WebBrowser à ApplicationAuthorizationServer:
  - • Action: process permission
  - • Le navigateur web envoie le formulaire rempli au serveur d’autorisation de l’application pour traitement.
- 9. ApplicationAuthorizationServer à WebBrowser:
  - • Action: <<https redirect>>
  - • Le serveur d’autorisation de l’application redirige le navigateur web via HTTPS.
- 10. WebBrowser à Application:
  - • Action: get authorization code
  - • Le navigateur web obtient un code d’autorisation.
- 11. Application à ApplicationAuthorizationServer:
  - • Action: get token
  - • L’application demande un jeton au serveur d’autorisation de l’application.
- 12. ApplicationAuthorizationServer à Application:
  - • Action: access token
  - • Le serveur d’autorisation de l’application fournit un jeton d’accès.
- 13. Application à ApplicationContentServer:
  - • Action: get the content of the application
  - • L’application demande le contenu de l’application au serveur de contenu de l’application.
- 14. ApplicationContentServer à Application:
  - • Action: return content of the application
  - • Le serveur de contenu de l’application renvoie le contenu demandé à l’application.
- 15. Application à WebBrowser:
  - • Action: display content of the application
  - • L’application envoie le contenu de l’application au navigateur web pour affichage.
- 16. WebBrowser à User:
  - • Action: read content of the application
  - • L’utilisateur peut lire le contenu de l’application affiché par le navigateur web.
  - • Alt [permission granted]: Si la permission est accordée, l’utilisateur peut lire le contenu de l’application.
- 17. ApplicationAuthorizationServer à Application:
  - • Action: no access token
  - • Si la permission n’est pas accordée, le serveur d’autorisation de l’application n’envoie pas de jeton d’accès.
- 18. Application à WebBrowser:
  - • Action: application resource not available
  - • L’application informe le navigateur web que les ressources de l’application ne sont pas disponibles.
- 19. WebBrowser à User:
  - • Action: application resource not available
  - • Le navigateur web informe l’utilisateur que les ressources de l’application ne sont pas disponibles.
  - • Alt [no permission]: Si la permission n’est pas accordée, l’utilisateur est informé que les ressources de l’application ne sont pas disponibles.
  </details>
