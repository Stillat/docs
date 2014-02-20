# Advanced Tenant Command Line Interface (CLI)

- [Creating a Tenant](#cli-create)
- [Dropping a Tenant](#cli-drop)
- [Resolving Tenant Names](#cli-name)

<a name="cli-create"></a>
## Creating a Tenant

You can create tenants, or account databases from the Artisan command line. To do this, use the `tenant:create <account_id>` Artisan command. This command accepts only one parameter: the name of the tenant, or account id. This *should* be a number.

For example, if we wanted to create a new tenant database for an account with an ID of `10` we would run this command:

    php artisan tenant:create 10

And then, depending on your configuration you will see output similar to this:

    dndoqqmezcaqqciokiidneemdamneecz created successfully

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