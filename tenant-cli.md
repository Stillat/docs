# Advanced Tenant Command Line Interface (CLI)

- [Installing the Tenant Server](#cli-install)
- [Removing the Tenant Server](#cli-uninstall)
- [Creating a Tenant](#cli-create)
- [Dropping a Tenant](#cli-drop)
- [Resolving Tenant Names](#cli-name)
- [Running Migrations on Tenants](#cli-migrations)

<a name="cli-install"></a>
## Installing the Tenant Server

In order for the tenant service to function, there needs to be one central database. We will call this the Tenant Server. This is usually the same database that holds the user's credentials and other common tables. Installing the tenant service is similar to installing the migrations table in Laravel. To install the tenant server tables, just run the `tenant:install` Artisan command:

    php artisan tenant:install

After the command has run, you will see (depending on your configuration) output similar to:

    Tenant table created successfully.
    Tenant account table created successfully.

<a name="cli-uninstall"></a>
## Removing the Tenant Server

To remove the tenant server tables, you can run the `tenant:uninstall` Artisan command:

    php artisan tenant:uninstall

This will produce output similar to the following:

    Tenant table removed successfully.
    Tenant account table removed successfully.

Currently, this command leaves the tenant databases available.

<a name="cli-create"></a>
## Creating a Tenant

You can create tenants, or account databases from the Artisan command line. To do this, use the `tenant:create <account_id>` Artisan command. This command accepts only one parameter: the name of the tenant, or account id. This *should* be a number.

For example, if we wanted to create a new tenant database for an account with an ID of `10` we would run this command:

    php artisan tenant:create 10

And then, depending on your configuration you will see output similar to this:

    dndoqqmezcaqqciokiidneemdamneecz created successfully

It should also be noted that this command will also create a `migrations` table for your new tenant database.

<a name="cli-drop"></a>
## Dropping a Tenant

After you have creating tenant databases, there will come a time when you have to remove them. Of course you could do this from your application code quite easily, but you can also achieve the same result by using the Artisan command `tenant:drop <account_id>`. This command accepts only one parameter: the ID of the tenant account. This **has** to be an integer, representing the tenant account.

If we wanted to drop the tenant we created in the above example, we could run this command:

    php artisan tenant:drop 10

If the drop was successful you will see output similar to this:

    dndoqqmezcaqqciokiidneemdamneecz dropped successfully

<a name="cli-name"></a>
## Resolving Names

You can find out, or resolve, the name the tenant service will give a particular database by using the `tenant:name <account_id>` Artisan command. This command accepts only one parameter: the name of the tenant, or account id. This is usually a number, but it could be any string or number.

> **Note:** In a future release, it is highly likely that the `tenant:name` command will only accept integers.

For example, if we wanted to find out what the tenant service would name a database with an account ID of `10`, we would run this command:

    php artisan tenant:name 10

Depending on your configuration, you will see output similar to this:

    dndoqqmezcaqqciokiidneemdamneecz

> **Note:** A tenant does **not** have to exist in order to determine what name it will be given.

<a name="cli-migrations"></a>
## Tenant Migrations

Laravel provides migrations, a type of version control for your databases. The tenant service allows you to run migrations on your tenant services, and this is overwhelmingly useful.

### Running Migrations

The following commands will perform their function on all tenant databases. To perform similar actions on the tenant server itself, see Laravel's documentation on migrations.

#### Running All Outstanding Migrations

    php artisan tenant:migrate

#### Running All Outstanding Migrations For A Path

    php artisan tenant:migrate --path=app/foo/migrations

#### Running All Outstanding Migrations For A Package

    php artisan tenant:migrate --package=vendor/package

> **Note:** If you receive a "class not found" error when running tenant migrations, try running the `composer dump-autoload` command.

### Rolling Back Migrations

#### Rollback The Last Migration Operation

    php artisan tenant:rollback

#### Rollback All Migrations

    php artisan tenant:reset

#### Rollback All Migrations And Run Them Again

    php artisan tenant:refresh