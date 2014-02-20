# Basic Tenant Usage

-[Configuration](#configuration)

<a name="configuration"></a>
## Configuration

Stillat makes connecting a single application instance to multiple databases at a time. This can be useful when developing Software as a Service (SaaS) applications. The tenant configuration file should be `app/config/tenant.php`. If this file does not exist (likely if you have just installed the Stillat framework), you should create it.

The default configuration file should look like this:

    <?php

    return array(

        /*
        |--------------------------------------------------------------------------
        | Default Tenant Table Names
        |--------------------------------------------------------------------------
        |
        | This option controls the names of the tables that the tenant manager will
        | create when you run commands such as tenant:install, amongst other things.
        |
        */
        'tableNames' => array(

            'tenantTable' => 'tenants',

            'accountsTable' => 'tenant_accounts',
        ),

        /*
        |--------------------------------------------------------------------------
        | Schema Prefix
        |--------------------------------------------------------------------------
        |
        | An optional two character schema prefix to be used when creating or
        | dropping schemas. This should remain consistent.
        |
        */
        'schemaPrefix' => '',

        /*
        |--------------------------------------------------------------------------
        | Preserve Connection Read/Write Values
        |--------------------------------------------------------------------------
        |
        | This option indicates whether or not the tenant service will attempt to
        | preserve the default connections read and write database options.
        |
        | A sensible default has been set.
        |
        */
        'preserveReadWrite' => false,

        /*
        |--------------------------------------------------------------------------
        | Migration Behavior
        |--------------------------------------------------------------------------
        |
        | This option controls the migration behavior when running migrations on
        | multiple tenants. The mode 'except' will run all the migrations that
        | have been defined except what is listed here. The mode 'only' will only
        | run the migrations that have been listed here.
        |
        | A sensible default has been set.
        |
        */
        'migrationBehavior' => 'except',

        /*
        |--------------------------------------------------------------------------
        | Migrations
        |--------------------------------------------------------------------------
        |
        | A list of migrations that the tenant service will use when running
        | migrations on tenant servers. Refer to the "Migrations Behavior" setting
        | to see what can be done with this before adding new migrations here.
        |
        | Note: You do not have to specify any migrations if you do not want to.
        */
        'migrations' => array(
            'CreateUsersTable'
        ),

    );