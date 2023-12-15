# Projet d'intégration Kairios

## Présentation
Vous trouverez dans ce dépôt le code source concernant une application Symfony et Vue qui viendra décrire une interface Web simpliste détaillant deux entités à savoir le `Dépot` et la `Reponse`.

## Installation
Le projet est configuré pour fonctionner sous un environnement Docker. Il suffit donc de lancer les commandes suivantes pour lancer les containers :
```bash
docker-compose up -d
```

Connectez vous ensuite au container de l'application et installer les `node_modules`. Une fois cette opération faite il vous reste plus qu'a compiler
le front de l'application (en mode dev ou prod selon vos besoins).

L'application sera donc accessible à l'adresse suivante : [http://localhost](http://localhost)

## Lancement des tests unitaires
Pour lancer les tests unitaires, il suffit de lancer la commande suivante :
```bash
docker-compose exec application composer atoum
```

## Lancement des tests d'intégration
Le lancement des tests d'intégration nécessite l'environnement de test. Afin de les lancer, 
vous devez modifier le fichier `docker-compose.yml` comme suit : \
```yml
    environment:
      APP_ENV: test
```

Rebuildez ensuite le container :
```bash
docker-compose up -d --build application
```

Enfin, pour lancer les tests intégration, il suffit de lancer la commande suivante :
```bash
docker-compose exec application composer phpunit
```

## Lancement de la suite de tests intégrale
La suite de test intégrale lance `phpCbf` et `phpCs` afin de valider le code style, puis les tests unitaire et d'intégration.
> /!\ La suite de tests Unitaire **vide la base de donnée de test et le cache**. /!\
> Le lancement de la suite de test nécessite l'environnement de test (CF **lancement des tests d'intégration**)
```bash
docker-compose exec application composer test-and-verif
```

## Se connecter en bash au container
Pour se connecter en bash au container, il suffit de lancer la commande suivante :
```bash
docker-compose exec application bash
```

## Lancer le mode watch pour le front
Pour lancer le mode watch pour le front, il suffit de lancer la commande suivante :
```bash
docker-compose exec application npm run watch
```

## Convention de commit
Le projet exige une norme de commit afin de faciliter la lecture de ces derniers. Il vient respecter le format suivant :

`<type>(<scope>): <subject>`
`<BLANK LINE>`
`<body>`

Par exemple :
```
feat(README): Ajout d'une section sur les tests unitaires

Ajout d'une section sur les tests unitaires dans le README
```

```
fix(demande clinique): Correction d'un bug sur la création d'une demande clinique

Un bug était présent sur la création d'une demande clinique. Il concernait la prise en compte du paramètre optionnel comme étant requis.
```
