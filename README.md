# Pire2pire.com

La conception de la base de données pour la plateforme de formation en ligne **pire2pire.com** est réalisée en utilisant la méthode MERISE et les diagrammes UML (Unified Modeling Language).  
Ce processus est mené en collaboration étroite avec le client pour garantir que chaque étape de la conception soit validée conjointement par nos équipes et notre client.

# Structure du dépôt

## [Table des matières](#table-des-matieres)

### 1. Introduction et Contexte

#### [1.1 Introduction](./doc/Client/Context.md)

#### [1.2 Acronyme MERISE](./doc/Merise/Merise-acronym.md)

#### [1.3 Dictionnaire de données](./doc/Dictionary.md)

#### [1.4 Règles de gestion](./doc/Gestion-rules.md)

### 2. Modélisation des Données avec Merise

#### [2.1 MCD (Modèle Conceptuel des Données)](./doc/Merise/MCD.md)

#### [2.2 MLD (Modèle Logique des Données)](./doc/Merise/MLD.md)

#### [2.3 Script SQL](./doc/Merise/SQL.md)

### 3. Modélisation UML

#### [3.1 UML-Use Case](./doc/UML/Use-Case/Use-case.md)

#### [3.2 UML-Diagramme d'activité - inscription à une formation](./doc/UML/Activity-Diagram/Course-registration.md)

#### [3.3 UML-Diagramme d'activité - gestion des formations](./doc/UML/Activity-Diagram/Training-management.md)

#### [3.4 UML-Diagramme de séquence - inscription à une formation](./doc/UML/Sequence-Diagram/Registration-sequence-diagram.md)

#### [3.5 UML-Diagramme de séquence - authentification](./doc/UML/Sequence-Diagram/UserAuthentification-sequence-diagram.md)

#### [3.6 UML-Diagramme de classe - inscription à une formation](./doc/UML/Class-Diagram/Class-Diagram.md)

### 4. Installation et Contribution

#### [4.1 Instructions d'installation](#instructions-dinstallation)

#### [4.2 Contribution](#contribution)

### 5. Conclusion

#### [5.1 Conclusion](./doc/Conclusion.md)

---

---

---

## Instructions d'installation

#### Configurer la base de données

Pour configurer la base de données et visualiser sa structure :

1. **Installer PostgreSQL** : Assurez-vous d'avoir PostgreSQL installé et que le serveur est en cours d'exécution.

2. **Exécuter le script SQL** : Dans le répertoire du projet, exécutez le script setup.sql pour initialiser la base de données :

```
psql -U [nom_utilisateur] -d [nom_base_de_donnees] -f setup.sql
```

Assurez-vous de remplacer [nom_utilisateur] et [nom_base_de_donnees] par les valeurs appropriées pour votre configuration.

3. **Visualiser la base de données** : Vous pouvez ensuite visualiser la structure de la base de données en utilisant des outils tels que pgAdmin ou en accédant directement à PostgreSQL :

```
psql -U [nom_utilisateur] -d [nom_base_de_donnees]
```

Cela vous permettra d'explorer les tables et les données de la base de données directement.

## Contribution

Si vous souhaitez contribuer à ce projet :

1. Fork ce dépôt.
2. Créez une branche pour votre contribution :

```
git checkout -b feature/ma-contribution
```

3. Apportez vos modifications aux documents Markdown ou au script SQL.
4. Soumettez une Pull Request pour intégrer vos changements dans le dépôt principal.
