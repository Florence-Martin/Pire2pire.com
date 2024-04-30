# Pire2pire.com

Conception de la base de données d’une plateforme de formation en ligne nommée pire2pire.com à l'aide de la méthode MERISE.

# Structure du dépôt

## Table des matières

1. [Introduction](./doc/Client/Context.md)
2. [Acronyme MERISE](./doc/Merise/Merise-acronym.md)
3. [Dictionnaire de données](./doc/Merise/Dictionary.md)
4. [Règles de gestion](./doc/Gestion-rules.md)
5. [MCD (Modèle Conceptuel des Données)](./doc/Merise/MCD.md)
6. [MLD (Modèle Logique des Données)](./doc/Merise/MLD.md)
7. [MPD (Modèle Physique des Données)](./doc/Merise/MPD.md)
8. [Script SQL](./doc/Merise/SQL.md)
9. [Instructions d'installation](#instructions-dinstallation)
10. [Conclusion](#conclusion)

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

#### Contribution

Si vous souhaitez contribuer à ce projet :

1. Fork ce dépôt.
2. Créez une branche pour votre contribution :

```
git checkout -b feature/ma-contribution
```

3. Apportez vos modifications aux documents Markdown ou au script SQL.
4. Soumettez une Pull Request pour intégrer vos changements dans le dépôt principal.

## Conclusion

Terminer par une conclusion récapitulative, soulignant la cohérence de l'ensemble et les prochaines étapes potentielles.
