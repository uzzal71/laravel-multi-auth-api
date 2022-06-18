# laravel-multi-auth-api
Laravel Multiple Auth API

### Step 1 : Create Laravel 9 Fresh Application
```
composer create-project --prefer-dist laravel/laravel laravel_multi_auth_api
```

### Step 2 : Setup Database
```
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=DatabaseName
DB_USERNAME=DatabaseUserName
DB_PASSWORD=DatabasePassword
```

### Step 3 : Create Admin Table
```
php artisan make:model Admin -m
```

database/migrations/2022_06_18_164237_create_admins_table.php
```
<?php

use Illuminate\Database\Migrations\Migration;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;

return new class extends Migration
{
    /**
     * Run the migrations.
     *
     * @return void
     */
    public function up()
    {
        Schema::create('admins', function (Blueprint $table) {
            $table->id();
            $table->string('name');
            $table->string('email')->unique();
            $table->timestamp('email_verified_at')->nullable();
            $table->string('password');
            $table->rememberToken();
            $table->timestamps();
        });
    }

    /**
     * Reverse the migrations.
     *
     * @return void
     */
    public function down()
    {
        Schema::dropIfExists('admins');
    }
};
```
Use this command to run migration

```
php artisan migrate
```

### Step 4 : Install Json web token (jwt)
```
composer require php-open-source-saver/jwt-auth
```

Next, we need to make the package configurations public. Copy the JWT configuration file from the vendor to confi/jwt.php with this command:

```
php artisan vendor:publish --provider="PHPOpenSourceSaver\JWTAuth\Providers\LaravelServiceProvider"
```

Now, we need to generate a secret key to handle the token encryption. To do so, run this command:

```
php artisan jwt:secret
```

This will update our .env file with something like this:
```
JWT_SECRET=xxxxxxxx
```
This is the key that will be used to sign our tokens.