+++
title = "Impletment User Auth Username or Email in Laravel"
date = "2023-05-04T14:33:46+02:00"
tags = ["FRAMEWORK"]
categories = ["FRAMEWORK"]
authors = ["Tejiri Mayone"]
banner = "/img/post/laravel.jpeg"
+++

## Introduction
Laravel is a popular PHP framework that is widely used for web application development. One of the most important features of any web application is authentication. In this blog, we will look at how to perform authentication with email or username in Laravel 10.

#### Step 1: Install Laravel 10

To get started, you need to have Laravel 10 installed on your system. You can install it using Composer by running the following command in your terminal:
Click [Laravel site for other options](https://laravel.com/docs/10.x/installation)

```
composer create-project laravel/laravel your-project-name  --prefer-dist "10.*"
```

#### Step 2: Create a new Laravel project

Once you have installed Laravel 10, create a new Laravel project using the following command:


```
php artisan new your-project-name
```

#### Step 3: Setup the database

Next, you need to setup the database connection in the .env file. Open the .env file in the root directory of your Laravel project and update the following lines with your database details:

```
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=your_database_name
DB_USERNAME=your_database_username
DB_PASSWORD=your_database_password
```

#### Step 4: Generate the Authentication Scaffolding

Laravel provides an easy way to generate authentication scaffolding using the `make:auth` command. To generate the authentication scaffolding, run the following command:

```
php artisan make:auth
```

This command will generate the necessary views, routes, controllers, and migrations required for authentication.

#### Step 5: Add Username Column
Now add new column username to your users table, so you can simply update your migration as like bellow.

##### migration
`database/migrations/`

```
<?php

  

use Illuminate\Database\Migrations\Migration;

use Illuminate\Database\Schema\Blueprint;

use Illuminate\Support\Facades\Schema;

  

class CreateUsersTable extends Migration

{

    /**

     * Run the migrations.

     *

     * @return void

     */

    public function up()

    {

        Schema::create('users', function (Blueprint $table) {

            $table->bigIncrements('id');

            $table->string('name');

            $table->string('email');

            $table->string('username')->nullable();

            $table->timestamp('email_verified_at')->nullable();

            $table->boolean('is_admin')->nullable();

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

        Schema::dropIfExists('users');

    }

}
```
#### Step 6: Run Migrations
Generated the authentication scaffolding, run the following command to create the necessary tables in the database:

```
php artisan migrate
```
#### Step 6: Modify the AuthenticatedSessionController.php

Now modify the `store()` method located in AuthenticatedSessionController.php file in 
`app\Http\Controller\Auth\AuthenticatedSessionController.php` like the code below: 

```
    public function store(LoginRequest $request)
    {
        $field = filter_var($request->input('email'), FILTER_VALIDATE_EMAIL) ? 'email' : 'username';

        $request->merge([$field => $request->input('email')]);

        $request->authenticate();

        $request->session()->regenerate();

        if(Auth::user()->user_role == 'IsValidAdmin'){
            return redirect()->intended(RouteServiceProvider::ISADMIN);
        }elseif(Auth::user()->user_role == 'IsValidUser'){
            return redirect()->intended(RouteServiceProvider::HOME);
        }
        return redirect()->intended(RouteServiceProvider::ISSUPERADMIN);
        
    }
```
you can read more about the `FILTER_VALIDATE_EMAIL` at [PHP Documentation](https://www.php.net/manual/en/filter.filters.validate.php)

#### Step 7: Lastly make few modification to authenticate() method:

Now modify the `authenticate()` method located in AuthenticatedSessionController.php file in 
`app\Http\Requests\Auth\LoginRequest.php` like the code below: 

```
public function authenticate()
    {
        $this->ensureIsNotRateLimited();

        if ($this->has(['username'])) {
           if (! Auth::attempt($this->only('username', 'password'), $this->boolean('remember'))) {
            RateLimiter::hit($this->throttleKey());

            throw ValidationException::withMessages([
                'email' => trans('auth.failed'),
            ]);
        }
        }else{
            if (! Auth::attempt($this->only('email', 'password'), $this->boolean('remember'))) {
                RateLimiter::hit($this->throttleKey());
    
                throw ValidationException::withMessages([
                    'email' => trans('auth.failed'),
                ]);
            }
        }

        RateLimiter::clear($this->throttleKey());
    }
```

In the above code we are looking are the incoming request if it contains either username or email fields in our request.


You can add some dummy records on your users table.
Now you can run your project.
You will get layout of login page like as bellow:

| ![space-1.jpg](/img/post/laravel-10.png) | 
|:--:| 
| *share my created login screen.* |


I hope it can help you...