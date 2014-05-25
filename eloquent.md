# Eloquent ORM

- [အၾကမ္းဖ်င္း](#အၾကမ္းဖ်င္း)
- [အေျခခံအသုုံးျပဳပုုံ](#အေျခခံအသုုံးျပဳပုုံ)
- [Mass Assignment](#mass-assignment)
- [Insert, Update, Delete](#insert-update-delete)
- [Soft Deleting](#soft-deleting)
- [Timestamps](#timestamps)
- [Query Scopes](#query-scopes)
- [Relationships](#relationships)
- [Querying Relations](#querying-relations)
- [Eager Loading](#eager-loading)
- [Inserting Related Models](#inserting-related-models)
- [Touching Parent Timestamps](#touching-parent-timestamps)
- [Working With Pivot Tables](#working-with-pivot-tables)
- [Collections](#collections)
- [Accessors & Mutators](#accessors-and-mutators)
- [Date Mutators](#date-mutators)
- [Model Events](#model-events)
- [Model Observers](#model-observers)
- [Converting To Arrays / JSON](#converting-to-arrays-or-json)

<a name="introduction"></a>
## အၾကမ္းဖ်င္း

Laravel တြင္ပါဝင္သည့္ ရုုိးရွင္းျပီး လွပသပ္ရပ္ေသာ Eloquent ORM သည္  သင့္ Database ကုုိ ActiveRecord ျဖင့္ အေျခခံထား သျဖင့္ အလြယ္တကူပင္ အသုုံးျပဳႏုုိင္မည္ ျဖစ္သည္။ Database မွ Table တစ္ခုုတုုိင္းကုုိ Model တစ္ခုု အေနျဖင့္ သတ္မွတ္ကာ အသုုံးျပဳရမည္ ျဖစ္သည္။ 

အသုုံးမျပဳခင္ ပထမဆုုံး အေနျဖင့္ `app/config/database.php` သုုိ ့သြားေရာက္ကာ ၾကိဳတင္ ျပင္ဆင္ရမည္ ျဖစ္သည္။ 

<a name="basic-usage"></a>
## အေျခခံအသုုံးျပဳပုုံ

စတင္ အသုုံးျပဳရန္ Eloquent model တစ္ခုုကိုု တည္ေဆာက္ရမည္ ျဖစ္သည္။ ပုုံမွန္အားျဖင့္ Models file မ်ားမွာ `app/models` အမည္ရွိသည့္ Folder ထဲတြင္ တည္ရွိမည္ ျဖစ္ေသာ္လည္း အလ်ဥ္းသင့္သလုုိ ျပင္ဆင္ႏုုိင္မည္ျဖစ္သည္။ ထုုိသုုိ ့ျပင္ဆင္ႏုုိင္ရန္ အတြက္ `composer.json` ထဲတြင္ မိမိတုုိ ့  autoload လုုပ္ခ်င္သည့္ file ၏ အမည္ႏွင့္ တည္ေနရာကိုု ထည့္သြင္းထားရမည္ ျဖစ္သည္။ 


#### Eloquent Model တစ္ခုု Define ျပဳလုုပ္ျခင္း

class User extends Eloquent {}

Eloquent Model တြင္ မည့္သည့္ table ကုုိ အသုုံးျပဳမည္ကုုိ မေၾကညာ ထားပါက Model အမည္၏ အမ်ားကိန္း ကုုိ အသုုံးျပဳမည္ ျဖစ္သည္။ ဥပမာ User.php ဟုု ေၾကညာထားပါက Users table ဟုု အလုုိအေလ်ာက္ သတ္မွတ္မည္ ျဖစ္သည္။ သုုိ ့မဟုုတ္ပဲ မိမိ စိတ္ၾကိဳက္ အသုုံးျပဳလုုိပါက ေအာက္ပါ အတုုိင္း သတ္မွတ္ႏုုိင္မည္ ျဖစ္သည္။ 

class User extends Eloquent {

protected $table = 'my_users';

}

> **မွတ္ခ်က္:** Eloquent အေနျဖင့္ Primary Key column ဟုု `id` ဟုု အလုုိအေလ်ာက္ သတ္မွတ္ျဖစ္ေသာ္လည္း အထက္က ကဲ့သုုိ ့ပင္ မိမိစိတ္ၾကိဳက္ column ကုုိ သတ္မွတ္ႏုုိင္သည္။ ထုုိကဲ့သုုိ ့ Database Connection ကုုိ `connection` ဟုုသည္ property ကုုိ အသုုံးျပဳ ထပ္မံ သတ္မွတ္ႏုုိင္မည္ ျဖစ္သည္။ 

Model ကုုိ သတ္မွတ္ျပီးသည္ႏွင့္ မိမိတုုိ ့ အလုုိရွိသည့္ record မ်ားကုုိ စတင္ တည္ေဆာက္ျခင္း ၊ ထုုတ္ယူျခင္းမ်ား ျပဳလုုပ္ႏုုိင္ျပီ ျဖစ္သည္။  သတိျပဳရမည့္ တစ္ခ်က္မွာ `updated_at` ႏွင့္ `created_at` ဆုုိသည့္ columns မ်ားမွာ သင့္ table တြင္ အလုုိအေလ်ာက္ ပါဝင္မည္ျဖစ္သည္။ သင့္ အေနျဖင့္ အလုုိမရွိပါက model အတြင္းရွိ `$timestamps`ဟုုသည္ property ကုုိ `false` ဟုု ေပးထားရန္ လုုိေပမည္။

#### Model အတြင္းမွ record အားလုုံး ထုုတ္ယူျခင္း

$users = User::all();

#### Model အတြင္း record မ်ားအား primary key ကုုိ အသုုံးျပဳကာ ထုုတ္ယူျခင္း

$user = User::find(1);

var_dump($user->name);

> **Note:**  [query builder] တြင္ အသုုံးျပဳႏုုိင္သည့္ method မ်ား အားလုုံး (/docs/queries) Eloquent models တြင္လည္း ဆက္လက္ အသုုံးျပဳႏုုိင္မည္ ျဖစ္သည္။ 

#### Model အတြင္း record မ်ားအား primary key ကုုိ အသုုံးျပဳကာ ထုုတ္ယူျပီး မရွိပါက Exception ျဖင့္ ျပသျခင္း

တခါတရံ သင့္ အေနျဖင့္ Model မွ data မ်ား ရွာမေတြ ့ပါက Exception အေနျဖင့္ ျပသခ်င္မည္ ျဖစ္သည္။ ထုုိသုုိ ့ ျပဳလုုပ္ႏဳိင္ရန္ `App::error` ဟုုေသာ handler ကုုိ အသုုံးျပဳျပီး 404 page ကုုိ လြဲေျပာင္းျပသႏုုိင္မည္ ျဖစ္သည္။

$model = User::findOrFail(1);

$model = User::where('votes', '>', 100)->firstOrFail();

To register the error handler, listen for the `ModelNotFoundException`

use Illuminate\Database\Eloquent\ModelNotFoundException;

App::error(function(ModelNotFoundException $e)
{
return Response::make('Not Found', 404);
});

#### Querying Using Eloquent Models ကုုိ အသုုံးျပဳကာ Query မ်ားေရးသားျခင္း

$users = User::where('votes', '>', 100)->take(10)->get();

foreach ($users as $user)
{
var_dump($user->name);
}

#### Eloquent ကို ေပါင္းစပ္ အသုုံးျပဳျခင္း 


သင့္အေနျဖင့္  Query Builder function မ်ားျဖင့္ Eloquent ကို ေပါင္းစပ္ အသုုံးျပဳႏုုိင္သည္။

$count = User::where('votes', '>', 100)->count();


If you are unable to generate the query you need via the fluent interface, feel free to use `whereRaw`:

$users = User::whereRaw('age > ? and votes = 100', array(25))->get();

#### Results မ်ားကုိ ခြဲထုတ္ျခင္း

သင့္အေနျဖင့္ ေထာင္ေပါင္းမ်ားစြာေသာ Eloquent records မ်ားကို ထုတ္ယူလုိပါက  `chunk` ဟုေသာ method ကို အသုံးျပဳ၍ Memory အသုံးျပဳမႈကုိ ေလ်ာ့ခ်ႏုိင္ပါသည္။ 


User::chunk(200, function($users)
{
foreach ($users as $user)
{
//
}
});

ပထမဆုံး argument   အေနျဖင့္ မိမိတုိ ့ ပုိင္းထုတ္လုိသည့္ အေရအတြက္ကုိ ထည့္သြင္း ေပးရမည္ ျဖစ္သည္။ ဒုတိယ argument အေနျဖင့္ closure ပါဝင္မည္ျဖစ္ျပီး ထုိထဲတြင္ ထြက္ေပၚလာေသာ record တုိင္းတြင္ ျဖစ္ေပၚေစလုိသည့္  Instruction မ်ား ေရးသားႏုိင္သည္။ 

#### Query Connection သတ္မွတ္အသုံးျပဳျခင္း

မိမိတုိ ့ အသုံးျပဳလုိသည္ Database connection အေပၚမူတည္၍ `on` method ကုိ အသုံးျပဳကာ ေျပာင္းလဲ အသုံးျပဳႏုိင္ပါသည္။

$user = User::on('connection-name')->find(1);

<a name="mass-assignment"></a>
## အေျမာက္အမ်ား ထည့္သြင္းျခင္း


Model အသစ္ကို တည္ေဆာက္ျပီးပါက Constructor အေနျဖင့္ ပါဝင္မည့္ attribute မ်ားကုိ array အေနျဖင့္ ထည့္သြင္းႏုိင္ပါသည္။  
ထုိကဲ့သုိ ့ attribute မ်ား ကုိ Model မ်ားမွ တဆင့္ အေျမာက္အမ်ား ထည့္သြင္းႏုိင္ျခင္းသည္ အဆင္ေျပေသာ္လည္း User Input ကို မစစ္မေဆးပဲ အေျမာက္အမ်ားထည့္သြင္းပါက လုံျခဳံေရး ဆုိင္ရာ **ျပႆနာ** မ်ားရွိႏုိင္ပါသည္။ ထုိေၾကာင့္ default အေနျဖင့္ Eloquent Model မ်ားအားလုံးတြင္ ထုိသုိ ့
ျပဳလုပ္ျခင္းကုိ ဖြင့္မေပးထားပါ။ သုိ ့ေသာ္ ထုိ ့သုိ ့ျပဳလုပ္ခ်င္ပါက `fillable` သုိ ့မဟုတ္ `guarded`  အစရွိသည့္ attribute မ်ားကုိ သတ္မွတ္ထားရန္ လုိေပမည္။

#### Defining Fillable Attributes On A Model

The `fillable` property specifies which attributes should be mass-assignable. This can be set at the class or instance level.

class User extends Eloquent {

protected $fillable = array('first_name', 'last_name', 'email');

}

အထက္က ဥပမာတြင္ array တြင္ထည့္သြင္းထားသည့္ attribute မ်ားသည္ အေျမာက္အမ်ား ထည့္သြင္းႏုိင္သည္။

#### Model တြင္ တားျမစ္ attribute မ်ားအား သတ္မွတ္ျခင္း


`fillable` ၏ ေျပာင္းျပန္မွာ `guarded` ျဖစ္ျပီၤး phone တစ္လုံး၏  "black-list" ကဲ့သုိ ့ အလုပ္လုပ္သည္။

class User extends Eloquent {

protected $guarded = array('id', 'password');

}

> **Note:** When using `guarded`, you should still never pass `Input::get()` or any raw array of user controlled input into a `save` or `update` method, as any column that is not guarded may be updated.

#### အေျမာက္အမ်ား ထည့္သြင္းျခင္းမွ တားျမစ္ျခင္း

အေပၚမွ ဥပမာတြင္ `id` ႏွင့္ `password` field မ်ားမွာ အေျမာက္အမ်ား ထည့္သြင္းႏုိင္မည္ မဟုတ္ေပ။ အျခား attribute မ်ားမွာမူ အေျမာက္အမ်ား ထည့္သြင္းႏုိင္မည္ ျဖစ္သည္။ အကယ္၏ field အားလုံးကို တားျမစ္လုိပါက 

protected $guarded = array('*');

<a name="insert-update-delete"></a>
## ထည့္သြင္း ၊ ျပင္ဆင္ ၊ ဖ်က္ပစ္

Model မွ record အသစ္ကုိ တည္ေဆာက္လုိပါက model instance တစ္ခုကို တည္ေဆာက္ျပီး  `save` method ကို အသုံးျပဳႏုိင္သည္။


#### Model တြင္ record မ်ား ထည့္သြင္းျခင္း

$user = new User;

$user->name = 'John';

$user->save();

> **Note:** Typically, your Eloquent models will have auto-incrementing keys. However, if you wish to specify your own keys, set the `incrementing` property on your model to `false`.

You may also use the `create` method to save a new model in a single line. The inserted model instance will be returned to you from the method. However, before doing so, you will need to specify either a `fillable` or `guarded` attribute on the model, as all Eloquent models protect against mass-assignment.

After saving or creating a new model that uses auto-incrementing IDs, you may retrieve the ID by accessing the object's `id` attribute:

$insertedId = $user->id;

#### Setting The Guarded Attributes On The Model

class User extends Eloquent {

protected $guarded = array('id', 'account_id');

}

#### Using The Model Create Method

// Create a new user in the database...
$user = User::create(array('name' => 'John'));

// Retrieve the user by the attributes, or create it if it doesn't exist...
$user = User::firstOrCreate(array('name' => 'John'));

// Retrieve the user by the attributes, or instantiate a new instance...
$user = User::firstOrNew(array('name' => 'John'));

#### Model တစ္ခုအား Update ျပဳလုပ္ျခင္း

Model အား update ျပဳလုပ္လုိပါက ေရွးဦးစြာ ျပဳလုပ္လုိသည္ record ကုိ retrieve ျပဳလုပ္ရပါမည္။ ထုိေနာက္ attribute အား မိမိတို ့ထည့္သြင္းလုိသည့္ႏွင့္
ေျပာင္းလဲ သတ္မွတ္ျပီး `save` method ကို အသုံးျပဳကာ update ျပဳလုပ္ႏုိင္ပါသည္။

$user = User::find(1);

$user->email = 'john@foo.com';

$user->save();

#### Model ႏွင့္ ၄င္း၏ Relationship မ်ားတြင္ save ျပဳလုပ္ျခင္း

တခါတရံ  သင့္အေနျဖင့္ လက္ရွိ အသုံးျပဳေနသည့္ model တြင္သာ မက ၄င္းႏွင့္ relationship ျပဳလုပ္ထားေသာ Model မ်ားတြင္ပါ save လုပ္လုိသည့္ အခါမ်ားရွိေပမည္။ ထုိသုိ ့ ျပဳလုပ္လုိပါက `push` method ကုိ အသုံးျပဳႏုိင္သည္။ 

$user->push();


You may also run updates as queries against a set of models:

$affectedRows = User::where('votes', '>', 100)->update(array('status' => 2));

> **Note:** No model events are fired when updating a set of models via the Eloquent query builder.

#### Model မွ record မ်ားအား ဖ်က္ပစ္ျခင္း

record တစ္ခုအား ဖ်က္ပစ္လုိပါက `delete` ဟုေသာ method ကုိ အသုံးျပဳႏိုင္သည္။

$user = User::find(1);

$user->delete();

#### Model မွ record မ်ားအား key အလုိက္ ဖ်က္ပစ္ျခင္း

User::destroy(1);

User::destroy(array(1, 2, 3));

User::destroy(1, 2, 3);

သင့္အေနျဖင့္ query လုပ္ျပီးမွလည္း ဖ်က္ပစ္ႏုိင္ပါသည္။

$affectedRows = User::where('votes', '>', 100)->delete();

####  Model ၏ Timestamps ကုိသာ update ျပဳလုပ္ျခင္း

Model ၏ Timestamps ကုိသာ update ျပဳလုပ္လိုပါက `touch` ကုိ အသုံးျပဳႏုိင္သည္။

$user->touch();

<a name="soft-deleting"></a>
## Soft Deleting  

Soft delete ျပဳလုပ္ပါက တကယ္ဖ်က္ပစ္လုိက္ျခင္း မဟုတ္ပဲ  သင့္ record ထဲတြင္  `deleted_at` ဟု timestamp တြင္ သင့္ဖ်က္ပစ္လုိက္သည့္ အခ်ိန္ကုိ မွတ္သားထားမည္ ျဖစ္သည္။ Soft delete ကုိ ထည့္သြင္းလုိပါက `SoftDeletingTrait` ကုိပါ ထည့္သြင္းရမည္ ျဖစ္သည္။

use Illuminate\Database\Eloquent\SoftDeletingTrait;

class User extends Eloquent {

use SoftDeletingTrait;

protected $dates = ['deleted_at'];

}

`deleted_at` ဟုသည့္ column ကုိ သင့္၏ table တြင္ ထည့္သြင္းလုိပါက migration တြင္ `softDeletes` ဟုသည့္ method ကုိ အသုံးျပဳႏုိင္ပါသည္။

$table->softDeletes();

ထုိသုိ ့ျပဳလုပ္ျပီး `delete` method ကို ေခၚယူပါက အမွန္တကယ္ ဖ်က္ပစ္မည္ မဟုတ္ပဲ `deleted_at` ဟု column တြင္ လက္ရွိ timestamp ကိုမွတ္သားထားမည္ ျဖစ္သည္။ Model တစ္ခုတြင္ soft delete ကို အသုံးျပဳထားပါက query ျပဳလုပ္ေသာ အခါတုိင္းတြင္ deleted record မ်ားမွာ ပါဝင္မည္ မဟုတ္ေပ။

#### Soft Deleted record မ်ားပါ ေရာစပ္ထုတ္ယူျခင္း


soft deleted record မ်ားပါ ေပါင္းစပ္ ထုတ္ယူလုိပါက `withTrashed` ကုိ query တြင္ထည့္သြင္း အသုံးျပဳရမည္ ျဖစ္သည္။

$users = User::withTrashed()->where('account_id', 1)->get();

`withTrashed` method ကုိ relationship ျပဳလုပ္ထားေသာ model တြင္လည္း အသုံးျပဳႏုိင္ပါသည္။

$user->posts()->withTrashed()->get();

ွSoft deleted ျပဳလုပ္ထားေသာ results မ်ားသာ ေတြ  ့ျမင္လုိပါက `onlyTrashed` ဟုေသာ method ကုိ အသုံးျပဳႏုိင္သည္။

$users = User::onlyTrashed()->where('account_id', 1)->get();

soft deleted ျပဳလုပ္ထားေသာ record မ်ားကုိ restore ျပဳလုပ္လုိပါက `restore` method ကို အသုံးျပဳႏုိင္သည္။

$user->restore();

`restore` method ကုိ query ျပဳလုပ္ေနသည့္ အေတာအတြင္းလည္း အသုံးျပဳႏုိင္သည္။

User::withTrashed()->where('account_id', 1)->restore();


`withTrashed` ကဲ့သုိ ့ပင္ `restore` method ကိုလည္း relationship မ်ားၾကားထဲအတြင္း အသုံးျပဳႏုိင္သည္။

$user->posts()->restore();

Record တစ္ခုကို အမွန္တကယ္ database ထဲမွ ဖ်က္ပစ္လုိပါက `forceDelete` method ကုိ အသုံးျပဳႏုိင္သည္။

$user->forceDelete();

`forceDelete` method မွာလည္း relationship မ်ားအၾကား အသုံးျပဳႏုိင္သည္။

$user->posts()->forceDelete();

soft delted ျပဳလုပ္ထားျခင္း ဟုတ္မဟုတ္ စစ္ေဆးႏုိင္ရန္  `trashed` method ကုိ အသုံးျပဳႏုိင္သည္။ 

if ($user->trashed())
{
//
}

<a name="timestamps"></a>
## Timestamps

ပုံမွန္အားျဖင့္ Eloquent အေနျဖင့္ `timestamp` attribute ကုိထည့္သြင္းေပးသည္ႏွင့္ `created_at` and `updated_at` ကို အလုိအေလ်ာက္ ကုိင္တြယ္ေပးမည္ ျဖစ္သည္။ သင့္အေနႏွင့္ မလုိခ်င္ပါက ေအာက္ပါအတုိင္း ေျပာင္းလဲ သတ္မွတ္ႏုိင္သည္။

#### အလုိအေလ်ာက္ Timestamps ျပဳလုပ္ျခင္းမွ ဖယ္ရွားျခင္း

class User extends Eloquent {

protected $table = 'users';

public $timestamps = false;

}

#### စိတ္ၾကိဳက္ Timestamp တစ္ခုသတ္မွတ္ျခင္း

Timestamp တစ္ခုကို စိတ္ၾကိဳက္သတ္မွတ္လုိပါက model အတြင္းရွိ `getDateFormat` ကုိ အသုံးျပဳ၍ သတ္မွတ္ႏုိင္သည္။

class User extends Eloquent {

protected function getDateFormat()
{
return 'U';
}

}

<a name="query-scopes"></a>
## Query Scopes

#### Query Scope တစ္ခုအား သတ္မွတ္ျခင္း

Scope မ်ားမွာ သင့္၏ query logic မ်ားကို ထပ္ခါထပ္ခါ အသုံးျပဳႏုိင္ျခင္း ျဖင့္ သက္သာေစသည္။  Scope တစ္ခုကုိ ဖန္တီးႏုိင္ရင္ `scope` ဟုပါဝင္သည့္ 
method တစ္ခုကုိ ဖန္တီးရန္ လုိေပမည္။

class User extends Eloquent {

public function scopePopular($query)
{
return $query->where('votes', '>', 100);
}

public function scopeWomen($query)
{
return $query->whereGender('W');
}

}

#### Query Scope တစ္ခုအား အသုံးျပဳျခင္း 

$users = User::popular()->women()->orderBy('created_at')->get();

#### Scopes အရွင္မ်ား ဖန္တီးျခင္း

တခါတရံ သင့္အေနျဖင့္ parameter မ်ားလက္ခံေသာ scope အရွင္မ်ားကို ဖန္တီးလုိေပမည္။ ထုိသုိ ့ျပဳလုပ္ႏုိင္ရန္ သင့္၏ scope function အတြင္းတြင္

class User extends Eloquent {

public function scopeOfType($query, $type)
{
return $query->whereType($type);
}

}

ထိုေနာက္ scope တြင္ parameter ကုိ ထည့္သြင္း အသုံးျပဳႏုိင္သည္။

$users = User::ofType('member')->get();

<a name="relationships"></a>
## Relationships

Database table မ်ားမွာ တခါတရံ တစ္ခုႏွင့္ တစ္ခု ဆက္စပ္ျပီး တည္ရွိႏုိင္ေပသည္။ ဥပမာ Blog post တစ္ခုတြင္ comment မ်ားစြာ ပါဝင္သကဲ့သုိ ့  Order တစ္ခုတြင္လည္း User တစ္ေယာက္ႏွင့္ ဆက္စပ္ႏုိင္ ေပသည္။ Laravel အေနျဖင့္ ဆက္စပ္မႈ မ်ိဳးစုံကုိ ေဆာင္ရြက္ႏုိင္ေအာင္ ကူညီေပးထားပါသည္။

- [One To One](#one-to-one)
- [One To Many](#one-to-many)
- [Many To Many](#many-to-many)
- [Has Many Through](#has-many-through)
- [Polymorphic Relations](#polymorphic-relations)
- [Many To Many Polymorphic Relations](#many-to-many-polymorphic-relations)

<a name="one-to-one"></a>
### One To One

#### One To One Relation တစ္ခုကုိ တည္ေဆာက္ျခင္း

one-to-one relationship မွာ အလြန္ပင္ အေျခခံက်ေသာ relation ျဖစ္သည္။  ဥပမာ User တစ္ေယာက္တြင္ Phone တစ္လုံး ရွိရမည့္ အေနအထားမ်ိဳး။ 
ထုိသုိ ့ေသာ relation မ်ိဳးကို Eloquent တြင္ ဖန္တီးႏုိင္ေပသည္။

class User extends Eloquent {

public function phone()
{
return $this->hasOne('Phone');
}

}


`hasOne` တြင္ထည့္သြင္းရမည့္ argument မွာ ဆက္စပ္ေနသည့္ Model ၏ အမည္ပင္ျဖစ္သည္။ relationship တည္ေဆာက္ျပီးသည္ႏွင့္ Eloquent ၏ [dynamic properties](#dynamic-properties): ကုိ အသုံးျပဳျပီး အခ်က္အလက္မ်ားကုိ ထုတ္ယူႏုိင္သည္။

$phone = User::find(1)->phone;

အထက္ပါ statement အတြက္ run သြားမည့္ SQL မွာ ေအာက္ပါ အတုိင္းျဖစ္သည္။

select * from users where id = 1

select * from phones where user_id = 1

Eloquent အေနျဖင့္ model name မ်ားကို အေျခခံျပီး Forigen key မ်ားကို သတ္မွတ္သြားမည္ကုိ သတိျပဳရမည္။ အထက္က `Phone` model တြင္ `user_id` ကုိ foreign key အေနျဖင့္ အလုိအေလ်ာက္ သတ္မွတ္မည္ ျဖစ္သည္။  မိမိတုိ ့ စိတ္ၾကိဳက္ေျပာင္းလဲလုိပါက `hasOne` method တြင္ ဒုတိယ argument အျဖစ္သြင္းေပးရန္ လုိေပမည္။  ထုိထက္ပုိ၍ တတိယ argument အေနျဖင့္ ထည့္သြင္းပါက မည္သည့္ local column ကုိ ပူးေပါင္းမည္ကုိပါ သတ္မွတ္ႏုိင္သည္။

return $this->hasOne('Phone', 'foreign_key');

return $this->hasOne('Phone', 'foreign_key', 'local_key');

#### Relation ေျပာင္းျပန္သတ္မွတ္ျခင္း

`Phone` model မွ Relation ကုိ ေျပာင္းျပန္အေနျဖင့္ သတ္မွတ္လုိပါက `belongsTo` ဟုသည့္ method ကုိ အသုံးျပဳႏုိင္သည္။

class Phone extends Eloquent {

public function user()
{
return $this->belongsTo('User');
}

}

အထက္က ဥပမာတြင္ Eloquent အေနျဖင့္ `phones` table မွ `user_id` column ကုိ အသုံးျပဳမည္ ျဖစ္သည္။ `hasMany` ကဲ့သုိ ့ပင္ Foriegn Key ကုိ သတ္မွတ္လုိပါက ဒုတိယ argument ကုိ ထည့္သြင္းေပးႏုိင္သည္။


class Phone extends Eloquent {

public function user()
{
return $this->belongsTo('User', 'local_key');
}

}

ထုိအျပင္ parent table ႏွင့္ဆက္စပ္ေနသည့္  column ကုိ တတိယ parameter အျဖစ္ ထည့္သြင္းႏုိင္သည္။

class Phone extends Eloquent {

public function user()
{
return $this->belongsTo('User', 'local_key', 'parent_key');
}

}

<a name="one-to-many"></a>
### One To Many

one-to-many relation ၏ ဥပမာမွာ blog post တစ္ခုတြင္ comment မ်ားစြာ ရွိသကဲ့သုိ ့ပင္ ျဖစ္သည္။ ထုိသုိ ့ relation ကုိ ေအာက္ပါအတုိင္း model တြင္
သတ္မွတ္ႏုိင္သည္။

class Post extends Eloquent {

public function comments()
{
return $this->hasMany('Comment');
}

}

ထုိအခါ post comments မ်ားကို [dynamic property](#dynamic-properties) ကုိ အသုံးျပဳ၍ ထုတ္ယူႏုိင္ပါျပီ။

$comments = Post::find(1)->comments;

ထုိထဲမွ  ထုတ္ယူလုိသည့္ comment မ်ားကုိ စစ္ယူလုိပါက `comments` method ေနာက္တြင္ method မ်ားကုိ စီတန္း အသုံးျပဳႏုိင္ပါေသးသည္။

$comments = Post::find(1)->comments()->where('title', '=', 'foo')->first();

၄င္းတြင္လည္း `hasOne` ကဲ့သုိ ့ foriegn key ကုိ  `hasMany` method  ေနာက္တြင္ second argument အေနျဖင့္ႏွင့္  third argument ကို local key အေနျဖင့္ ထည့္သြင္းႏုိင္ေပသည္။

return $this->hasMany('Comment', 'foreign_key');

return $this->hasMany('Comment', 'foreign_key', 'local_key');

#### ေျပာင္းျပန္ relation သတ္မွတ္ျခင္း

`Comment` model ေျပာင္းျပန္ သတ္မွတ္ႏုိင္ရန္  `belongsTo` ဟုသည့္ method ကုိ အသုံးျပဳႏုိင္သည္။

class Comment extends Eloquent {

public function post()
{
return $this->belongsTo('Post');
}

}

<a name="many-to-many"></a>
### Many To Many


Many-to-many relations မွာ ပုိမိုရႈပ္ေထြးသည့္ relation ျဖစ္သည္။ ဥပမာ User တစ္ေယာက္မွာ တာဝန္မ်ားစြာ ရွိျပီး တာဝန္တစ္ခုကိုလည္း User မ်ားစြာ ခြဲေဝေပးအပ္ထားသည္ ဆုိပါစုိ ့။  User မ်ားစြာ  "Admin" တာဝန္ကုိ ယူထားႏုိင္သည့္ အေျခအေနတြင္ရွိေပမည္။  ထုိသုိ ့ေသာ အေျခအေနတြင္ Database 
Table သုံးခု လုိအပ္မည္ ျဖစ္သည္။ ၄င္းတုိ ့မွာ `users` ၊ `roles` ႏွင့္ `role_user` တုိ ့ျဖစ္ၾကသည္။ `role_user` table မွာ ဆက္စပ္ေနသည့္ model အမည္မ်ားကုိ ဆက္စပ္ေပးမည္ ျဖစ္ျပီး ၄င္းတြင္ `user_id` ႏွင့္ `role_id` ဟူေသာ columns ႏွစ္ခု ပါဝင္မည္ ျဖစ္သည္။


many-to-many relation  ကုိ  `belongsToMany` method ကုိ အသုံးျပဳ၍ ေရးသားႏုိင္သည္။

class User extends Eloquent {

public function roles()
{
return $this->belongsToMany('Role');
}

}

ထုိအခါ `User` မွ role ကုိ ေအာက္ပါ အတုိင္း ထုတ္ယူႏုိင္မည္ ျဖစ္သည္။

$roles = User::find(1)->roles;

မိမိ၏ ၾကားခံ table ၏ အမည္ကုိ စိတ္ၾကိဳက္ သတ္မွတ္လုိပါက `belongsToMany` method ၏ ဒုတိယ argument မွ သြင္း၍ စိတ္ၾကိဳက္ သတ္မွတ္ႏုိင္သည္။

return $this->belongsToMany('Role', 'user_roles');

ထုိအျပင္ ပါဝင္ပတ္သတ္ေနေသာ Keys မ်ားကိုလည္း စိတ္ၾကိဳက္ သတ္မွတ္ႏုိင္သည္။

return $this->belongsToMany('Role', 'user_roles', 'user_id', 'foo_id');

ထုိအျပင္ `Role` model မွလည္း ေျပာင္းျပန္သတ္မွတ္ ၍လည္း ျဖစ္ပါသည္။

class Role extends Eloquent {

public function users()
{
return $this->belongsToMany('User');
}

}

<a name="has-many-through"></a>
### Has Many Through

 "has many through"  ေဝးကြာေနသည့္ relation မ်ားမွ record မ်ားကုိ access လုပ္ႏုိင္ရန္ အလြယ္တကူ ၾကားျဖတ္ေဆာင္ရြက္ေပးေသာ method ျဇစ္သည္။ ဥပမာ  `Country` model မွာ  `Posts` ျဖင့္ ခ်ိတ္ဆက္ထားျခင္း မရွိေသာ္လည္း `Users` model ျဖင့္မူ ခ်ိတ္ဆက္ထားပါက တဆင့္ေက်ာ္၍ access လုပ္ႏုိင္သည္။  ထုိ table မ်ား၏  relationship မွာ ေအာက္ပါအတုိင္း ဆုိပါစို ့

countries
id - integer
name - string

users
id - integer
country_id - integer
name - string

posts
id - integer
user_id - integer
title - string

`posts` table တြင္ `country_id` column မပါဝင္ေသာ္လည္း `hasManyThrough` relation ျဖင့္ `$country->posts` ဟု၍ accessible ျဖစ္ေအာင္ စြမ္းေဆာင္ႏုိင္ေပသည္။ 

class Country extends Eloquent {

public function posts()
{
return $this->hasManyThrough('Post', 'User');
}

}

relationship key မ်ားကုိ စိတ္ၾကိဳက္သတ္မွတ္လုိပါက တတိယႏွင့္ စတုတၳ parameter အမ်ားအျဖစ္ ထည့္သြင္းႏုိင္ေပသည္။

class Country extends Eloquent {

public function posts()
{
return $this->hasManyThrough('Post', 'User', 'country_id', 'user_id');
}

}

<a name="polymorphic-relations"></a>
### Polymorphic Relations

Polymorphic relations ကုိ အသုံးျပဳျခင္းျဖင့္ အျခား Model တစ္ခုထက္ပုိ၍ associate ျပဳလုပ္ထားေသာ record မ်ားကို ထုတ္ယူႏုိင္သည္။ ဥပမာ သင့္တြင္ 
staff ဟုေသာ model ႏွင့္ order ဟုေသာ model ႏွစ္ခုလုံးႏွင့္ ပတ္သတ္ေနသည့္ photo ဟုေသာ model ရွိသည္ ဆုိပါစုိ ့။


class Photo extends Eloquent {

public function imageable()
{
return $this->morphTo();
}

}

class Staff extends Eloquent {

public function photos()
{
return $this->morphMany('Photo', 'imageable');
}

}

class Order extends Eloquent {

public function photos()
{
return $this->morphMany('Photo', 'imageable');
}

}

#### Polymorphic Relation ကုိ အသုံးျပဳျခင္း

ေအာက္ပါ အတုိင္း photo မ်ားကို Staff member မ်ားမွေသာ္လည္းေကာင္း  Order မွေသာ္လည္းေကာင္း ထုတ္ယူႏုိင္သည္။

$staff = Staff::find(1);

foreach ($staff->photos as $photo)
{
//
}

#### Polymorphic Relation မွ Owner ၏ record မ်ားကုိ ထုတ္ယူျခင္း

သုိ ့ေသာ္ တကယ့္ "polymorphic" အလွတရားမွာ `Photo` model မွ staff ျဖစ္ေစ ၊ order ျဖစ္ေစ ထုတ္ယူႏုိင္ျခင္း ျဖစ္သည္။


$photo = Photo::find(1);

$imageable = $photo->imageable;

`Photo` model မွ `imageable` relation  မွာ `Staff` မွျဖစ္ေစ `Order` instance ျဖစ္ေစ ပိုင္ဆုိင္သည့္ model ေပၚမူတည္၍ ထုတ္ေပးသြားမည္ ျဖစ္သည္။

#### Polymorphic Relation Table Structure

မည္သုိ ့မည္ပုံ အလုပ္လုပ္ေဆာင္သြားသည္ကုိ သိရွိႏုိင္ရန္ ေအာက္ပါ database structure ကုိ ၾကည့္ရႈႏုိင္ပါသည္။

staff
id - integer
name - string

orders
id - integer
price - integer

photos
id - integer
path - string
imageable_id - integer
imageable_type - string

Key field အေနျဖင့္  `photos` table မွ `imageable_id` ႏွင့္ `imageable_type` တုိ ့ကုိ မွတ္သားထားရပါမည္ ျဖစ္သည္။ ID မွာ Order သုိ ့မဟုတ္ 
Staff တုိ ့၏  ID ႏွင့္ ခ်ိတ္ဆက္ထားမည္ ျဖစ္သည္။  ORM အေနျဖင့္ မည္သည့္ model ကုိျပန္ရမည္ ဆုိသည္ကုိ `imageable` ၏ relation ကို ေထာက္ရႈ၍ လုပ္ေဆာင္ သြားမည္ ျဖစ္သည္။

<a name="many-to-many-polymorphic-relations"></a>
### Many To Many Polymorphic Relations

#### Polymorphic Many To Many Relation Table Structure  

သမရုိးက် polymorphic relations တစ္ခုသာမက many-to-many polymorphic relations မ်ားကိုပါ တည္ေဆာက္ႏုိင္သည္။ ဥပမာ blog တစ္ခု၏ database structure ျဖစ္ေသာ  `Post` ႏွင့္ `Video` model တုိ ့တြင္ `Tag` model ကုိ တူညီစြာ polymorphic relation အေနျဖင့္ ခ်ိတ္ဆက္ရန္ လုိေပမည္။ ေရွဦးစြာ table structure ကုိၾကည့္လုိက္ပါ။

posts
id - integer
name - string

videos
id - integer
name - string

tags
id - integer
name - string

taggables
tag_id - integer
taggable_id - integer
taggable_type - string

အထက္ပါ table အတြက္ relationship မ်ားကုိ model တြင္ ေအာက္ပါအတုိင္း တည္ေဆာက္ရမည္ျဖစ္သည္။ `Post` ႏွင့္ `Video` model တုိ ့ႏွစ္ခုလုံးတြင္
`tags` method မွ `morphToMany` relationship ကုိ ေၾကညာေပးရမည္ ျဖစ္သည္။

class Post extends Eloquent {

public function tags()
{
return $this->morphToMany('Tag', 'taggable');
}

}

`Tag` model အေနျဖင့္ ၄င္း၏ relationships ကုိ ေအာက္ပါ အတုိင္း သတ္မွတ္ႏုိင္သည္။ 

class Tag extends Eloquent {

public function posts()
{
return $this->morphedByMany('Post', 'taggable');
}

public function videos()
{
return $this->morphedByMany('Video', 'taggable');
}

}

<a name="querying-relations"></a>
## Relation မ်ားကုိ Query ျပဳလုပ္ျခင္း

#### Relations မ်ားတြင္ Select ကုိ အသုံးျပဳျခင္း

Model မ်ားမွ record မ်ားကုိ access ျပဳလုပ္ရာတြင္ ၊  result မ်ားကို စစ္ေဆးျပီးမွ ထုတ္ယူလုိသည့္ အေနအထားမ်ိဳးတြင္ ရွိေပႏုိင္သည္။ ဥပမာ သင့္အေနျဖင့္ Comment တစ္ခု အနည္းဆုံး ရွိသည့္ blog post မ်ားကုိ ဆြဲထုတ္လုိသည္ ဆုိပါစို ့။  သင့္အေနနဲ ့ `has` method ကုိ အသုံးျပဳရမည္ ျဖစ္သည္။

$posts = Post::has('comments')->get();

has method တြင္ သင့္အေနျဖင့္ operator မ်ား ႏွင့္  ထုတ္ယူလုိသည့္ အေရအတြက္ကုိ သတ္မွတ္ႏုိင္သည္။

$posts = Post::has('comments', '>=', 3)->get();

သင့္အေနျဖင့္ ပုိ၍ အေသးစိတ္က်ျပီး "where" conditions မ်ားကုိ `has` queries အတြင္း စစ္ေဆးလုိပါက `whereHas` ႏွင့္ `orWhereHas` method မ်ားကုိအသုံးျပဳႏုိင္သည္။

$posts = Post::whereHas('comments', function($q)
{
$q->where('content', 'like', 'foo%');

})->get();

<a name="dynamic-properties"></a>
### Dynamic Properties


Eloquent တြင္ သင့္အေနျဖင့္ relations မ်ားမွ properties မ်ားကုိ dynamic properties အေနျဖင့္ ဆြဲယူႏုိင္သည္။ Eloquent အေနျဖင့္ သင့္၏ relationship အလုိအေလ်ာက္အေနျဖင့္ relations ကုိ အလိုအေလ်ာက္ load လုပ္ကာ ေခၚယူမည္ ျဖစ္ျပီး  `get` ( one-to-many relationships) ေပေလာ၊ `first` (for one-to-one relationships) method ေပေလာ ကုိပင္ ခြဲျခားလုပ္ေဆာင္ေပးမည္ ျဖစ္သည္။ ထုိေနာက္ တူညီေသာ အမည္မွ တဆင့္
dynamic property ကုိ အလြယ္တကူ ေခၚဆုိ ႏုိင္ေပမည္။ ဥပမာ `$phone` ဟုသည့္ model မွ တဆင့္

class Phone extends Eloquent {

public function user()
{
return $this->belongsTo('User');
}

}

$phone = Phone::find(1);

Instead of echoing the user's email like this:

echo $phone->user()->first()->email;

It may be shortened to simply:

echo $phone->user->email;

> **Note:** Relationships မ်ားကုိ return ျပန္ေသာ result မ်ားကုိ အလုပ္လုပ္သြားေသာ method မွာ `Illuminate\Database\Eloquent\Collection` class မွ instance မ်ားကုိ ျပန္ျခင္းျဖစ္သည္။

<a name="eager-loading"></a>
## Eager Loading


Eager loading exists to N+1 query ကဲ့သို ့ေသာ Query မ်ားကုိ ပုိ ့၍ ေပါ့ပါးစြာ အသုံးျပဳႏုိင္ရန္ ျဖစ္သည္။ ဥပမာ `Author` model ႏွင့္ `Book` model တုိ ့ ဆက္စပ္ေနသည္ ဆုိပါစုိ ့။ ၄င္းတုိ ့၏ relationship ကုိ ေအာက္ပါ အတိုင္း သတ္မွတ္ႏုိင္ပါသည္။ 

class Book extends Eloquent {

public function author()
{
return $this->belongsTo('Author');
}

}

ထုိေနာက္ ေအာက္ပါ code ကုိ ၾကည့္ၾကည့္ပါ။

foreach (Book::all() as $book)
{
echo $book->author->name;
}

ထုိ loop မွာ Book မွ ရွိသမွ် စာအုပ္တုိင္းကုိ ေခၚယူမည္ ျဖစ္သည္။ ထုိေနာက္ ထုိေနာက္ ထုိေနာက္ ေနာက္ query တစ္ခုအေနျဖင့္ စာအုပ္တစ္ခုခ်င္းဆီ၏ 
author ကုိ  ေဖာ္ျပသြားမည္ ျဖစ္သည္။ အကယ္၍ စာအုပ္ ၂၅ အုပ္ ရွိသည္ ဆုိပါစုိ ့ ၊ query ၂၆ ေၾကာင္း run ျဖစ္သည္။ သုိ ့ပင္ေသာ္ညား eager loading ၏ အက်ိဳးေက်းဇူးေၾကာင့္ မလုိအပ္ေသာ query မ်ားကုိ ေလွ်ာ့ခ်ႏုိင္သည္။ ထုိ relationship တြင္ `with` method အသုံးျပဳ၍ eager load ျပဳလုပ္ႏုိင္သည္။


foreach (Book::with('author')->get() as $book)
{
echo $book->author->name;
}

အထက္ပါ loop တြင္မူ query ႏွစ္ေၾကာင္းသာ execute ျပဳလုပ္မည္ ျဖစ္သည္။

select * from books

select * from authors where id in (1, 2, 3, 4, 5, ...)

Eager loading ကုိ အသုံးျပဳျခင္း အားျဖင့္ သင့္ application ၏ performance ကုိ သိသိသာသာ ျမင့္တက္ေစမည္ ျဖစ္သည္။

ထုိအျပင္ တစ္ခုထက္ပုိေသာ relation မ်ားတြင္ တခ်ိန္တည္းတြင္ eager load အသုံးျပဳႏုိင္မည္ ျဖစ္သည္။

$books = Book::with('author', 'publisher')->get();

Nested relationship မ်ားတြင္လည္း eager load အသုံးျပဳႏုိင္သည္။

$books = Book::with('author.contacts')->get();

အထက္ ဥပမာ တြင္ `author` ႏွင့္ ပတ္သတ္ေနသည္မ်ားကုိ eager load ျပဳလုပ္ျပီး author ၏ `contacts` relation ပါ load သြားမည္ ျဖစ္သည္။

### Eager Load အကန္ ့အသတ္မ်ား 

ထခါတရံ condition မ်ား စစ္ေဆးျပီးမွ relationship မ်ားကို eager load ျပဳလုပ္လုိမည္ အခ်ိန္ကာလ လည္း ရွိေပမည္။ ေအာက္က ဥပမာတြင္ ဆုိပါစို ့

$users = User::with(array('posts' => function($query)
{
$query->where('title', 'like', '%first%');

}))->get();

ထုိ ဥပမာ တြင္ user's post တြင္းမွ  "first"  စကာလုံး ႏွင့္စတင္သည္မ်ားကိုသာ eager load လုပ္သြားမည္ ျဖစ္သည္။ Closure မ်ား အတြင္းတြင္မူ အကန့္ အသတ္မရွိေပ။  သင့္အေနျဖင့္ ေအာက္က အတုိင္း order အလုိက္ စီရီႏုိင္ေပဦးမည္။

$users = User::with(array('posts' => function($query)
{
$query->orderBy('created_at', 'desc');

}))->get();

### Lazy Eager Loading

တည္ရွိေနျပီးေသာ model collection မ်ားထဲမွ eager load ႏွင့္ ဆက္စပ္ေနေသာ model မ်ားကုိ တုိက္ရုိက္ ေခၚယူ၍လည္း ျဖစ္ႏုိင္ေပသည္။ ထုိသုိ ့ျပဳလုပ္ျခင္း Model မ်ားကို Load လုပ္ရာတြင္ load လုပ္မည္ မလုပ္မည္ကုိ dynamically စဥ္းစားဆုံးျဖတ္ရာတြင္ ေသာ္လည္းေကာင္း ၊ caching ျဖင့္ ပူးေပါင္း အသုံးျပဳရာတြင္ေသာ္လည္းေကာင္း အသုံးဝင္သည္။

$books = Book::all();

$books->load('author', 'publisher');

<a name="inserting-related-models"></a>
## Inserting Related Models

#### ဆက္စပ္ေနသည့္ Model တစ္ခုႏွင့္ ခ်ိတ္ဆက္ျခင္း

တခါတရံ ဆက္စပ္ေနသည့္ model မ်ားအား insert ျပဳလုပ္ရန္လည္း လုိေပမည္။ ဥပမာ သင့္အေနျဖင့္ post တစ္ခုတြင္ comment တစ္ခုကုိ ထည့္သြင္းမည္ ဆုိပါစုိ ့။  Model တစ္ခု၏ `post_id` foreign key ကုိ manually ထည့္သြင္းေနမည့္ အစား `Post` model ဖက္မွ တုိက္ရုိက္ထည့္သြင္း၍လည္း ရေပသည္။

$comment = new Comment(array('message' => 'A new comment.'));

$post = Post::find(1);

$comment = $post->comments()->save($comment);

အထက္က ဥပမာတြင္ `post_id` field ကုိ အလုိအေလ်ာက္ ထည့္သြင္းသြားမည္ ျဖစ္သည္။

### Associating Models (Belongs To)


When updating a `belongsTo` relationship, you may use the `associate` method. This method will set the foreign key on the child model:

$account = Account::find(10);

$user->account()->associate($account);

$user->save();

### Inserting Related Models (Many To Many)

You may also insert related models when working with many-to-many relations. Let's continue using our `User` and `Role` models as examples. We can easily attach new roles to a user using the `attach` method:

#### Attaching Many To Many Models

$user = User::find(1);

$user->roles()->attach(1);

You may also pass an array of attributes that should be stored on the pivot table for the relation:

$user->roles()->attach(1, array('expires' => $expires));

Of course, the opposite of `attach` is `detach`:

$user->roles()->detach(1);

#### Using Sync To Attach Many To Many Models

You may also use the `sync` method to attach related models. The `sync` method accepts an array of IDs to place on the pivot table. After this operation is complete, only the IDs in the array will be on the intermediate table for the model:

$user->roles()->sync(array(1, 2, 3));

#### Adding Pivot Data When Syncing

You may also associate other pivot table values with the given IDs:

$user->roles()->sync(array(1 => array('expires' => true)));

Sometimes you may wish to create a new related model and attach it in a single command. For this operation, you may use the `save` method:

$role = new Role(array('name' => 'Editor'));

User::find(1)->roles()->save($role);

In this example, the new `Role` model will be saved and attached to the user model. You may also pass an array of attributes to place on the joining table for this operation:

User::find(1)->roles()->save($role, array('expires' => $expires));

<a name="touching-parent-timestamps"></a>
## Touching Parent Timestamps

When a model `belongsTo` another model, such as a `Comment` which belongs to a `Post`, it is often helpful to update the parent's timestamp when the child model is updated. For example, when a `Comment` model is updated, you may want to automatically touch the `updated_at` timestamp of the owning `Post`. Eloquent makes it easy. Just add a `touches` property containing the names of the relationships to the child model:

class Comment extends Eloquent {

protected $touches = array('post');

public function post()
{
return $this->belongsTo('Post');
}

}

Now, when you update a `Comment`, the owning `Post` will have its `updated_at` column updated:

$comment = Comment::find(1);

$comment->text = 'Edit to this comment!';

$comment->save();

<a name="working-with-pivot-tables"></a>
## Working With Pivot Tables

As you have already learned, working with many-to-many relations requires the presence of an intermediate table. Eloquent provides some very helpful ways of interacting with this table. For example, let's assume our `User` object has many `Role` objects that it is related to. After accessing this relationship, we may access the `pivot` table on the models:

$user = User::find(1);

foreach ($user->roles as $role)
{
echo $role->pivot->created_at;
}

Notice that each `Role` model we retrieve is automatically assigned a `pivot` attribute. This attribute contains a model representing the intermediate table, and may be used as any other Eloquent model.

By default, only the keys will be present on the `pivot` object. If your pivot table contains extra attributes, you must specify them when defining the relationship:

return $this->belongsToMany('Role')->withPivot('foo', 'bar');

Now the `foo` and `bar` attributes will be accessible on our `pivot` object for the `Role` model.

If you want your pivot table to have automatically maintained `created_at` and `updated_at` timestamps, use the `withTimestamps` method on the relationship definition:

return $this->belongsToMany('Role')->withTimestamps();

#### Deleting Records On A Pivot Table

To delete all records on the pivot table for a model, you may use the `detach` method:

User::find(1)->roles()->detach();

Note that this operation does not delete records from the `roles` table, but only from the pivot table.

#### Updating A Record On A Pivot Table

Sometimes you may need to update your pivot table, but not detach it. If you wish to update your pivot table in place you may use `updateExistingPivot` method like so:

User::find(1)->roles()->updateExistingPivot($roleId, $attributes);

#### Defining A Custom Pivot Model

Laravel also allows you to define a custom Pivot model. To define a custom model, first create your own "Base" model class that extends `Eloquent`. In your other Eloquent models, extend this custom base model instead of the default `Eloquent` base. In your base model, add the following function that returns an instance of your custom Pivot model:

public function newPivot(Model $parent, array $attributes, $table, $exists)
{
return new YourCustomPivot($parent, $attributes, $table, $exists);
}

<a name="collections"></a>
## Collections

All multi-result sets returned by Eloquent, either via the `get` method or a `relationship`, will return a collection object. This object implements the `IteratorAggregate` PHP interface so it can be iterated over like an array. However, this object also has a variety of other helpful methods for working with result sets.

#### Checking If A Collection Contains A Key

For example, we may determine if a result set contains a given primary key using the `contains` method:

$roles = User::find(1)->roles;

if ($roles->contains(2))
{
//
}

Collections may also be converted to an array or JSON:

$roles = User::find(1)->roles->toArray();

$roles = User::find(1)->roles->toJson();

If a collection is cast to a string, it will be returned as JSON:

$roles = (string) User::find(1)->roles;

#### Iterating Collections

Eloquent collections also contain a few helpful methods for looping and filtering the items they contain:

$roles = $user->roles->each(function($role)
{
//
});

#### Filtering Collections

When filtering collections, the callback provided will be used as callback for [array_filter](http://php.net/manual/en/function.array-filter.php).

$users = $users->filter(function($user)
{
return $user->isAdmin();
});

> **Note:** When filtering a collection and converting it to JSON, try calling the `values` function first to reset the array's keys.

#### Applying A Callback To Each Collection Object

$roles = User::find(1)->roles;

$roles->each(function($role)
{
//
});

#### Sorting A Collection By A Value

$roles = $roles->sortBy(function($role)
{
return $role->created_at;
});

#### Sorting A Collection By A Value

$roles = $roles->sortBy('created_at');

#### Returning A Custom Collection Type

Sometimes, you may wish to return a custom Collection object with your own added methods. You may specify this on your Eloquent model by overriding the `newCollection` method:

class User extends Eloquent {

public function newCollection(array $models = array())
{
return new CustomCollection($models);
}

}

<a name="accessors-and-mutators"></a>
## Accessors & Mutators

#### Defining An Accessor

Eloquent provides a convenient way to transform your model attributes when getting or setting them. Simply define a `getFooAttribute` method on your model to declare an accessor. Keep in mind that the methods should follow camel-casing, even though your database columns are snake-case:

class User extends Eloquent {

public function getFirstNameAttribute($value)
{
return ucfirst($value);
}

}

In the example above, the `first_name` column has an accessor. Note that the value of the attribute is passed to the accessor.

#### Defining A Mutator

Mutators are declared in a similar fashion:

class User extends Eloquent {

public function setFirstNameAttribute($value)
{
$this->attributes['first_name'] = strtolower($value);
}

}

<a name="date-mutators"></a>
## Date Mutators

By default, Eloquent will convert the `created_at`, `updated_at`, and `deleted_at` columns to instances of [Carbon](https://github.com/briannesbitt/Carbon), which provides an assortment of helpful methods, and extends the native PHP `DateTime` class.

You may customize which fields are automatically mutated, and even completely disable this mutation, by overriding the `getDates` method of the model:

public function getDates()
{
return array('created_at');
}

When a column is considered a date, you may set its value to a UNIX timestamp, date string (`Y-m-d`), date-time string, and of course a `DateTime` / `Carbon` instance.

To totally disable date mutations, simply return an empty array from the `getDates` method:

public function getDates()
{
return array();
}

<a name="model-events"></a>
## Model Events

Eloquent models fire several events, allowing you to hook into various points in the model's lifecycle using the following methods: `creating`, `created`, `updating`, `updated`, `saving`, `saved`, `deleting`, `deleted`, `restoring`, `restored`.

Whenever a new item is saved for the first time, the `creating` and `created` events will fire. If an item is not new and the `save` method is called, the `updating` / `updated` events will fire. In both cases, the `saving` / `saved` events will fire.

#### Cancelling Save Operations Via Events

If `false` is returned from the `creating`, `updating`, `saving`, or `deleting` events, the action will be cancelled:

User::creating(function($user)
{
if ( ! $user->isValid()) return false;
});

#### Setting A Model Boot Method

Eloquent models also contain a static `boot` method, which may provide a convenient place to register your event bindings.

class User extends Eloquent {

public static function boot()
{
parent::boot();

// Setup event bindings...
}

}

<a name="model-observers"></a>
## Model Observers

To consolidate the handling of model events, you may register a model observer. An observer class may have methods that correspond to the various model events. For example, `creating`, `updating`, `saving` methods may be on an observer, in addition to any other model event name.

So, for example, a model observer might look like this:

class UserObserver {

public function saving($model)
{
//
}

public function saved($model)
{
//
}

}

You may register an observer instance using the `observe` method:

User::observe(new UserObserver);

<a name="converting-to-arrays-or-json"></a>
## Arrays / JSON သုိ ့ေျပာင္းလဲ အသုံးျပဳျခင္း

#### Converting A Model To An Array

JSON APIs မ်ား တည္ေဆာက္ရာတြင္ ၊ သင့္ အေနျဖင့္ model ႏွင့္ ဆက္စပ္ပတ္သတ္သည္မ်ားကို array အေနျဖင့္ေသာ လည္းေကာင္း JSON အေနျဖင့္ေသာ္ လည္းေကာင္း ထုတ္ေပးလုိသည့္ အခ်ိန္ကာလ မ်ား ရွိေပမည္။ Eloquent အေနျဖင့္ ထုိသုိ ့ျပဳလုပ္ႏုိင္ရန္ ေထာက္ပံ့ေပးေသာ method မ်ားလည္း ရွိေပသည္။ ထုိသုိ ့ ၄င္းႏွင့္ တကြ ဆက္စပ္ပတ္သတ္ေနသည္မ်ားကိုပါက array အျဖစ္ေျပာင္းလဲ ႏုိင္ရန္ `toArray` method ကုိ အသုံးျပဳႏုိင္သည္။

$user = User::with('roles')->first();

return $user->toArray();

Models connection တစ္ခုလုံးပါ array အျဖစ္ ေျပာင္းလဲသြားသည္ကုိ သတိျပဳရမည္။ 

return User::all()->toArray();

#### Model တစ္ခုကုိ JSON သုိ ့ ေျပာင္းလဲျခင္း

Model တစ္ခုကုိ JSON အေနျဖင့္ ေျပာင္းလဲလုိပါက `toJson` method ကုိ အသုံးျပဳႏုိင္သည္။

return User::find(1)->toJson();

#### Route တစ္ခုမွ Model ကုိ return ျပန္ျခင္း  

Model သုိ ့မဟုတ္ collection တစ္ခုသည္ string အျဖစ္သုိ ့ cast အလုပ္ခံရပါက အလုိအေလ်ာက္ JSON အျဖစ္သုိ ့ေျပာင္းလဲသြားမည္ ျဖစ္သည္။ 
ထုိ ့ေၾကာင့္ သင့္ application route မွ တုိက္ရုိက္ return ျပန္၍လည္း ရႏုိင္သည္။

Route::get('users', function()
{
return User::all();
});

#### Array သုိ ့မဟုတ္ JSON သုိ ့ေျပာင္းလဲရာတြင္ Attribute တစ္ခ်ိဳ  ့ကုိ ေဖ်ာက္ထားျခင္း

တခါတရံ သင့္အေနျဖင့္ တခ်ိဳ  ့ေသာ attribute မ်ားကို array သုိ ့မဟုတ္ JSON သုိ ့ေျပာင္းလဲရာတြင္ ပါမလာ ေစခ်င္သည့္ attribute မ်ား (ဥပမာ password မ်ားကဲ့သုိ ့ေသာ ) ရွိေပမည္။ ထုိသုိ ့ျပဳလုပ္ႏုိင္ရန္ model အတြင္းတြင္ `hidden` ဟူေသာ property တစ္ခုအျဖစ္ ေၾကညာေပးရန္ လုိေပမည္။

class User extends Eloquent {

protected $hidden = array('password');

}

> **Note:** When hiding relationships, use the relationship's **method** name, not the dynamic accessor name.

အျပန္အလွန္အားျဖင့္ သင့္အေနျဖင့္ ထုတ္ခ်င္သည္မ်ားကိုသာ ေဖာ္ျပႏုိင္ရန္ `visible` ဟုသည္ property တစ္ခု ေၾကညာႏုိင္ေပသည္။

protected $visible = array('first_name', 'last_name');

<a name="array-appends"></a>
Occasionally, you may need to add array attributes that do not have a corresponding column in your database. To do so, simply define an accessor for the value:

public function getIsAdminAttribute()
{
return $this->attributes['admin'] == 'yes';
}

Once you have created the accessor, just add the value to the `appends` property on the model:

protected $appends = array('is_admin');

Once the attribute has been added to the `appends` list, it will be included in both the model's array and JSON forms.