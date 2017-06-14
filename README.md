# WP Engine Cache Flush

Adds a programmatic way to flush the cache on your WP Engine site.

## Setup
To use, you must first set a private key by either:
* set the `WPE_CACHE_FLUSH` constant in `wp-config.php`
* add a filter to `\A7\WPE_Cache\Flush\wpe_cache_flush_token` and return the token as a string
* set an environmental variable for `WPE_CACHE_FLUSH`

## Usage
Simply hit your site and append the query parameter `?wpe-cache-flush=%token%` where the token is the same token you specified earlier.