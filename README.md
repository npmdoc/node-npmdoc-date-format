# api documentation for  [date-format (v1.1.0)](https://github.com/nomiddlename/date-format#readme)  [![npm package](https://img.shields.io/npm/v/npmdoc-date-format.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-date-format) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-date-format.svg)](https://travis-ci.org/npmdoc/node-npmdoc-date-format)
#### Formatting Date objects as strings since 2013

[![NPM](https://nodei.co/npm/date-format.png?downloads=true)](https://www.npmjs.com/package/date-format)

[![apidoc](https://npmdoc.github.io/node-npmdoc-date-format/build/screenCapture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-date-format_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-date-format/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-date-format/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-date-format/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "Gareth Jones",
        "email": "gareth.nomiddlename@gmail.com"
    },
    "bugs": {
        "url": "https://github.com/nomiddlename/date-format/issues"
    },
    "dependencies": {},
    "description": "Formatting Date objects as strings since 2013",
    "devDependencies": {
        "eslint": "^3.12.0",
        "eslint-plugin-import": "^2.2.0",
        "eslint-plugin-mocha": "^4.8.0",
        "mocha": "^3.2.0",
        "should": "^11.1.2"
    },
    "directories": {},
    "dist": {
        "shasum": "be7df68ec270fd9ec78482bd85be68c8fb8fbebc",
        "tarball": "https://registry.npmjs.org/date-format/-/date-format-1.1.0.tgz"
    },
    "engines": {
        "node": ">=4.0"
    },
    "gitHead": "bf59015ab6c9e86454b179374f29debbdb403522",
    "homepage": "https://github.com/nomiddlename/date-format#readme",
    "keywords": [
        "date",
        "format",
        "string"
    ],
    "license": "MIT",
    "main": "lib/index.js",
    "maintainers": [
        {
            "name": "csausdev",
            "email": "gareth.jones@sensis.com.au"
        }
    ],
    "name": "date-format",
    "optionalDependencies": {},
    "readme": "ERROR: No README data found!",
    "repository": {
        "type": "git",
        "url": "git+https://github.com/nomiddlename/date-format.git"
    },
    "scripts": {
        "lint": "eslint lib/* test/*",
        "pretest": "eslint lib/* test/*",
        "test": "mocha"
    },
    "version": "1.1.0"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module date-format](#apidoc.module.date-format)
1.  [function <span class="apidocSignatureSpan">date-format.</span>asString (format, date, timezoneOffset)](#apidoc.element.date-format.asString)
1.  string <span class="apidocSignatureSpan">date-format.</span>ABSOLUTETIME_FORMAT
1.  string <span class="apidocSignatureSpan">date-format.</span>DATETIME_FORMAT
1.  string <span class="apidocSignatureSpan">date-format.</span>ISO8601_FORMAT
1.  string <span class="apidocSignatureSpan">date-format.</span>ISO8601_WITH_TZ_OFFSET_FORMAT



# <a name="apidoc.module.date-format"></a>[module date-format](#apidoc.module.date-format)

#### <a name="apidoc.element.date-format.asString"></a>[function <span class="apidocSignatureSpan">date-format.</span>asString (format, date, timezoneOffset)](#apidoc.element.date-format.asString)
- description and source-code
```javascript
function asString(format, date, timezoneOffset) {
    if (typeof format !== 'string') {
        timezoneOffset = date;
        date = format;
        format = module.exports.ISO8601_FORMAT;
    }
    if (!date) {
        date = new Date();
    }
  // make the date independent of the system timezone by working with UTC
    if (timezoneOffset === undefined) {
        timezoneOffset = date.getTimezoneOffset();
    }

    date.setUTCMinutes(date.getUTCMinutes() - timezoneOffset);
    var vDay = addZero(date.getUTCDate());
    var vMonth = addZero(date.getUTCMonth() + 1);
    var vYearLong = addZero(date.getUTCFullYear());
    var vYearShort = addZero(date.getUTCFullYear().toString().substring(2, 4));
    var vYear = (format.indexOf('yyyy') > -1 ? vYearLong : vYearShort);
    var vHour = addZero(date.getUTCHours());
    var vMinute = addZero(date.getUTCMinutes());
    var vSecond = addZero(date.getUTCSeconds());
    var vMillisecond = padWithZeros(date.getUTCMilliseconds(), 3);
    var vTimeZone = offset(timezoneOffset);
    date.setUTCMinutes(date.getUTCMinutes() + timezoneOffset);
    var formatted = format
    .replace(/dd/g, vDay)
    .replace(/MM/g, vMonth)
    .replace(/y{1,4}/g, vYear)
    .replace(/hh/g, vHour)
    .replace(/mm/g, vMinute)
    .replace(/ss/g, vSecond)
    .replace(/SSS/g, vMillisecond)
    .replace(/O/g, vTimeZone);
    return formatted;
}
```
- example usage
```shell
...
'''

usage
=====

'''js
var format = require('date-format');
format.asString(); //defaults to ISO8601 format and current date.
format.asString(new Date()); //defaults to ISO8601 format
format.asString('hh:mm:ss.SSS', new Date()); //just the time
'''

or

'''js
...
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
