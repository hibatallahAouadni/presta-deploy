# Prest-deploy configuration

This documentation describes basic principles of presta-deploy configuration.

Configuration is managed at three different levels :
1. ***local configuration*** level is defined for presta-deploy.
    
    This configuration is managed by ``infra/env/deploy.env`` file and you can find a precise description of this file in ``infra/env/deploy.env.template``.
2. ***environment configuration*** level is defined for ``$DEPLOY_ENV`` environment.
    
    This configuration is defined by ``infra/env/data/{$DEPLOY_ENV}/*.env`` files. You can find description in ``infra/env/template/*.env`` files.
    > :point_up: *environment configuration* depends on *local configuration*.
3. ***services configuration*** level is defined for ``$DEPLOY_ENV`` environment for each service managed by presta-deploy

    This configuration is defined by ``infra/env/data/{$DEPLOY_ENV}/{service_tag}/`` directories. You can find description in ``infra/env/template/{service_tag}/`` directories.
    > :point_up: *services configuration* depends on *environment configuration*.


## Configuration conventions

All configuration files are stored under ``infra/env/``

| ``env`` element        | Description                                                                                                               |
|------------------------|---------------------------------------------------------------------------------------------------------------------------|
| ``deploy.env``         | file used for presta-deploy self configuration.                                                                           |
| ``infra/env/template`` | prestashop configuration template (files list, directory structure, ...)                                          |
| ``infra/env/data``     | stores defined environment ( ``dev`` / ``development`` / ``test`` / ``demo`` / ... )                                      |
| ``infra/env/backup``   | stores cleaned/removed environments. This backup should give you a chance to restore a mistake due to ``make`` commandes. |


## Configuration process

In order to understand configuration usage, you can take a look at Makefile ``config-*`` commands.

For install, please follow this process :
1. *local configuration*
    1. ``cp infra/env/deploy.env.template infra/env/deploy.env``
    2. Edit ``deploy.env`` values.
2. *environment configuration*
    1. ``make config-prepare-env``
    2. Edit all ``*.env`` values you need.
3. *services configuration*
    1. ``make config-apply-env``


## Using environment variables

If you have *.env files, variables from env files are used.

If files not defined, variables are defined from environment.

If you don't have .env files neiher environment variables, you should encounter some weird behaviour.