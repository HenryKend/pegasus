# Pegasus ![Bower version](http://img.shields.io/badge/bower%20package-0.1.6-brightgreen.svg?style=flat)

> Load data while still loading other scripts

Do this

```
load json 
load script
  →  start app
```

Instead of this

```
load script
  →  start app 
    →  load json
```

Pegasus is a tiny lib (0.2 kB min/gzip) that lets you load data while loading other scripts. 

Using this technique, you can reduce the time to display data in single page apps without touching the server.

_Backbone user? See [backbone-pegasus](https://github.com/typicode/backbone-pegasus)._

## Install

```bash
$ bower install pegasus
```

## Benchmark

Average time to display data on http://typicode.github.io/pegasus

|             | jQuery only  | jQuery + Pegasus  |
|:------------|:-------------|:------------------|
|__EDGE__     | 3000 ms      | 2100 ms           |
|__3G__       | 860 ms       | 640 ms            |
|__DSL__      | 270 ms       | 230 ms            | 

See the [screenshots](http://typicode.github.io/pegasus).

_* Network Link Conditioner was used to slow down connection._

_** jQuery is used for illustration only, you can use Pegasus with any other Javascript library._

## Usage example

```html
<!-- Load (or embed) Pegasus and start request(s) before loading any other script -->
<script src="pegasus.min.js"></script>

<!-- Request will start as soon as Pegasus is loaded -->
<script>
  var request = pegasus('http://api.example.com');
</script>

<!-- Load your app lib(s) -->
<script src="jquery.js"></script>

<!-- Use the request promise to retrieve data in your app -->
<script>
  request.then(
    function(data, xhr) {
      // success - xhr.status < 400
      // do something useful like
      $('#data').text(JSON.stringify(data));
    },
    function(data, xhr) {
      // error (optional) - xhr.status >= 400
      console.error(data, xhr.status)
    }
  );
</script>
```

__Note__: The same method can be applied with any other JavaScript library (Backbone, AngularJS, ...).

__Tip__: You can also directly embed [pegasus.min.js](https://github.com/typicode/pegasus/blob/master/pegasus.min.js) into your html file to save a network call (it's smaller than the Google analytics tracking code).

## Support

All modern browsers and IE7+
