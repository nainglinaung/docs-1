# Redis

- [အစပ်ိဳး](#introduction)
- [Configuration](#configuration)
- [Usage](#usage)
- [Pipelining](#pipelining)

<a name="introduction"></a>
## အစပ်ိဳး

[Redis](http://redis.io) သည္ open source advanced key-value store တစ္ခုျဖစ္သည္။  ၄င္းသည္ keys မ်ားတြင္ [strings](http://redis.io/topics/data-types#strings), [hashes](http://redis.io/topics/data-types#hashes), [lists](http://redis.io/topics/data-types#lists), [sets](http://redis.io/topics/data-types#sets), and [sorted sets](http://redis.io/topics/data-types#sorted-sets) ပါဝင္ေသာေၾကာင့္  ရံဖန္ရံခါ  data structure server ဟု သတ္မွတ္ျခင္း ခံရသည္။   

> **Note:** သင့္တြင္ Redis PHP extension ကုိ PECL မွ တဆင့္ သြင္းျပီးပါက Redis အတြက္ အတုိေကာက္ အမည္ကုိ `app/config/app.php` ေၾကညာေပးရမည္။

<a name="configuration"></a>
## Configuration

Application အတြက္ Redis configuration မွာ **app/config/database.php**  အမည္ရွိ file ထဲတြင္ တည္ရွိမည္ ျဖစ္ျပီး ထုိ file ထဲတြင္  **redis** 
အမည္ရွိ array ကို application မွ အသုံးျပဳမည္ ျဖစ္သည္။


	'redis' => array(

		'cluster' => true,

		'default' => array('host' => '127.0.0.1', 'port' => 6379),

	),

default server configuration မွာ development အတြက္ ဦးတည္ထားေသာ္လည္း မိမိတုိ ့စိတ္ၾကိဳက္ ထုိ array ကိုေျပာင္းလဲ သတ္မွတ္ႏုိင္သည္။ 
ထုိ Redis server ၏ name ၊ host ႏွင့္ Server မွ အသုံးျပဳသည့္ port ကုိ ေၾကညာေပးရန္လုိေပမည္။

The `cluster` option will tell the Laravel Redis client to perform client-side sharding across your Redis nodes, allowing you to pool nodes and create a large amount of available RAM. However, note that client-side sharding does not handle failover; therefore, is primarily suited for cached data that is available from another primary data store.

If your Redis server requires authentication, you may supply a password by adding a `password` key / value pair to your Redis server configuration array.

<a name="usage"></a>
## Usage

You may get a Redis instance by calling the `Redis::connection` method:

	$redis = Redis::connection();

This will give you an instance of the default Redis server. If you are not using server clustering, you may pass the server name to the `connection` method to get a specific server as defined in your Redis configuration:

	$redis = Redis::connection('other');

Once you have an instance of the Redis client, we may issue any of the [Redis commands](http://redis.io/commands) to the instance. Laravel uses magic methods to pass the commands to the Redis server:

	$redis->set('name', 'Taylor');

	$name = $redis->get('name');

	$values = $redis->lrange('names', 5, 10);

Notice the arguments to the command are simply passed into the magic method. Of course, you are not required to use the magic methods, you may also pass commands to the server using the `command` method:

	$values = $redis->command('lrange', array(5, 10));

When you are simply executing commands against the default connection, just use static magic methods on the `Redis` class:

	Redis::set('name', 'Taylor');

	$name = Redis::get('name');

	$values = Redis::lrange('names', 5, 10);

> **Note:** Redis [cache](/docs/cache) and [session](/docs/session) drivers are included with Laravel.

<a name="pipelining"></a>
## Pipelining

Pipelining should be used when you need to send many commands to the server in one operation. To get started, use the `pipeline` command:

#### Piping Many Commands To Your Servers

	Redis::pipeline(function($pipe)
	{
		for ($i = 0; $i < 1000; $i++)
		{
			$pipe->set("key:$i", $i);
		}
	});