z# Artisan CLI

- [Introduction](#introduction)
- [အသုုံးျပဳပုုံ](#အသုုံးျပဳပုုံ)

<a name="introduction"></a>
## Introduction

Artisan is the name of the command-line interface included with Laravel. It provides a number of helpful commands for your use while developing your application. It is driven by the powerful Symfony Console component.

<a name="usage"></a>
## အသုုံးျပဳပုုံ

#### အသုုံးျပဳႏုုိင္သည့္ Command မ်ားကုုိ စီရီျပသျခင္း

Artisan တြင္ပါဝင္သည့္ Command အကုုန္လုုံးကုုိ list အေနျဖင့္ ျပသလုုိပါက `list` ဟုုသည့္ command ကုုိ အသုုံးျပဳႏုုိင္သည္။

	php artisan list

#### Command  တစ္ခုုခ်င္း၏ အသုုံးျပဳျခင္း လမ္းညြန္မႈကုုိ ၾကည့္ရႈျခင္း 

Command တုုိင္းလုုိလုုိ တြင္ “help” ဟုု အပုုိေဆာင္း ရုုိက္ျခင္း ျဖင့္ မိမိတုုိ ့ အသုုံးျပဳမည့္ Command တြင္ ထည့္သြင္းရမည့္ arguments မ်ားႏွင့္ ေရြးခ်ယ္စရာမ်ားကုုိ သိရွိႏုုိင္ပါသည္။

	php artisan help migrate

#### Configuration Environment ကုုိ သတ္မွတ္ျခင္း

မိမိတုုိ ့ အသုုံးျပဳလုုိသည္ Configuration Environment ကုုိ —env ဟုုေသာ  switch ျဖင့္ ေရြးခ်ယ္သတ္မွတ္ႏုုိင္သည္။ 


	php artisan migrate --env=local

#### လက္ရွိ အသုုံးျပဳေနသည့္ Laravel version ကိုုေဖာ္ျပျခင္း

မိမိတုုိ ့လက္ရွိအသုုံးျပဳေနသည့္ Laravel version ကုုိ သိရွိလုုိပါက —switch ကုုိ အသုုံးျပဳျပီး  သိရွိႏုုိင္ပါသည္။ 
 

	php artisan --version
