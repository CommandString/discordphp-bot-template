# DiscordPHP Bot Template
An unofficial way to structure a discordPHP bot.

# Table of Contents
* [Installation](#installation)
* [Configuration](#configuration)
* [Slash Commands](#slash-commands)
* [Events](#events)
* [Disabling Commands and Events](#disabling-commands-and-events)

# Installation

```
composer create-project commandstring/dphp-bot
```

# Important Resources #

[DiscordPHP Class Reference](https://discord-php.github.io/DiscordPHP/guide/)

[DiscordPHP Documentation](https://discord-php.github.io/DiscordPHP/)

[DiscordPHP Discord Server](https://discord.gg/kM7wrJUYU9)
*Only ask questions relevant to using DiscordPHP's own wrapper, not on how to use this.*

#[Developer Hub]()

# Configuration

Copy the `.env.example` file to `.env` and add your bot token.

# Slash Commands

Create a class that implements `Core\Commands\CommandHandler` and attach the `Core\Commands\Command` attribute to it.

```php
<?php

namespace Commands;

use Core\Commands\Command;
use Core\Commands\CommandHandler;
use Discord\Builders\CommandBuilder;
use Discord\Parts\Interactions\Interaction;

use function Core\messageWithContent;

#[Command]
class Ping implements CommandHandler
{
    public function handle(Interaction $interaction): void
    {
        $interaction->respondWithMessage(messageWithContent('Ping :ping_pong:'), true);
    }

    public function autocomplete(Interaction $interaction): void
    {
    }

    public function getConfig(): CommandBuilder
    {
        return (new CommandBuilder())
            ->setName('ping')
            ->setDescription('Ping the bot');
    }
}
```

Once you start the bot, it will automatically register the command with Discord.
And if you make any changes to the config, it will update the command on the fly.

# Events

Create a class that implements any of the interfaces found inside of `Core\Events`.
Implement the interface that matches your desired event.

```php
<?php

namespace Events;

use Core\Events\Init;
use Discord\Discord;

class Ready implements Init
{
    public function handle(Discord $discord): void
    {
        echo "Bot is ready!\n";
    }
}
```

# Disabling Commands and Events

If you want to disable a command handler or event listener attach the `Core\Commands\Disabled` attribute to it.

```php
<?php

namespace Events;

use Core\Events\Init;
use Discord\Discord;

#[Disabled]
class Ready implements Init
{
    public function handle(Discord $discord): void
    {
        echo "Bot is ready!\n";
    }
}
```
