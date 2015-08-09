# nginx caching for vanilla/mainline dokku
===================

This is a tweak of @rummnik's `dokku-alt` plugin to work on vanilla `dokku` (tested with 0.3.22)

### Installing
```
$ cd /var/lib/dokku/plugins
$ git clone https://github.com/rummik/dokku-nginx-cache.git nginx-cache
$ dokku plugins-install
```

### Quick start

Enable nginx request caching
```
$ dokku nginx:cache:enable my-app
```

Disable nginx request caching
```
$ dokku nginx:cache:disable my-app
```

### Configuration

There are no configuration options (other than tweaking the `nginx-pre-reload` hook). And since `nginx` caches entire raw requests on disk, there might be some interesting behavior if you're used to Varnish.

`nginx` does, however, obey a number of caching- and `X-Accel-*`-related headers you can set in your app:

- `X-Accel-Expires`, `Expires`, `Cache-Control`, `Set-Cookie`, and `Vary` set
  the parameters of response [caching][];
- `X-Accel-Redirect` performs an [internal redirect][] to the specified URI;
- `X-Accel-Limit-Rate` sets the [rate limit][] for transmission of a response
  to a client;
- `X-Accel-Buffering` enables or disables [buffering][] of a response;
- `X-Accel-Charset` sets the desired [charset][] of a response.

[Nginx docs]: http://nginx.org/en/docs/http/ngx_http_proxy_module.html#proxy_ignore_headers
[caching]: http://nginx.org/en/docs/http/ngx_http_proxy_module.html#proxy_cache_valid
[internal redirect]: http://nginx.org/en/docs/http/ngx_http_core_module.html#internal
[rate limit]: http://nginx.org/en/docs/http/ngx_http_core_module.html#limit_rate
[buffering]: http://nginx.org/en/docs/http/ngx_http_proxy_module.html#proxy_buffering
[charset]: http://nginx.org/en/docs/http/ngx_http_charset_module.html#charset
