---
title: "Guide"
date: 2022-07-15T11:12:06-04:00
draft: false
---

## Table des matières
1. [Comment ça marche?](#comment-ça-marche)
	1. [Prérequis](#prérequis)
	2. [Créer son bot](#créer-son-bot)
	3. [Les plugins](#les-plugins)

## Comment ça marche?

### Prérequis
- Node.js et NPM (nous recommandons la dernière version LTS)
- Un éditeur de code (Visual Studio Code ou un autre)
- Un peu de connaissances en développement JavaScript ou TypeScript
- Oui, juste ça

### Créer son bot
Créez un nouveau projet Node.js et NPM:
```bash
npm init
```

Installez le core du Artibot:
```bash
npm i artibot
```

Nous vous recommandons aussi nodemon pour faciliter le développement de votre bot:
```bash
npm i nodemon --save-dev
```

Mettez votre projet en mode ESM (au lieu de commonjs). Ajoutez cette ligne dans votre package.json:
```json
{
	...
	"type": "module",
	...
}
```

Créez votre fichier index.js où sera le code principal de votre bot:
```js
// Importer le core Artibot
import Artibot from "artibot";

// Créer une nouvelle instance de bot
// Ça s'occupe tout seul de la partie avec Discord.js!
const artibot = new Artibot({
	ownerId: "votre ID Discord",
	testGuildId: "ID de votre serveur de test",
	botName: "Nom de votre bot",
	lang: "fr", // Pour que votre bot et les plugins soient en français
	prefix: "!"
	// Suite de la configuration...
	// Vous en découvrirez plus loin dans ce guide ou dans la documentation.
});

// Démarrer le bot
artibot.login({ token: "token de bot Discord: https://discord.com/developers/applications" });
```

Vous devez maintenant inviter votre bot dans votre serveur. 
Remplacez le client_id dans l'URL suivante par celui de votre bot:

`https://discord.com/api/oauth2/authorize?client_id=12345789123456789&permissions=8&scope=bot%20applications.commands`

Une fois que votre bot a bien rejoint votre serveur, démarrez-le:
```bash
node index.js
```

Ou avec nodemon:
```bash
nodemon index.js
```

Votre bot est maintenant en ligne!

Bien-sûr, puisque aucun plugin n'est installé il n'y a pas encore de fonctionnalités intéressantes.
Vous découvrirez plus bas dans le guide comment ajouter des plugins!

### Les plugins
Plusieurs plugins open-source sont disponibles, vous pouvez donc les installer et les utiliser facilement!

Vous pouvez aussi développer vos propres plugins pour personnaliser votre bot et même les publier par la suite si vous le voulez!

Prenons par exemple le plugin [Giveaways](#), disponible pour tous et très simple à utiliser.

Installez-le comme vous feriez avec n'importe quel module NPM:
```bash
npm i artibot-giveaways
```

Modifiez votre code de lancement pour ajouter un plugin (ou module, si vous préférez les apperler comme ça):
```js
// Importer le core Artibot
import Artibot from "artibot";
// Importer le module Giveaways
import artibotGiveaways from "artibot-giveaways";

// Créer une nouvelle instance de bot
const artibot = new Artibot({
	// Configuration de votre bot
});

// Ajouter le plugin au Artibot avant le démarrage
artibot.registerModule(artibotGiveaways);

// Démarrer le bot
artibot.login({ token: "token de bot Discord: https://discord.com/developers/applications" });
```

Aussi simple que ça!

Certains modules peuvent avoir une configuration (facultative ou obligatoire, au choix du développeur).
Prenons par exemple le module [Welcome](#), qui a une configuration assez complexe:
```bash
npm i artibot-welcome
```

Modifiez votre index.js:
```js
// Importer le core Artibot
import Artibot from "artibot";
// Importer le module Giveaways
import artibotGiveaways from "artibot-giveaways";
// Importer le module Welcome
import artibotWelcome from "artibot-welcome";

// Créer une nouvelle instance de bot
const artibot = new Artibot({
	// Configuration
});

// Ajouter le plugin Giveaways
artibot.registerModule(artibotGiveaways);

// Ajouter le plugin Welcome, qui a besoin d'une configuration
artibot.registerModule(artibotWelcome, {
	// Configuration du module
	// Voir la documentation du module pour comprendre mieux!
	servers: {
		"784679956717240391": {
			welcome: {
				activate: true,
				channel: "877932737850404935",
				showProfilePicture: true,
				showMemberCount: true
			},
			farewell: {
				activate: true,
				channel: "877932737850404935",
				showProfilePicture: false,
				showMemberCount: false
			}
		}
	}
});

// Démarrer le bot
artibot.login({ token: "token de bot Discord: https://discord.com/developers/applications" });
```

Un peu plus complexe car vous devez comprendre la configuration du module mais ça reste assez simple.