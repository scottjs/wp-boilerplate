# WP Boilerplate

WP Boilerplate was originally created for use internally within our development team to maintain a consistent deployment workflow across projects. However, this repository and its companion packages may be of some use to others. Feel free to use in your own projects, your mileage may vary. 

## Requirements

* Composer
* PHP 5.3.9

## Notes

* The configuration for this boilerplate is inspired by Laravel 5's dotenv mechanism using  .env files.
* This setup has been designed to work within a Vagrant environment, it may work in other flavours as long as it has its own host entry/vhost and isn't set up as a subdomain install.
* Similar to Laravel and other frameworks, the WordPress files are stored in the `public` directory and this directory must be set as the document root for your project. 

## Installation

1. Download/extract a copy of this repository to a location accessable by your local environment. Ensure that the `public` directory is set to the document root and you have a host entry configured for the project. 
2. Copy, paste and rename `.env-sample` to `.env`.
3. Update the `.env` configuration options as necessary. 
4. Run `composer install` to download the companion packages and install WP core.
5. Run `composer generate-config` to create a modified WordPress config that supports the .env file. You can run `composer generate-config-with-salts` if you would like the salts automatically generated. 
6. Visit the project in your browser and continue to set up the local database as normal. 
7. Install your theme and begin development.

## Configuration

TODO

## Companion Packages

TODO
