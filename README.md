# WP Boilerplate

WP Boilerplate was originally created for use internally within our development team to maintain consistent repositories across our projects. However, this repository and its companion packages may be of some use to others. Feel free to use in your own projects, your mileage may vary. 

## Requirements

* Composer
* PHP >= 5.3.9
* Virtual machines or development environment, such as Vagrant.

## Notes

* The configuration for this boilerplate is inspired by Laravel 5's dotenv mechanism using  .env files.
* This setup has been designed to work within a Vagrant environment, it may work in other flavours as long as the project has its own host entry/vhost and isn't set up as a subdomain install.
* Similar to Laravel and other frameworks, the WordPress files are stored in the `public` directory and this directory should be set as the document root for your project. 
* Ensure you have a host entry configured for the project. 

## Companion Packages

This repository comes with the following composer packages preloaded to provide additional features for this boilerplate:

* [scottjs/wp-dotenv](https://github.com/scottjs/wp-dotenv) - Enables WordPress to use dotenv config files. 
* [scottjs/db-sync](https://github.com/scottjs/db-sync) - Scripts to quickly sync a remote database to a local database, as well as safe search/replace.
* [scottjs/helper-scripts](https://github.com/scottjs/helper-scripts) - Other scripts to assist with common tasks, such as allowing remote uploads to load locally. 

## Installation

1. Download/extract a copy of this repository to a location accessible by your local environment.
2. Copy, paste and rename `.env-sample` to `.env`.
3. Update the `.env` configuration options as necessary. 
4. Within your environment terminal, browse to the project root folder, e.g. `cd /var/www/<project-name>`
5. Run `composer install` to download the companion packages and install WP core.
6. Run `composer generate-config` or `composer generate-config-with-salts` to create a modified WordPress config that uses the .env config file. 
7. Visit the project in your browser and continue to set up the local database as normal. 
8. Install or build your theme and begin development.

## Usage

To use the features of the companion packages mentioned above, the following composer commands have been added to the composer.json file:

* ***composer generate-config*** - All of the companion packages rely on the .env file to get their configuration. This command will generate a modified wp-config.php file to allow WordPress to also use the .env file and avoids having to maintain two config files. This requires `APP_DOCROOT` to be set in the .env file.

* ***composer generate-config-with-salts*** - As above, but will also generate the salts automatically. This is a handy  command to use when starting a new project, but it can be used at any time.
	
* ***composer database-update*** - When working on an active project, your local database might be too out of date from the database in staging or production. This command will backup and empty your locally configured database and update it with copy of your remote or production database. This requires all `DB_*` and `REMOTE_DB_*` options to be set in the .env file and also assumes your remote database is accessible externally.

* ***composer database-prepare*** - When developing locally, links to images and assets might be referencing your local development web address and won't work in staging or production. This command will run a safe search/replace script on your locally configured database, replacing all instances of `DOMAIN_LOCAL` with `DOMAIN_REMOTE` configured in the .env file. The database will then be exported to `dumps/prepared-database-YYYY.MM.DD-HH.MM.SS.sql` ready for deployment.

* ***composer remote-uploads-enable*** - When developing locally on an active project, it's likely that the main uploads folder is not bundled within your repository, causing CMS uploaded images not to load. This command will install a local .htaccess file in your configured uploads directory and will redirect all requests to the remote server instead. This requires `DOMAIN_REMOTE`, `APP_DOCROOT` and `APP_UPLOADS` to be set in the .env file. It's recommended to ignore this .htaccess file from your project repository.

* ***composer remote-uploads-disable*** - A convenient helper command to remove the .htaccess file created by the command above just in case you find it causes issues. This assumes that the .env configuration hasn't changed since it was added.

## Configuration Options

See below for an explanation of each configuration option used within the .env file.

* ***DOMAIN_REMOTE*** - Required by ***composer database-prepare*** and ***composer remote-uploads-enable***, it should point to your remote or production environment (if available) and not include http:// or trailing slashes. Example: `www.example.com` or `subdomain.example.com`.

* ***DOMAIN_LOCAL*** - Required by ***composer database-prepare***, it should not include http:// or trailing slashses. Example: `www.example.local` or `subdomain.example.local`.

* ***APP_DOCROOT*** - Required by ***composer generate-config*** and ***composer remote-uploads-enable***, it should be relative to your project root folder and point to where the document root is configured. It should start with a slash and not include a trailing slash. Leave blank if not applicable. Example: `/public`.

* ***APP_CORE*** - Required only if using the wp-config.php file generated by ***composer generate-config*** and if WP core files are located in a subdirectory. It should point to the directory where WP core is installed relative to `APP_DOCROOT`. It should start with a slash and include a trailing slash. Leave blank if not applicable. Example: `/wp`.

* ***APP_UPLOADS*** - Required by ***composer remote-uploads-enable*** and should point to the remote URL where remote uploads are located relative to `DOMAIN_REMOTE`. It should start with a slash and not include a trailing slash. Example: `/wo-content/uploads`.

* ***APP_DEBUG*** - Required only if using the wp-config.php file generated by ***composer generate-config***. Allows you to enable or disable WP debugging. Options: `true` or `false`.

* ***APP_WWW*** - Required only if using the wp-config.php file generated by ***composer generate-config***. Allows you to force WordPress to redirect to www or non-www web addresses. Options: `true` or `false`.

* ***APP_SSL*** - Required only if using the wp-config.php file generated by ***composer generate-config***. Allows you to force WordPress to use the SSL protocol handle redirection. Options: `true` or `false`.

* ***DB_**** - Required only if using the wp-config.php file generated by ***composer generate-config*** and provides options to set the local database configuration details.

* ***REMOTE\_DB_**** - Required by ***composer update-database*** and provides options to set the remote staging or production database configuration details.

