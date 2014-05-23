# Installation

- [Install Composer](#install-composer)
- [Install Laravel](#install-laravel)
- [Server Requirements](#server-requirements)
- [Configuration](#configuration)
- [URL လွလွေလးလိုခ်င္တယ္](#pretty-urls)

<a name="install-composer"></a>
## Install Composer

Laravel ရဲ႕အသံုးဝင္တဲ႕tool .... [Composer](http://getcomposer.org), သူ႕ရဲ႕ depenedencies ေတြကို Manage လုပ္ဖို႕။ ပထမဆံုး `composer.phar` copy ကိုိ download လုပ္လိုက္ပါ။ download လုပ္ၿပီးသြားၿပီဆိုရင္ သင္႕မွာ PHAR ဆိုတဲ႕file ေလးရွိသြားပါၿပီ၊ အဲဒီ႕ file ကိုသင္႕ရဲ႕local project မွာဒီတိုင္းထားခ်င္ရင္လည္းရပါတယ္ တကယ္လို႕သင္က `usr/local/bin` ထဲကိုေရႊ႕ၿပီးေတာ႕သင္႕ရဲ႕  System အတြက္ Global လုပ္မယ္ဆိုလည္းလုပ္ႏိုင္ပါတယ္။ Window မွာဆိုရင္ေတာ႕ [Windows installer](https://getcomposer.org/Composer-Setup.exe) ကိုသံုးၿပီး install လုပ္ႏိုင္ပါတယ္။

<a name="install-laravel"></a>
## Install Laravel

### Laravel Installer မွတစ္ဆင့္

ပထမဆံုး[Laravel installer PHAR archive](http://laravel.com/laravel.phar) ကို  download လုပ္ပါ၊ install လုပ္ရာမွာလြယ္ကူေအာင္လို႕ file name ကို `laravel` လို႕ေျပာင္းလိုက္ပါ၊ ေျပာင္းၿပီးသြားရင္အဲ႕ဒီ႕ File ကို  `/usr/local/bin` ထဲကိုေရႊ႕လိုက္ပါ။ Laravel ကို Install လုပ္မယ္ဆိုရင္ `laravel new` ဆိုၿပီး command line ကေန run လိုက္ရင္ Laravel Framework တစ္ခုကိုကိုယ္ႀကိဳက္တဲ႕ေနရာမွာ Install လုပ္ႏိုင္ပါၿပီ။ `laravel new blog` ဆိုၿပီး command line ကေန run လိုက္ရင္ blog ဆိုတဲ႕အမည္နဲ႕ command line ကေနကိုယ္ create လုပ္ခ်င္တဲ႕ေနရာမွာ Laravel Framework အသစ္တစ္ခုကို install လုပ္ေပးမွာျဖစ္ပါတယ္။ ဒီနည္းက composer ကေန download လုပ္တာထက္ပိုျမန္ပါတယ္။

သင္႕အေနနဲ႕ Laravel ကို Composer ကေနတစ္ဆင္႕ `create-project`  command သံုးၿပီးေတာ႕လည္း install လုပ္ႏိုင္ပါတယ္၊ terminal မွာ ေအာက္မွာေရးထားတဲ႕ command ကို run ၿပီးေတာ႕လည္း install လုပ္ႏိုင္ပါတယ္

	composer create-project laravel/laravel --prefer-dist

### Download မွတစ္ဆင္႕

Composer ကို install လုပ္ၿပီးသြားၿပီဆိုရင္ Laravel Framework [latest version](https://github.com/laravel/laravel/archive/master.zip) ကို download လုပ္လိုက္ပါ၊  သင္႕ရဲ႕ web server ထဲမွာ  zip ကို extra လုပ္လိုက္ပါ၊ extra လုပ္ထားတဲ႕  framework folder ထဲကို command line ကဝင္ၿပီးေတာ႕  `php composer.phar install` (or `composer install`) ဆိုၿပီး run လိုက္ပါ။ ဒီ command က framework ရဲ႕ dependencies ေတြကို install လုပ္ခိုင္းလိုက္တာပါ။ ဒီ installation လုပ္တဲ႕ေနရာမွာ webserver မွာ git install လုပ္ထားမွ successfully complete ျဖစ္မွာပါ။

တကယ္လို႕သင္ Framework ကို update လုပ္ခ်င္တယ္ဆိုရင္`php composer.phar update` command ကို run ေပးရပါ႕မယ္။

<a name="server-requirements"></a>
## Server Requirements
Laravel Framework မွာ system requirements တစ္ခ်ိဳ႕ရွိပါတယ္။ ဘာေတြလည္းဆိုရင္

- PHP >= 5.3.7
- MCrypt PHP Extension

တို႕ဘဲျဖစ္ပါတယ္။

PHP 5.5 မွာ တစ္ခ်ိဳ႔ OS ေတြက PHP JSON extension ကို manullly install လုပ္ေပးရပါတယ္။ တကယ္လို႕ Ubuntu သံုးတယ္ဆိုရင္ `apt-get install php5-json` ဆိုၿပီး terminal ကေန run လိုက္တာနဲ႕အဆင္ေျပပါတယ္။

<a name="configuration"></a>
## Configuration

Laravel က configuration ဆိုတာမရွိသေလာက္ပါဘဲ။ သင္စၿပီး develop ဖို႕ရာအဆင္သင္႕ပါဘဲ။ဘယ္လိုဘဲေျပာေျပာ သင္႕အေနနဲ႕ `app/config/app.php` file နဲ႕သူ႕ရဲ႕ Documencation ကိုျပန္ၾကည္႕ခ်င္မွာပါဘဲ။ `app/config/app.php`မွာဘာေတြပါသလဲဆိုရင္ေတာ႕ `timezone` ေနာက္ `locale`တို႕ပါပါတယ္၊သင္႕ရဲ႕ application နဲ႕အဆင္ေျပမယ္႕ configure လုပ္ႏိုင္ပါတယ္။

Laravel တစ္ခါ Install လုပ္တိုင္း [သင္႕ရဲ႕ local environmet](/docs/configuration#environment-configuration) ကို Configure ျပန္လုပ္သင္႕ပါတယ္။ local machine မွာ     develop လုပ္တဲ႕အခါ erros ကိုျမင္ရမယ္။ မူလကေတာ႕ error reporting က သင္႕ရဲ႕ development production မွာ disable လုပ္ထားပါတယ္။

> **မွတ္ခ်က္:** `app.debug` ကို production မွာဘယ္ေတာ႕မွ true မေပးသင္႕ပါဘူး။ဘယ္ေတာ႕မွ မလုပ္ပါနဲ႕။

<a name="permissions"></a>
### Permissions

Laravel က   `app/storage` ကို web server အတြက္ permission write ေပးရပါမယ္။

<a name="paths"></a>
### လမ္းေၾကာင္းမ်ား

Framework ရဲ႕ လမ္းေၾကာင္းေတြကေျပာင္းလဲႏိုင္ပါတယ္၊ ဒီ location ေတြကိုေျပာင္းခ်င္တယ္ဆိုရင္ `bootstrap/paths.php` မွာၾကည္႕ရွူေျပာင္းလည္းႏိုင္ပါတယ္။

<a name="pretty-urls"></a>
## Pretty URLs

### Apache

Framework ထဲက `public/.htaccess` ကို URL မွာ `index.php` မပါေအာင္ေဖ်ာက္ထားေပးမွာျဖစ္ပါတယ္။ တကယ္လို႕သင္႕ ရဲ႕ Laravel application က Apache ကိုသံုးတယ္ဆိုရင္  `mod_rewrite` ကို enable လုပ္ဖို႕မေမ႕ပါနဲ႕ဦး။

တကယ္လို႕ `.htaccess`file က သင္႕ Application မွာအလုပ္မလုပ္ဘူးဆိုရင္ ေအာက္ကတစ္ခုကိုစမ္းၾကည္႕လိုက္ပါ:

	Options +FollowSymLinks
	RewriteEngine On

	RewriteCond %{REQUEST_FILENAME} !-d
	RewriteCond %{REQUEST_FILENAME} !-f
	RewriteRule ^ index.php [L]

### Nginx

Nginx မွာဆိုရင္ေအာက္ကညႊန္ၾကားခ်က္ကို လိုက္လုပ္လိုက္တာနဲ႕URL လွလွေလးေတြရပါတယ္

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }