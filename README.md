# Pire2pire.com

Conception de la base de données d’une plateforme de formation en ligne nommée pire2pire.com à l'aide de la méthode MERISE.

# Table des matières

1. [Introduction](#introduction)
2. [Acronyme MERISE](#acronyme-merise)
3. [Dictionnaire de données](#dictionnaire-de-donnees)
4. [Règles de gestion](#regles-de-gestion)
5. [MCD (Modèle Conceptuel des Données)](#mcd-modele-conceptuel-des-donnees)
6. [MLD (Modèle Logique des Données)](#mld-modele-logique-des-donnees)
7. [MPD (Modèle Physique des Données)](#mpd-modele-physique-des-donnees)
8. [Script SQL](#script-sql)
9. [Instructions d'installation](#instructions-dinstallation)
10. [Conclusion](#conclusion)

## Introduction du brief - Contexte du projet

Les formations sont organisés en modules.

Chaque module est caractérisé par un numéro de module sous forme de Semantic Versionning, un intitulé, un objectif pédagogique, un contenu (textes, images et vidéos), une durée en heures (facultatif), un ou plusieurs tags et un auteur.

Un module peut faire partie d'une ou plusieurs formations, comme par exemple un pire module "Commandes de base Git" pourrait faire partie d'une pire formation "Frontend Javascript" et "DevOps", voir plus.

Un module peut contenir un texte et/ou une image et/ou une vidéo.

Les apprenants peuvent s'inscrire à une ou plusieurs formations, ils peuvent choisir de ne pas suivre certains des modules s'ils possèdent déjà, par exemple, les compétences. Autrement dit, ils peuvent arbitrairement valider les modules de leur choix en un clic.

Chaque apprenant est évalué pour chaque module et possède un état de fin de module (OK / KO).

Une formation est considérée comme terminée lorsque tous les modules ont été validés.

Chaque apprenant est caractérisé par un numéro d’inscription unique, un nom, un prénom, une adresse et une date de naissance.

Un formateurs est auteur d'un module pour une formation donnée, chaque formateur est caractérisé par un code, un nom, un prénom.

## Acronyme MERISE

Ajouter une section dédiée à la définition de l'acronyme MERISE. Expliquer brièvement cette méthodologie de modélisation des données et son rôle dans le projet.

## Dictionnaire de données

Incluer une section décrivant le dictionnaire de données. Expliquer sa fonction en listant les entités clés, leurs attributs, et les relations entre elles, offrant ainsi une vision détaillée de la structure des données.

## Règles de gestion

Détailler les règles de gestion pour la plateforme, en clarifiant les relations entre les modules, les formations, les apprenants, et les formateurs. Mentionner les mécanismes d'évaluation, les conditions pour valider une formation, et les règles de création de modules.

## MCD (Modèle Conceptuel des Données)

Fournir une description du MCD, expliquant la représentation conceptuelle des entités, leurs attributs, et les relations entre elles.

## MLD (Modèle Logique des Données)

Ajouter une section pour le MLD, montrant la transformation du MCD en une structure plus détaillée. Cela inclut les types de données, les contraintes, et les relations logiques.

## MPD (Modèle Physique des Données)

Présenter ensuite le MPD, qui illustre la structure physique de la base de données, y compris les tables, les colonnes, et les index éventuels.

## Script SQL

Inclure une section pour le script SQL de la base de données. Expliquer comment ce script permet de créer les tables, les relations, et les contraintes définies dans les sections précédentes.

## Instructions d'installation

Fournir des instructions claires sur la manière de cloner le dépôt GitHub, et comment exécuter le script SQL pour configurer la base de données.

## Conclusion

Terminer par une conclusion récapitulative, soulignant la cohérence de l'ensemble et les prochaines étapes potentielles.
