# Redis PHP Mock [![Build Status](https://secure.travis-ci.org/M6Web/RedisMock.png?branch=master)](http://travis-ci.org/M6Web/RedisMock)

PHP 5.3 library providing a Redis PHP mock for your tests.  

## Installation

Add this line in your `composer.json` :

```json
{
    "require": {
        "m6web/redis-mock": "~1.2"
    }
}
```

Update your vendors :

```
$ composer update m6web/redis-mock
```

## Functions

It currently mocks these Redis commands :

Redis command                                    | Description
-------------------------------------------------|------------
**DEL** *key*                                    | Deletes a key
**EXISTS** *key*                                 | Determines if a key exists
**EXPIRE** *key* *seconds*                       | Sets a key's time to live in seconds
**KEYS** *pattern*                               | Finds all keys matching the given pattern
**TTL** *key*                                    | Gets the time to live for a key
**TYPE** *key*                                   | Returns the string representation of the type of the value stored at key.
**GET** *key*                                    | Gets the value of a key
**INCR** *key*                                   | Increments the integer value of a key by one
**SET** *key* *value*                            | Sets the string value of a key
**SADD** *key* *member*                          | Adds one member to a set
**SISMEMBER** *key* *member*                     | Determines if a member is in a set
**SMEMBERS** *key*                               | Gets all the members in a set
**SREM** *key* *member*                          | Removes one member from a set
**HDEL** *key* *field*                           | Delete one hash fields
**HEXISTS** *key* *field*                        | Determines if a hash field exists
**HGET** *key* *field*                           | Gets the value of a hash field
**HGETALL** *key*                                | Gets all the fields and values in a hash
**HSET** *key* *field* *value*                   | Sets the string value of a hash field
**ZADD** *key* *score* *member*                  | Adds one member to a sorted set, or update its score if it already exists
**ZRANGE** *key* *start* *stop*                  | Returns the specified range of members in a sorted set
**ZRANGEBYSCORE** *key* *min* *max* *options*    | Returns a range of members in a sorted set, by score
**ZREM** *key* *member*                          | Removes one membner from a sorted set
**ZREMRANGEBYSCORE** *key* *min* *max*           | Removes all members in a sorted set within the given scores
**ZREVRANGE** *key* *start* *stop*               | Returns the specified range of members in a sorted set, with scores ordered from high to low
**ZREVRANGEBYSCORE** *key* *min* *max* *options* | Returns a range of members in a sorted set, by score, with scores ordered from high to low
**FLUSHDB**                                      | Flushes the database

It mocks **MULTI**, **DISCARD** and **EXEC** commands but without any transaction behaviors, they just make the interface fluent and return each command results.  
**PIPELINE** and **EXECUTE** pseudo commands (client pipelining) are also mocked.

## Usage

RedisMock library provides a factory able to build a mocked class of your Redis library that can be directly injected in your application :

```php
$factory          = new \M6Web\Component\RedisMock\RedisMockFactory();
$myRedisMockClass = $factory->getAdapterClass('My\Redis\Library');
$myRedisMock      = new $myRedisMockClass($myParameters);
```

In a simpler way, if you don't need to instanciate the mocked class with custom parameters (e.g. to easier inject the mock using Symfony config file), you can use `getAdapter` instead of `getAdapterClass` to directly create the adapter :

```php
$factory     = new \M6Web\Component\RedisMock\RedisMockFactory();
$myRedisMock = $factory->getAdapter('My\Redis\Library');
```

**WARNING !** *RedisMock doesn't implement all Redis features and commands. The mock can have undesired behavior if your parent class uses unsupported features.*

## Tests

```shell
$ curl -sS https://getcomposer.org/installer | php
$ php composer.phar install
$ ./vendor/bin/atoum
```

## Credits

Developped by the [Cytron Team](http://cytron.fr/) of [M6 Web](http://tech.m6web.fr/).  
Tested with [atoum](http://atoum.org).

## License

RedisMock is licensed under the [MIT license](LICENSE).
