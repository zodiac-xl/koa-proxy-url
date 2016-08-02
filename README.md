# koa-proxy-url [![Build Status](https://travis-ci.org/popomore/koa-proxy.png?branch=master)](https://travis-ci.org/popomore/koa-proxy) [![Coverage Status](https://coveralls.io/repos/popomore/koa-proxy/badge.png?branch=master)](https://coveralls.io/r/popomore/koa-proxy?branch=master) 



* Proxy middleware for koa
* clone from koa-proxy 
* added: option.url support function(http){return url} to free url 
* added:option.customPath
* added:option.customHost
* added:this.callBack


---

## Install

```
$ npm install koa-proxy-url
```

## Usage

Execution order：

1. customHost
2. customPath
3. options.url (if the type of url is function) 


```
app.use(proxy({
    match: /\/proxy/,
    customHost: function (http) {
        let cutomHost = null;
        let host = http.host;
        cutomHost = host == 'test.com' ? 'custom.com' : host;
        return cutomHost;
    },
    customPath: function (http, options) {
        let path = http.path
        if (options.host == 'test.com') {
            path = '/test' + path;
        }
        return path;
    },
    url: function (http) {
        let source = httpQueryParse(http.request).source;
        if (source != undefined) {
            return source
        } else {
            return null;
        }
    },
}));
```


## LICENSE

Copyright (c) 2016 popomore. Licensed under the MIT license.