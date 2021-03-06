﻿# Laravel Quickstart

- [Installation](#installation)
- [Routing](#routing)
- [Creating A View](#creating-a-view)
- [Creating A Migration](#creating-a-migration)
- [Eloquent ORM](#eloquent-orm)
- [Displaying Data](#displaying-data)

<a name="installation"></a>
## Installation

### Laravel Installer ကုိ အသုံးျပဳျခင္း

ေရွးဦးစြာ [Laravel installer PHAR archive](http://laravel.com/laravel.phar) ကုိ ေဒါင္းပါ။  အဆင္ေျပေစရန္အတြက္ ထုိ  file ကုိ `laravel` ဟု အမည္ေပးျပီး `/usr/local/bin` ထဲသုိ ့ေျပာင္းေရြ  ့လုိက္ပါ။ ထုိေနာက္ `laravel new` command ျဖင့္ သင္ထားရွိထားေသာ directory ေပၚတြင္ laravel installation အလုိအေလ်ာက္ ျပလုပ္သြားမည္ ျဖစ္သည္။  ဥပမာ `laravel new blog` ဆုိသည့္ command ကုိအသုံးျပပါက `blog` အမည္ရွိ folder တစ္ခုကုိ တည္ေဆာက္ေပးျပီး လုိအပ္သည့္ package မ်ားကိုပါ တခါတည္း ေဒါင္းလုပ္လုပ္ကာ စုစည္းေပးသြားမည္ ျဖစ္သည္။ ၄င္းသုိ ့ install ျပဳလုပ္ျခင္းသည္ Composer မွ install လုပ္ျခင္းထက္ ပုိ၍ လ်င္ျမန္ပါလိမ့္မည္။

### Composer ကို အသုံးျပဳျခင္း

Laravel framework ကုိ [Composer](http://getcomposer.org) မွလည္း installation ႏွင့္ လုိအပ္သည့္ package မ်ားကုိ ထည့္သြင္းႏုိင္သည္။ Composer မသြင္းရေသးပါက  [Composer ထည့္သြင္းျခင္းနည္းလမ္း](http://getcomposer.org/doc/00-intro.md) ကုိၾကည့္၍ ထည့္သြင္းႏုိင္ပါသည္။

ထုိေနာက္ သင့္အေနျဖင့္ terminal မွ ေအာက္ပါ command ကုိ ရုိက္သြင္းျခင္းျဖင့္ Laravel ကုိ install ျပဳလုပ္ႏုိင္မည္ ျဖစ္သည္။

	composer create-project laravel/laravel your-project-name --prefer-dist

၄င္း command မွ laravel အသစ္စက္စက္ ကုိ သင့္`your-project-name` folder အတြင္းတြင္ တည္ရွိေနမည္ကို ေတြ ့ရပါမည္။

ထုိတင္မက သင့္ အေနျဖင့္ [Laravel repository from Github](https://github.com/laravel/laravel/archive/master.zip) မွ ေဒါင္းေလာ့ ျပဳလုပ္ျပီး directory ထဲတြင္ `composer install` run ၍လည္း install ျပဳလုပ္ႏုိင္ပါသည္။ ထုိ command မွ framework တြင္ လုိအပ္ေသာ package မ်ားကုိ အလုိအေလ်ာက္ download ျပဳလုပ္ျပီး install သြားမည္ ျဖစ္သည္။

### Permissions

Laravel ကုိ install ျပဳလုပ္ျပီးပါက သင့္အေနျဖင့္ web server ၏ write permission ျဖင့္ပတ္သတ္၍ `app/storage` ထဲတြင္ ျပင္ဆင္ရန္ လုိအပ္ေကာင္း လုိအပ္ေပမည္။ အေသးစိတ္ အခ်က္အလက္ကုိ  [Installation](/docs/installation) တြင္ ၾကည့္ရႈႏုိင္ပါသည္။

### Serving Laravel

အၾကမ္းအားျဖင့္ Apache သုိ ့မဟုတ္ Nginx ေပၚတြင္ laravel application ကုိ တင္ထားႏုိင္သည္။  သင့္ အသုံးျပဳေသာ PHP version မွာ 5.4 အထက္ျဖစ္ျပီး PHP တြင္ပါဝင္ေသာ default server ကုိ အသုံးျပဳလုိပါက သင့္အေနျဖင့္ Artisan command ျဖစ္သည့္ `serve` ကုိ အသုံးျပဳႏုိင္သည္။

	php artisan serve

<a name="directories"></a>
### Directory Structure

Framework ကုိ install ျပဳလုပ္ျပီးေနာက္ သင့္ အေနျဖင့္ directory structure ျဖင့္ ရင္းႏွီးေနရန္ လုိေပမည္။ `app` directory ထဲတြင္ `views`, `controllers`, and `models` အစရွိသည့္ folder မ်ား တည္ရွိေနသည္ကုိ ေတြ ့ ရမည္ ျဖစ္သည္။ သင့္ application ၏ code မ်ားကုိ ထုိထဲတြင္ ေရးသားရမည္ ျဖစ္သည္။ သင့္အေနျဖင့္ လုိအပ္မည့္ configuration ႏွင့္ ပတ္သတ္၍ `app/config` အမည္ရွိ directory ထဲတြင္ၾကည့္ရႈရမည္ ျဖစ္သည္။

<a name="routing"></a>
## Routing

ေရွးဦးစြာ Route တစ္ခုကို တည္ေဆာက္ၾကပါစို ့။  Laravel တြင္ အရုိးရွင္းဆုံး route မွာ route to Closure ျဖစ္သည္။ `app/routes.php` ကုိဖြင့္ျပီး ေအာက္ပါ code ကုိထည့္သြင္းၾကည့္ပါ။ 

	Route::get('users', function()
	{
		return 'Users!';
	});

ထုိေနာက္ web browser ေပၚတြင္ `/users` ဟူေသာ route ျဖင့္ စမ္းၾကည့္ပါက သင့္အေနျဖင့္ `Users!` တုံ ့ျပန္သည္ကို ျမင္ေတြ ့ရမည္ ျဖစ္သည္။ 
ေကာင္းေလစြ! သင့္အေနျဖင့္ ပထမဦးစြာ route တစ္ခုကို ဖန္တီးလုိက္ျပီ ျဖစ္သည္။


Route မ်ားမွာ controller မ်ားႏွင့္လည္း ခ်ိတ္ဆက္ အလုပ္လုပ္ႏိုင္သည္။ ဥပမာ

	Route::get('users', 'UserController@getIndex');

အဆုိပါ route တြင္ 	`/users` ဟုေခၚယူလုိက္ပါက `UserController` class အတြင္းရွိ `getIndex` method  ကုိ အလုပ္လုပ္မည္ ျဖစ္သည္။ Controller routing ႏွင့္ ပတ္သတ္၍ အေသးစိတ္ကုိ [controller documentation](/docs/controllers) တြင္ၾကည့္ရႈႏုိင္သည္။

<a name="creating-a-view"></a>
## View တစ္ခု တည္ေဆာက္ျခင္း

ထုိေနာက္ user data မ်ားကို ေဖာ္ျပရန္ ရုိးရွင္းသည့္ view တစ္ခုကို တည္ေဆာက္ရန္ လုိေပမည္။  view file မ်ားသည္ `app/views` directory  ထဲတြင္ တည္ရွိမည္ ျဖစ္သည္။  View တြင္ သင့္ application တြင္ ေဖာ္ျပလုိသည့္  HTML ျဖင့္ ေဖာ္ျပသြားမည္ ျဖစ္သည္။  `layout.blade.php` ႏွင့္ `users.blade.php` ဟု၍ file ႏွစ္ခုကို တည္ေဆာက္လုိက္ပါ။ `layout.blade.php` ဟုသည့္ file တြင္ ေအာက္ပါ အတုိင္း ေရးသားလုိက္ပါ။

	<html>
		<body>
			<h1>Laravel Quickstart</h1>

			@yield('content')
		</body>
	</html>

Next, we'll create our `users.blade.php` view:

	@extends('layout')

	@section('content')
		Users!
	@stop

Some of this syntax probably looks quite strange to you. That's because we're using Laravel's templating system: Blade. Blade is very fast, because it is simply a handful of regular expressions that are run against your templates to compile them to pure PHP. Blade provides powerful functionality like template inheritance, as well as some syntax sugar on typical PHP control structures such as `if` and `for`. Check out the [Blade documentation](/docs/templates) for more details.

Now that we have our views, let's return it from our `/users` route. Instead of returning `Users!` from the route, return the view instead:

	Route::get('users', function()
	{
		return View::make('users');
	});

Wonderful! Now you have setup a simple view that extends a layout. Next, let's start working on our database layer.

<a name="creating-a-migration"></a>
## Creating A Migration

To create a table to hold our data, we'll use the Laravel migration system. Migrations let you expressively define modifications to your database, and easily share them with the rest of your team.

First, let's configure a database connection. You may configure all of your database connections from the `app/config/database.php` file. By default, Laravel is configured to use MySQL, and you will need to supply connection credentials within the database configuration file. If you wish, you may change the `driver` option to `sqlite` and it will use the SQLite database included in the `app/database` directory.

Next, to create the migration, we'll use the [Artisan CLI](/docs/artisan). From the root of your project, run the following from your terminal:

	php artisan migrate:make create_users_table

Next, find the generated migration file in the `app/database/migrations` folder. This file contains a class with two methods: `up` and `down`. In the `up` method, you should make the desired changes to your database tables, and in the `down` method you simply reverse them.

Let's define a migration that looks like this:

	public function up()
	{
		Schema::create('users', function($table)
		{
			$table->increments('id');
			$table->string('email')->unique();
			$table->string('name');
			$table->timestamps();
		});
	}

	public function down()
	{
		Schema::drop('users');
	}

Next, we can run our migrations from our terminal using the `migrate` command. Simply execute this command from the root of your project:

	php artisan migrate

If you wish to rollback a migration, you may issue the `migrate:rollback` command. Now that we have a database table, let's start pulling some data!

<a name="eloquent-orm"></a>
## Eloquent ORM

Laravel ships with a superb ORM: Eloquent. If you have used the Ruby on Rails framework, you will find Eloquent familiar, as it follows the ActiveRecord ORM style of database interaction.

First, let's define a model. An Eloquent model can be used to query an associated database table, as well as represent a given row within that table. Don't worry, it will all make sense soon! Models are typically stored in the `app/models` directory. Let's define a `User.php` model in that directory like so:

	class User extends Eloquent {}

Note that we do not have to tell Eloquent which table to use. Eloquent has a variety of conventions, one of which is to use the plural form of the model name as the model's database table. Convenient!

Using your preferred database administration tool, insert a few rows into your `users` table, and we'll use Eloquent to retrieve them and pass them to our view.

Now let's modify our `/users` route to look like this:

	Route::get('users', function()
	{
		$users = User::all();

		return View::make('users')->with('users', $users);
	});

Let's walk through this route. First, the `all` method on the `User` model will retrieve all of the rows in the `users` table. Next, we're passing these records to the view via the `with` method. The `with` method accepts a key and a value, and is used to make a piece of data available to a view.

Awesome. Now we're ready to display the users in our view!

<a name="displaying-data"></a>
## Displaying Data

Now that we have made the `users` available to our view, we can display them like so:

	@extends('layout')

	@section('content')
		@foreach($users as $user)
			<p>{{ $user->name }}</p>
		@endforeach
	@stop

You may be wondering where to find our `echo` statements. When using Blade, you may echo data by surrounding it with double curly braces. It's a cinch. Now, you should be able to hit the `/users` route and see the names of your users displayed in the response.

This is just the beginning. In this tutorial, you've seen the very basics of Laravel, but there are so many more exciting things to learn. Keep reading through the documentation and dig deeper into the powerful features available to you in [Eloquent](/docs/eloquent) and [Blade](/docs/templates). Or, maybe you're more interested in [Queues](/docs/queues) and [Unit Testing](/docs/testing). Then again, maybe you want to flex your architecture muscles with the [IoC Container](/docs/ioc). The choice is yours!
