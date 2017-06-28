# WP Engine Cache Flush

## Purpose

### What is this?

If you host on [wpengine](https://wpengine.com/) you may be familiar with their cache system, and even more likely: their 'Purge All Caches' button:

![](http://d.pr/i/ZTLqNw/G6BK1Jg8+)

Unfortunately, WP Engine has not yet offered a programmatic way to purge the cache for your site (i.e. using a simple webhook).

I did some digging and discovered that the functionality for the WP Engine's cache purge is all within `mu-plugins` and have combine the cache purging functionality and a simple webhook request to achieve a programmatic way to clear your site's cache (object cache AND varnish full page cache).

### Why would I use this?

If you deal with any sort of deployment, build, or continuous delivery system, you know how important having a programmatic way to do everything is. In this case, clearing the cache is crucial to be able to run acceptance tests and verify that the new changes have not caused any regressions.

This clears the cache for sites hosted on WP Engine.

## Setup

### Composer
Include via composer:
```bash
composer require a7/wpe-cache-flush
```

### Private Key
Create a [private key](https://www.random.org/strings/?num=10&len=20&digits=on&upperalpha=on&loweralpha=on&unique=on&format=html&rnd=new).

Set the private key one of three ways:

#### Constant
Define the constant `WPE_CACHE_FLUSH` with they key:
```php
define( 'WPE_CACHE_FLUSH', $private_key );
```

#### Filter
Add a filter to `\A7\WPE_Cache_Flush\wpe_cache_flush_token` and return the token as a string
```php
add_filter( '\A7\WPE_Cache_Flush\wpe_cache_flush_token', function() {
  return $private_key;
} );
```

#### Environmental Variable
Set an environmental variable for `WPE_CACHE_FLUSH`
```php
putenv( 'WPE_CACHE_FLUSH=' . $private_key );
```

## Usage
Make a GET request to your site's URL with the query parameter `?wpe-cache-flush=$private_key`.
```
GET http://example.com/?wpe-cache-flush=$private_key
```

You can also call the flush function directly from your code via 
```php
\A7\WPE_Cache_Flush\cache_flush()
```
