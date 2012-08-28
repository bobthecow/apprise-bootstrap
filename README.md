# Apprise Bootstrap

Stylish alerts for a Bootstrapped web.


### [Download today!](https://github.com/downloads/bobthecow/apprise-bootstrap/apprise-bootstrap-1.0.0.tgz)


## Using Apprise Bootstrap

Apprise requires jQuery, so make sure you've got that handy. Then add `apprise.min.js` and
`apprise-bootstrap.min.css` to your site:

```html
<link rel="stylesheet" href="css/apprise-bootstrap.min.css">
<script src="js/apprise.min.js"></script>
```

Now go wild! You can use `apprise()` anywhere you would use an `alert()`:

```html
<a href="http://google.com" onclick="apprise('You are now leaving our site');">Leave the site</a>
```

... or maybe something like this:

```html
<script>
$('a').click(function(e) {
    e.preventDefault();

    apprise('Are you sure you want to leave me?', {verify: true}, function(r) {
        if (r) {
            document.location = $(this).attr('href');
        } else {
            apprise('Phew! That was close!');
        }
    });
});
</script>
```

[Read more about Apprise](http://thrivingkings.com/read/Apprise-The-attractive-alert-alternative-for-jQuery)

[Read more about Bootstrap](http://twitter.github.com/bootstrap/)


## Custom builds

You can include Apprise Bootstrap in your custom Bootstrap build. Simply `@include` it at the bottom of your
`bootstrap.less` file:

```css
/*!
 * Bootstrap v2.1.0
 *
 * Copyright 2012 Twitter, Inc
 * Licensed under the Apache License v2.0
 * http://www.apache.org/licenses/LICENSE-2.0
 *
 * Designed and built with all the love in the world @twitter by @mdo and @fat.
 */

// CSS Reset
@import "reset.less";

// Core variables and mixins
@import "variables.less"; // Modify this for custom colors, font-sizes, etc
@import "mixins.less";

...

// Apprise Bootstrap
@import "path/to/apprise-bootstrap.less";
```


## Legal stuffs

 * Apprise Bootstrap is copyright 2012 Justin Hileman and released under the Apache License, Version 2.0.
 * Apprise is copyright Daniel Raftery. [License info is pending](https://github.com/ThrivingKings/Apprise/issues/17).
 * Bootstrap is copyright 2012 Twitter, Inc. and released under the Apache License, Version 2.0.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this work except in compliance with the License.
You may obtain a copy of the License in the LICENSE file, or at:

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.