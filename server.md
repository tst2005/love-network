# Server part

# Web Server

I'm trying to use NGINX with Lua support.
I have 2 choices :
 * Take [NGINX](http://nginx.org/) + [ngx_devel_kit+lua-nginx-module](http://wiki.nginx.org/HttpLuaModule#Installation) to got the Lua support.
 * Take [OpenResty](http://openresty.org/) that pack all required patch (and disable all modules what I don't need).

I choose the second way (because I planned to need more than only the Lua support).
See my "download-extract-compile-install script" : https://github.com/tst2005/resty-auto-compil/

I choose to use luajit for performance consideration.

# Web Service

I choose to try the [lusty web framework](https://github.com/Olivine-Labs/lusty/).


# Protocol

It use a RESTfull API. (with JSON, XML is not planned to be used).
The lua-cjson is recommended for performance consideration.

# Database

Nothing decided yet.
 * Maybe flat json file will be enough for testing...
 * If I need SQL engine I will use Sqlite3 as database backend.
 * If I need KeyValue engine I will use redis.


# Licenses

 * [My project](https://github.com/tst2005/love-network): MIT License
 * [NGINX](http://nginx.org/LICENSE): 2-clause BSD-like license
 * [OpenResty](http://openresty.org/#About): BSD style licenses (See [also](https://github.com/openresty/lua-nginx-module#copyright-and-license))
 * [LuaJIT](http://luajit.org/luajit.html): MIT License.
 * [Lusty](https://github.com/Olivine-Labs/lusty/blob/master/README.md): MIT License
 * lua-cjson: MIT license
 * ...
