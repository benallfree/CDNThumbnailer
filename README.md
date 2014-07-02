# CDNThumbnailer

This is a fork of `shulard/cdn-thumbnailer` with `benallfree/makenv` environment support for configuration.

CDNThumbnailer is a PHP tool for dynamic image resizing. It has a fast and accurate caching subsystem and so can be used redily with CDNs.

This tool is written in **PHP 5.2** to maximize compatibility (but in a **PHP 5.3** style).

# Installation

```
"require": {
  "benallfree/cdn-thumbnailer": "1.0.*@dev"
}
```

# Configuration

## .htaccess rewrite

Add an image proxy rewrite rule to your `.htaccess` file as follows:

```
RewriteRule ^([0-9]+x[0-9]+)\/(.*)$ vendor/benallfree/cdn-thumbnailer/index.php?path=$2&format=$1 [L]
```

A full example for WordPress:

```
# BEGIN WordPress
<IfModule mod_rewrite.c>
RewriteEngine On
RewriteBase /
RewriteCond %{REQUEST_FILENAME} !sblogin
RewriteRule ^([0-9]+x[0-9]+)\/(.*)$ vendor/benallfree/cdn-thumbnailer/index.php?path=$2&format=$1 [L]
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule . /index.php
</IfModule>
# END WordPress
```

## Cache folder

CDNThumbnailer needs to know the absolute path to the cach folder it will be using.

In `makenv`, add a `CDNThumbnailer'. If your folder is named `cache` in the web root, then your `makenv` section would look like this:

```
$config = array(
  'CDNThumbnailer'=>array(
    'cache_path'=>__DIR__.'/cache'
  ),
);
```

Make sure the folder as write permissions.

That's it! You're done.

# Usage

To use CDNThumbnailer, simply prefix any image URL with `WxH` as follows:

Original URL:

`http://mysite.com/my/image/path.jpg`

Becomes:

`http://mysite.com/320x200/my/image/path.jpg`

## Security

For added security, you may want to customize the `.htaccess` rewirte rules to allow only images of predefined sizes. CDNThumbnailer will happily resize to
any dimension supplied.

# Licence

Copyright (c) 2013 **Stéphane HULARD**

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
