[![tests](https://github.com/ddev/ddev-platformsh/actions/workflows/tests.yml/badge.svg)](https://github.com/ddev/ddev-platformsh/actions/workflows/tests.yml) ![project is maintained](https://img.shields.io/maintenance/yes/2024.svg)

## What is ddev-platformsh?

This repository is used with `ddev get ddev/ddev-platformsh` to get a rich integration between your checked-out Platform.sh project and [DDEV](https://github.com/ddev/ddev).

## Using with a Platform.sh project
### Dependencies

Make sure you have [DDEV v1.22.1+ installed](https://ddev.readthedocs.io/en/latest/users/install/ddev-installation/)

### Install
1. Clone your project repository (e.g. `platform get <projectid>`)
2. `cd` into your project directory
3. Run `ddev config` and answer the questions as appropriate
4. Run `ddev get ddev/ddev-platformsh` and answer the questions as appropriate
5. Run `ddev start`
6. (Optional) Run `ddev pull platform` to retrieve a copy of the database and contents from the project's file mounts from the environment you entered in step #5
   1. If you only want to retrieve the database (skipping the file mounts), add the `--skip-files` flag to the `ddev pull platform` command

### Upgrade

To upgrade your version of ddev-platformsh, repeat the `ddev get ddev/ddev-platformsh` to get the latest release. To see the installed version, `ddev get --installed`.

### Run it again if you change your Platform.sh configuration

If you change your `.platform.app.yaml` or something in your `.platform` directory, repeat the `ddev get ddev/ddev-platformsh` so that the generated configuration for DDEV will be updated.

## Notes

* If your local project has a different database type than the upstream (Platform.sh) database, it will conflict, so please back up your database with `ddev export-db` and `ddev delete -y` before starting the project with new config based on upstream.
* Your experience is super-important: Please let us know about how it went for you in any of the [DDEV support venues](https://ddev.readthedocs.io/en/latest/users/support/)

## What does it do right now?

* Works with many projects of type `php`, for example, `php:8.1` or `php:8.2`. It does not work with non-php projects.
* Takes your checked-out Platform.sh project and configures DDEV based on that information.
    * PHP and Database version
    * hooks are converted to DDEV post-start hooks
    * A working `ddev pull platform` integration with all mounts is created.
    * Exposes specific `$PLATFORM_` variables (e.g., `$PLATFORM_RELATIONSHIPS`, `$PLATFORM_ROUTES`)
* Supports the following services:
    * Databases
      * MariaDB
      * Oracle MySQL
      * Postgresql
    * Redis
    * Redis-persistent
    * Memcached
    * ElasticSearch
* Provides the following [Platform.sh-provided environmental variables](https://docs.platform.sh/development/variables/use-variables.html#use-platformsh-provided-variables): 
  * PLATFORM_APP_DIR
  * PLATFORM_APPLICATION_NAME
  * PLATFORM_CACHE_DIR
  * PLATFORM_ENVIRONMENT
  * PLATFORM_PROJECT
  * PLATFORM_PROJECT_ENTROPY
  * PLATFORM_RELATIONSHIPS
  * PLATFORM_ROUTES
  * PLATFORM_TREE_ID
  * PLATFORM_VARIABLES

## What has been tested

These Platform.sh templates are included in the automated tests that run nightly. They will be growing in maturity with your feedback!

* [php](https://github.com/platformsh-templates/php)
* [drupal9](https://github.com/platformsh-templates/drupal9) and [drupal10](https://github.com/platformsh-templates/drupal10)
* [laravel](https://github.com/platformsh-templates/laravel)
* [magento2ce](https://github.com/platformsh-templates/magento2ce)
* [wordpress-composer](https://github.com/platformsh-templates/wordpress-composer)

(Each of the above but magento2ce has automated tests.)

## What will it do in the future

- [x] Populate important PLATFORMSH environment variables that would be found upstream
- [x] Populate PHP and other dependencies configured upstream
- [x] Automatically figure out the name and other information of the upstream project
- [x] Automatically configure the .ddev/providers/platform so you can immediately do a `ddev pull platform` with no configuration effort.
- [ ] Let us know what's important to you!

**Contributed and maintained by [@rfay](https://github.com/rfay) and [@lolautruche](https://github.com/lolautruche)**


