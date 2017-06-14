# WP Engine Cache Flush

Adds a programmatic way to flush the cache on your WP Engine site.

![](http://d.pr/i/ZTLqNw/G6BK1Jg8+)

## Setup

### Composer
Include via composer:
```bash
composer require a7/wpe-cache-flush
```

Create a [private key](https://www.random.org/strings/?num=10&len=20&digits=on&upperalpha=on&loweralpha=on&unique=on&format=html&rnd=new).

Set the private key one of three ways:

### Constant
Define the constant `WPE_CACHE_FLUSH` with they key:
```php
define( 'WPE_CACHE_FLUSH', $private_key );
```

### Filter
Add a filter to `\A7\WPE_Cache_Flush\wpe_cache_flush_token` and return the token as a string
```php
add_filter( '\A7\WPE_Cache_Flush\wpe_cache_flush_token', function() {
  return $private_key;
} );
```

### Environmental Variable
Set an environmental variable for `WPE_CACHE_FLUSH`
```php
putenv( 'WPE_CACHE_FLUSH=' . $private_key );
```

## Usage
Make a GET request to your site's URL with the query parameter `?wpe-cache-flush=$private_key`.
```
GET http://example.com/?wpe-cache-flush=$private_key
```
