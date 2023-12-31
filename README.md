# Local development using Lando for setting up a Drupal site.
Using lando to build a decoupled drupal site.
JSON:API module is enabled serve content to the front end which for development purpose will be using Nuxt/Vue framework.

## Prerequisite
Installations for WSL2
1. Docker desktop (https://docs.docker.com/desktop/windows/install/)
2. Get latest lando (3.18 at the time of writing this). Preferred method so WSL to Lando path works.
    a. install into WSL root directory
        https://github.com/lando/lando/releases/download/v3.18.0/lando-x64-v3.18.0.deb
    b. run the land
        sudo dpkg -i lando-x64-v3.18.0.deb

## Starting Drupal with Lando
1. Ensure docker (docker -v) desktop and lando (lando -v) is up and running.
2. Run the following command in order

```bash
# composer with drush to be used later
lando composer install 
```

```bash
# this will create the app and will have the appserver urls including the proxies.
lando start
```

![Appserver](image.png)

```bash
# Database with some book content
lando db-import dump.sql.gz 
```

```bash
# Import configs (probably not needed but this is related to RESTFUL Web Service module view)
lando drush cim -y
```

```bash
# Quick password update
lando upwd admin "password"
```

```bash
# Clear Drupal cache to bring in latest change.
lando drush cr
```

Check that Drupal site is up and running and also the jsonapi link is there e.g https://vic-uni-book.lndo.site/jsonapi/node/books
