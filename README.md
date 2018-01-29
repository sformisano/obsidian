# Obsidian &mdash; A WordPress Starter Kit For The Modern Web

*Please note: this project is a work in progress. The CI script is customised around my personal needs and would require you to update it in order to fit yours. I have no reliable timeline for it, but I do plan to standardise Obsidian to the point that most people can not only use it to quickly setup a local development environment, but to also be able to deploy via SSH/RSYNC or SFTP to any server of their choosing.*

Obsidian is a WordPress starter kit that allows you to easily provision local development environments and setup CI/CD for WordPress websites. This project is based on:

* **[Bedrock](https://github.com/roots/bedrock):** a WordPress boilerplate which turns WordPress into a [12 Factor App](https://12factor.net/).
* **[Lando](https://docs.devwithlando.io/):** a Docker based local development environment that you can provision through a simple `.lando.yml` file, in a similar way to what's done for services like Travis CI.
* **[GitLab CI](https://about.gitlab.com/features/gitlab-ci-cd/):** The CI/CD pipelines service from GitLab, i.e. if you want to use this starter kit as is, you must host your repository on GitLab or at least have a GitLab remote you push to for your CI/CD needs.

## How to Start a New Project With Obsidian

Before diving into Obsidian, make sure you have [Docker](https://www.docker.com/community-edition#/download) and [Lando](https://docs.devwithlando.io/installation/installing.html) installed.

Once that's done, clone this repository and run the `npm run setup` command inside the repository directory.

This will let you setup the project directly through command line by taking your input and then generating the `.lando.yml` file, creating and starting the docker containers, downloading the dependencies, initialising the database etc.

Once this process is completed, your local WordPress website will be available at the `subdomain.lndo.site` address you specified during the setup (`.lndo.site` is static, you get to pick the subdomain).

## How to Stop and Start an existing Obsidian Project 

To stop a running project, run this command inside the project's directory:

```
lando stop
```

To start the project again, run this command inside the project's directory:

```
lando start 
```

If you want to know more about what you can do with Lando, read the [documentation](https://docs.devwithlando.io/).

## Did You See Red URLs? A Note on DNS Rebinding

This is taken directly from the Lando documentation you can find [here](https://docs.devwithlando.io/issues/dns-rebind.html).

If you are using Lando proxying (which is enabled by default) some Routers and Firewalls may prevent Lando from properly routing yourapp.lndo.site to your local environment through DNS Rebinding protection. DD-WRT router firmware enables this protection by default.

If you are seeing failed URLs (they show up in red) after app start up and you are unable to look up the url (nslookup <sitename>.lndo.site), DNS rebinding protection may be the cause. We recommend you consult your router documentation or system administrator to whitelist *.lndo.site domains.

If you can't or don't want to remove this protection, you can alternatively:

* Use the steps in Working Offline to bypass.
* Disable proxying and rely on the Lando produced localhost address.

### DD-WRT Solution

If you use DNSMasq on the DD-WRT firmrware:

1. Open the services page of the DD-WRT administration panel
2. Go to the "Additional DNSMasq Options" section
3. Add the following line in the textarea `rebind-domain-ok=/lndo.site/`

If you already had the rebind-domain-ok line for other domains, you can add multiple ones like this:

`rebind-domain-ok=/domain1.com/domain2.com/domain3.com/`

# Credits

As mentioned in the introduction, this project is just an aggregator of other people's work with a few modifications and extra things added by me. Here's a list of people you should thank if you end up using Obsidian:

* **[The Roots team](https://roots.io/):** they are the authors of the Bedrock WordPress boilerplate.
* **[The ThinkTandem team](https://thinktandem.io/):** the authors of Lando. Also, the setup script triggered by the `npm run setup` is a slightly modified version of a script available in their [WP-Boilerplate](github.com/thinktandem/wp-boilerplate). I created Obsidian when I stumbled upon Lando and their WP-Boilerplate and wanted to have a version of all that to work with my own default plugins/theme and CI/CD setup.
* **Plugin Authors:** take the time to see who makes the plugins I use in this starter kit, each developer/team behind them deserves a huge thanks for making them available to everyone for free.
* **[The GitLab team](https://gitlab.com/):** the pipelines feature is awesome and available to everyone for free even for private repositories.

#### Why Is it Called Obsidian?

The biggest piece of this starter kit is the `Bedrock` WordPress boilerplate, which I assume was named after "*the lithified rock that lies under a loose softer material called regolith at the surface of the Earth or other terrestrial planets*". Since Obsidian is "*a naturally occurring volcanic glass formed as an extrusive igneous rock*", i.e. a rock that I think is [a lot cooler](http://awoiaf.westeros.org/index.php/Dragonglass), I just named after it to keep the rocks theme going.
