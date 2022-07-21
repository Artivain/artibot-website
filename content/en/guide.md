---
title: "Guide"
date: 2022-07-15T11:12:06-04:00
type: "page"
subtitle: "Simplified documentation to learn how to use this framework"
---

## Table of Contents
1. [How it works?](#how-it-works)
	1. [Prerequisites](#prerequisites)
	2. [Create your bot](#create-your-bot)
	3. [Plugins](#plugins)

## How it works?

### Prerequisites
- Node.js and NPM (we recommend the latest LTS version)
- A code editor (Visual Studio Code or another)
- Some JavaScript or TypeScript development knowledge
- Yes, just that

### Create your bot
Create a new Node.js and NPM project:
```bash
npm init
```

Install the Artibot core:
```bash
npm i artibot
```

We also recommend [nodemon](https://nodemon.io/) to facilitate the development of your bot:
```bash
npm i nodemon --save-dev
```

Put your project in ESM mode (instead of commonjs). Add this line in your package.json:
```json
{
	...
	"type": "module",
	...
}
```

Create your index.js file where your bot's main code will be:
```js
// Import the Artibot Core
import Artibot from "artibot";

// Create a new bot instance
// It takes care of the part with Discord.js!
const artibot = new Artibot({
	ownerId: "your Discord ID",
	testGuildId: "ID of your test server",
	botName: "Name of your bot",
	lang: "en", // To make the core and plugins use English
	prefix: "!"
	// Continuation of the configuration...
	// You'll find out about that later in this guide or in the documentation.
});

// Start the bot
artibot.login({ token: "your bot token: https://discord.com/developers/applications" });
```

Now you need to invite your bot to your server.
Replace the client_id in the following URL with the one of your bot:

`https://discord.com/api/oauth2/authorize?client_id=12345789123456789&permissions=8&scope=bot%20applications.commands`

Once your bot has successfully joined your server, start it:
```bash
node index.js
```

Or with nodemon:
```bash
nodemon index.js
```

Your bot is now online!

Of course, since no plugin is installed there are no interesting features yet.
You will discover further down in the guide how to add plugins!

### Plugins
Several open-source plugins are available, so you can easily install and use them!

You can also develop your own plugins to customize your bot and even publish them afterwards if you want!

Take for example the [Giveaways](/en/plugins/giveaways/) plugin, available to everyone and very easy to use.

Install it as you would any NPM module:
```bash
npm i artibot-giveaways
```

Edit your launch code to add a plugin (or module, if you prefer to call them this way):
```js
// Import the Artibot core
import Artibot from "artibot";
// Import the Giveaways module
import artibotGiveaways from "artibot-giveaways";

// Create a new bot instance
const artibot = new Artibot({
	// Configuring your bot
});

// Add the plugin to the Artibot before starting it
artibot.registerModule(artibotGiveaways);

// Start the bot
artibot.login({ token: "your bot token: https://discord.com/developers/applications" });
```

As simple as that!

Some modules can have a configuration (optional or mandatory, developer's choice).
Take for example the [Welcome](/en/plugins/welcome/) module, which has quite a complex configuration:
```bash
npm i artibot-welcome
```

Edit your index.js:
```js
// Import the Artibot core
import Artibot from "artibot";
// Import the Giveaways module
import artibotGiveaways from "artibot-giveaways";
// Import the Welcome module
import artibotWelcome from "artibot-welcome";

// Create a new bot instance
const artibot = new Artibot({
	// Configuration
});

// Add the Giveaways plugin
artibot.registerModule(artibotGiveaways);

// Add the Welcome plugin, which needs configuration
artibot.registerModule(artibotWelcome, {
	// Configure module
	// See module documentation to understand better!
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

// Start the bot
artibot.login({ token: "your bot token: https://discord.com/developers/applications" });
```

A little more complex because you have to understand the configuration of the module but it's still quite simple.