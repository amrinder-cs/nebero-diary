Monday 12 August 2024 

# Back to work

I had 2 days off at the weekend, so i went back home. It was raining cats and dogs when i arrived, and same while leaving.
Anyhow, I continued with learning Laravel today.


# Prerequisites

Before installing Laravel, i needed to install PHP's dependency manager.

One thing i love about PHP's dependency manager is that it doesn't just force you to work, instead it does things by itself. Such as if you are using old packages, it automatically updates them to the latest without you having to change stuff in Node. 

No matter what you use, node - Bun or yarn, all of them just throw deprecation notices on your face and expect them to dive back into coding just to update the old methods, Laravel does not do that. It just fixes the stuff for you and tells you what it could not. Good for backwards compatibility and also good for keeping your software running long term.

## Installing Composer

If you have PHP installed, installing Composer is very simple:

```bash
curl -sS https://getcomposer.org/installer | php
```

since we want to use composer from anywhere, we will need to move it to our binaries folder in linux:

```bash
sudo mv composer.phar /usr/local/bin/composer
```

then we run `composer --version` to check if we have it installed and working.

## updating composer
updating composer is quite simple as well:

```bash
composer self-update
```

how thoughtful



# exploring Laravel projects to use for testing

Now since i will be testing Laravel projects, i had to find some pre made projects to test (since i am not Laravel developer, just the DevOps guy)

Finding a project wasn't easy, so i just stuck to the basics and used the default Laravel application for testing, however then the time was over, so i decided to continue it next day
