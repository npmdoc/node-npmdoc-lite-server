# api documentation for  [lite-server (v2.3.0)](https://github.com/johnpapa/lite-server#readme)  [![npm package](https://img.shields.io/npm/v/npmdoc-lite-server.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-lite-server) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-lite-server.svg)](https://travis-ci.org/npmdoc/node-npmdoc-lite-server)
#### Lightweight development node server for serving a web app, providing a fallback for browser history API, loading in the browser, and injecting scripts on the fly.

[![NPM](https://nodei.co/npm/lite-server.png?downloads=true)](https://www.npmjs.com/package/lite-server)

[![apidoc](https://npmdoc.github.io/node-npmdoc-lite-server/build/screen-capture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-lite-server_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-lite-server/build..beta..travis-ci.org/apidoc.html)

![package-listing](https://npmdoc.github.io/node-npmdoc-lite-server/build/screen-capture.npmPackageListing.svg)



# package.json

```json

{
    "bin": {
        "lite-server": "./bin/lite-server"
    },
    "bugs": {
        "url": "https://github.com/johnpapa/lite-server/issues"
    },
    "contributors": [
        {
            "name": "John Papa",
            "email": "john@johnpapa.net"
        },
        {
            "name": "Christopher Martin",
            "email": "cgmartin@gmail.com"
        }
    ],
    "dependencies": {
        "browser-sync": "^2.18.5",
        "connect-history-api-fallback": "^1.2.0",
        "connect-logger": "0.0.1",
        "lodash": "^4.11.1",
        "minimist": "1.2.0"
    },
    "description": "Lightweight development node server for serving a web app, providing a fallback for browser history API, loading in the browser, and injecting scripts on the fly.",
    "devDependencies": {
        "eslint": "^2.8.0",
        "istanbul": "^0.4.3",
        "mocha": "^3.2.0",
        "mockery": "^1.6.2",
        "sinon": "^1.17.3"
    },
    "directories": {},
    "dist": {
        "shasum": "5b4cc8f5d5fd4836105480ab2ac48a3a0de2b0c8",
        "tarball": "https://registry.npmjs.org/lite-server/-/lite-server-2.3.0.tgz"
    },
    "gitHead": "9d0a040858e6a1f8f28a899750e1b8f9754d0814",
    "homepage": "https://github.com/johnpapa/lite-server#readme",
    "keywords": [
        "angular",
        "spa",
        "static",
        "server",
        "development"
    ],
    "license": "MIT",
    "main": "index.js",
    "maintainers": [
        {
            "name": "johnpapa",
            "email": "john@johnpapa.net"
        }
    ],
    "name": "lite-server",
    "optionalDependencies": {},
    "readme": "ERROR: No README data found!",
    "repository": {
        "type": "git",
        "url": "git+https://github.com/johnpapa/lite-server.git"
    },
    "scripts": {
        "test": "eslint *.js lib/*.js && istanbul cover _mocha -- -R spec"
    },
    "version": "2.3.0"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module lite-server](#apidoc.module.lite-server)
1.  [function <span class="apidocSignatureSpan">lite-server.</span>server (opts, cb)](#apidoc.element.lite-server.server)
1.  object <span class="apidocSignatureSpan">lite-server.</span>defaults



# <a name="apidoc.module.lite-server"></a>[module lite-server](#apidoc.module.lite-server)

#### <a name="apidoc.element.lite-server.server"></a>[function <span class="apidocSignatureSpan">lite-server.</span>server (opts, cb)](#apidoc.element.lite-server.server)
- description and source-code
```javascript
function start(opts, cb) {
  opts = opts || {};
  opts.argv = opts.argv || process.argv;
  opts.console = opts.console || console;
  cb = cb || function noop() { };

  // Load configuration
  var argv = require('minimist')(opts.argv.slice(2));
  var bsConfigName = argv.c || argv.config || 'bs-config';

  // Load optional browser-sync config file from user's project dir
  var bsConfigPath = path.resolve(bsConfigName);
  var overrides = {};
  try {
    overrides = require(bsConfigPath);
  } catch (err) {
    if (err.code && err.code === 'MODULE_NOT_FOUND') {
      logMissingConfigFile();
    } else {
      throw (err);
    }
  }

  // Set optional baseDir
  config.server.baseDir = argv.baseDir || config.server.baseDir;

  if (typeof overrides === 'function') {
    overrides = overrides(browserSync);
  }

  _.merge(config, overrides);

  // Fixes browsersync error when overriding middleware array
  if (config.server.middleware) {
    config.server.middleware = _.compact(config.server.middleware);
  }

  logConfig();

  // Run browser-sync
  browserSync.init(config, cb);

  return browserSync;

  function logEnabled() {
    return config.logLevel !== 'silent';
  }

  function logConfig() {
    if (logEnabled()) {
      opts.console.log('** browser-sync config **');
      opts.console.log(config);
    }
  }

  function logMissingConfigFile() {
    if (logEnabled()) {
      opts.console.info(
        'Did not detect a 'bs-config.json' or 'bs-config.js' override file.' +
        ' Using lite-server defaults...'
      );
    }
  }

}
```
- example usage
```shell
n/a
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
