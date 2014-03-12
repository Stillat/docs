# Basic Tenant Usage

- [Introduction](#introduction)
- [Configuration](#configuration)
- [ORM and Models](#orm)

<a name="introduction"></a>
## Introduction

Some applications require that each client organization have their application data isolated from other client organizations. This requires that one application instance, in this case your Laravel application, can connect and respond to multiple database connections and servers for any given request. This can be accomplished by creating a new connection entry for each client in your `app/config/database.php` configuration file, but this can become unmaintainable quite quickly, especially if your service is quite popular and you are adding new connections all the time. A better solution would be a hands-off, dynamic system where you could assign users to tenants, or remove them at any given time.

The Stillat Tenant service makes getting a setup like this running quickly. Using the Tenant service, you can define what migrations will run on your clients tenants (databases). It also provides Artisan commands to create or remove client tenants, run migrations or roll them back. In addition to the Artisan commands, it also exposes a simple API to make using it simple.

<a name="configuration"></a>
## Configuration

The Tenant service has quite a few configuration options that you can modify. They will be located in the `app/config/packages/stillat/common/tenants.php` file.

<a name="orm"></a>
## ORM and Models

The Stillat Tenant service allows developers to leverage Laravel's Eloquent ORM for mutli-tenant applications. It also realizes that there are instances where you need your application models to communicate to a central server (for things such as user authentication and some logging) and need other models to communicate with your client's individual tenant database.

The Stillat Tenant service does this by extending Eloquent's `Model` class and making a few changes. This means that you can use your models just like you are used to. The only change you have to make to your model is to extend from the Tenant service's model class instead of Eloquent's:

    <?php

    use Stillat\Common\Database\Tenant\Model as Eloquent;

    class Message extends Eloquent {
        
        protected $table = 'messages';

        public $timestamps = true;

    }

After making this change, the Tenant service will know that when you use the `Message` model, it should connect to the current user's tenant database instead of the central hub database.

Let's consider an example where we use Laravel's default `User` model, which would connect to the central hub database, and our `Message` model above, which would connect to a user's tenant. We could write code like this:

    <?php

    Routes::get('/', function()
    {
        
        // This would use the central hub database.
        $user = User::findOrFail(1);

        // This would create a new message on an entirely different database.
        $message = new Message;
        $message->title   = 'Hello There';
        $message->content = 'You look friendly.';
        $message->save();
        
    });