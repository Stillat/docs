# Installing Stillat/Common

- [Via Composer](#via-composer)
- [Tenant Facade](#tenant-facade)
- [Configuration](#config)

<a name="via-composer"></a>
## With Composer

To install `Stillat/Common` edit your project's `composer.json` file to require `stillat/common`.

    "require": {
        "stillat/common": "dev-master"
    }

Next, update Composer from the command line:

    composer update

Once Composer has finished updating, you can add the service provider. Open your `app/config/app.php` file and add a new service provider to the providers array:

    'Stillat\Common\CommonServiceProvider',

<a name="tenant-facade"></a>
## Tenant Facade

If you want to use the Tenant service, and want to access it's properties and functions by using a `Tenant` facade, open your `app/config/app.php' file file and add a new entry to the aliases array:

    'Tenant'          => 'Stillat\Common\Facades\Tenant',

<a name="config"></a>
## Configuration

To modify the configuration options that are available to you, you first have to publish the configuration for this package. Do this using Artisan by running this command:

    php artisan config:publish stillat/common

