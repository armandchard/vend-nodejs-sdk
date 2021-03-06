vend-js-sdk
===========

[![Gitter](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/ShoppinPal/vend-nodejs-sdk?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

Aims to provides a rich set of client-side functionality for Vend's public APIs

If you don't use nodejs, please be aware that there are still other libraries out there! Hopefully, one that works with your preferred language is already present:

1. https://github.com/pzurek/go-vend
2. https://github.com/ShoppinPal/vend-php-tools
3. https://github.com/chipwillman/VendAPI.Net
4. https://github.com/wso2-extensions/esb-connector-vend

Simple-Legal-Speak
==================

This is a labor of love. This effort is not funded, endorsed or sponsored by Vend.

This module is being written out of sheer respect for Vend's uncanny success at platformizing retail with their public API. It will hopefully help democratize access further by adding ease of use for developers. The authors of this module are not Vend employees and Vend didn't ask us to do this. Retail is a tricky/competitive space and we want to help reduce development churn, by open-sourcing pieces that allow folks to build iterative solutions. When in doubt, be sure to pay attention to the details expressed in the LICENSE file.

Who are we?
===========

ShoppinPal is a team of engineers and product guys with background in developing core systems at well-known Silicon Valley companies. We have deep expertise with Vend APIs. Several retailers use our ecommerce add-on, which works beautifully with Vend. We would love to assist you with any custom development needs that help you get the most out of Vend. We are listed in http://www.vendhq.com/expert-directory

Features
========
1. Added sample API call for fetching product
  1. requires nothing more than a subdomain/domain-prefix and basic authN for developers to start experimenting: `NODE_ENV=dev node sample.js`
  2. *always* uses promises instead of callbacks
  3. *handles* 429 response code for rate limiting by retrying as many as 3 times
2. Uses oauth for API calls.

Roadmap
=======

1. Add sample API calls for all the exposed REST endpoints at https://developers.vendhq.com/documentation/api/index.html
2. Code up a plug-&-play or drop-in utility class for OAuth w/ Vend that anyone can add to their workflow.

Usage
=====
```
// this module isn't published to NPM yet, so you have to clone it to the node_modules folder in your machine, beforehand
var vendSdk = require('vend-nodejs-sdk')({}); 

var args = vendSdk.args.products.fetch();
args.orderBy.value = 'id';
args.page.value = 1;
args.pageSize.value = 5;
args.active.value = true;

var connectionInfo = {
  domainPrefix: nconf.get('domain_prefix'),
  accessToken: nconf.get('access_token')
};

vendSdk.products.fetch(args, connectionInfo)
  .then(function(response){
    _.each(response.products, function(product){
      console.log(product.id + ' : ' + product.name);
    });
  });

```
