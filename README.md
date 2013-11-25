# mobile-detect.js

A loose port of [Mobile-Detect](https://github.com/serbanghita/Mobile-Detect) to JavaScript.

This script will detect the device by comparing patterns against a given User-Agent string.
You can find out information about the device rendering your web page:

  * mobile or not
  * if mobile, whether phone or tablet
  * operating system
  * [Mobile Grade (A, B, C)](http://jquerymobile.com/gbs/)
  * specific versions (e.g. WebKit)


# Usage

## Browser

```html
<script src="mobile-detect.js"></script>
<script>
    var md = new MobileDetect(window.navigator.userAgent);
    // ... see below
</script>
```

## Node.js / Express

```js
var MobileDetect = require('mobile-detect'),
    md = new MobileDetect(req.headers['user-agent']);
// ... see below
```

## General

```js
var md = new MobileDetect(
    'Mozilla/5.0 (Linux; U; Android 4.0.3; en-in; SonyEricssonMT11i' +
    ' Build/4.1.A.0.562) AppleWebKit/534.30 (KHTML, like Gecko)' +
    ' Version/4.0 Mobile Safari/534.30');

// more typically we would instantiate with 'window.navigator.userAgent'
// as user-agent; this string literal is only for better understanding

console.log( md.mobile() );          // 'Sony'
console.log( md.phone() );           // 'Sony'
console.log( md.tablet() );          // null
console.log( md.userAgent() );       // 'Safari'
console.log( md.os() );              // 'AndroidOS'
console.log( md.is('iPhone') );      // false
console.log( md.is('bot') );         // false
console.log( md.version('Webkit') );         // 534.3
console.log( md.versionStr('Build') );       // '4.1.A.0.562'
console.log( md.match('playstation|xbox') ); // false
```

## More Info ...

There is some documentation generated by JSDoc:

<http://hgoebl.github.io/mobile-detect.js/doc/MobileDetect.html>

## Side Effects

Script creates the global property `MobileDetect`.

## Modernizr Extension

When using [Modernizr](http://modernizr.com/), you can include `mobile-detect-modernizr.js`.
It will add the CSS classes `mobile`, `phone`, `tablet` and `mobilegradea` if applicable.

You can easily extend it, e.g. `android`, `iphone`, etc.

## Size (bytes)

 * development: 48.170
 * minified: 24.301
 * minified + gzipped: 10.335 (`cat mobile-detect.min.js | gzip -9f | wc -c`)

# Installation

## Bower

    $ bower install hgoebl/mobile-detect.js --save

## Node.js / npm

    $ npm install mobile-detect --save

# Alternatives / Infos

Often device detection is the first solution in your mind. Please consider looking for other solutions
like media queries and feature detection (e.g. w/ Modernizr). Maybe there are better (simpler, smaller,
faster) device detection libraries, so here you have a list (order has no meaning apart from first element):

  * [Modernizr](http://modernizr.com/)
    In most cases the better solution: don't use knowledge about device and version, but detect features
    (touch, canvas, ...)
  * [Mozilla Hacks - User-Agent detection, history and checklist](https://hacks.mozilla.org/2013/09/user-agent-detection-history-and-checklist/)
  * [Mobile-Detect](https://github.com/serbanghita/Mobile-Detect)
    A lightweight PHP class for detecting mobile devices (including tablets).
    This is the "source" of this JavaScript project and if you use PHP on your server you should use it!
  * [Detect Mobile Browsers](http://detectmobilebrowsers.com/) Open source mobile phone detection in many languages
    and for Webservers (Apache, nginx, IIS). mobile-detect.js uses the code of this library as a fallback in case
    of incomplete detection regular expressions.
  * [sebarmeli / JS-Redirection-Mobile-Site](https://github.com/sebarmeli/JS-Redirection-Mobile-Site/)
    JS to handle the redirection to the mobile version of your site
  * [dmolsen/Detector](https://github.com/dmolsen/Detector)
    Detector is a simple, PHP- and JavaScript-based browser- and
    feature-detection library that can adapt to new devices & browsers
    on its own without the need to pull from a central database of browser information.
  * [matthewhudson/device.js](https://github.com/matthewhudson/device.js)
    Conditional CSS and/or JavaScript based on device operating system, orientation and type
  * [brendanlim/mobile-fu](https://github.com/brendanlim/mobile-fu)
    Automatically detect mobile requests from mobile devices in your Rails application.
  * [FormFactor](https://github.com/PaulKinlan/formfactor)
    FormFactor helps you customize your web app for different form factors, e.g. when you make
    "the mobile version", "the TV version", etc.
  * [UAParser.js](http://faisalman.github.com/ua-parser-js/)
    Lightweight JavaScript-based User-Agent String Parser
  * [MobileESP - Easily detect mobile web site visitors](http://blog.mobileesp.com/)
  * [WURFL](http://wurfl.sourceforge.net/)
  * [Handset and Tablet Detection](http://www.handsetdetection.com/)
  * [Search on microjs.com](http://microjs.com/#detect)

## Mobile-Usage Statistics

If you have to provide statistics about how many and which mobile devices are hitting your web-site, you can
generate statistics (data and views) with [hgoebl/mobile-usage](https://github.com/hgoebl/mobile-usage).
There are many hooks to customize statistical calculation to your needs.


# License

MIT-License (see LICENSE file).


# Contributing

Your contribution is welcome.
If you want new devices to be supported, please contribute to
[Mobile-Detect](https://github.com/serbanghita/Mobile-Detect) instead.

To run generate-script it is necessary to have [Mobile-Detect](https://github.com/serbanghita/Mobile-Detect)
as a sibling directory to mobile-detect.js/.
(I tried to use `git subtree` but had some problems on Mac OS X - probably my fault...)

  * fork or clone serbanghita/Mobile-Detect
  * fork hgoebl/mobile-detect.js
  * run `npm install`
  * create branch
  * make changes and run `grunt` (needs PHP >= 5.4 in your path)
  * run browser test (tests/SpecRunner.html)
  * commit, push to your branch
  * create pull request

## Testing

### Browser

Open `tests/SpecRunner.html` in different browsers.

### Node.js

    $ npm test
    $ # or
    $ grunt jasmine_node


# Donations

If you want, you can donate to [Mobile-Detect](https://github.com/serbanghita/Mobile-Detect).


# TODO

  * Extend RegEx patterns so that test passes
  * Provide a live example on gh-pages
  * Deploy on <http://cdn.jsdelivr.net/> through <https://github.com/jimaek/jsdelivr>
