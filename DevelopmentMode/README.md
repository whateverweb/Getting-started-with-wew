## Development mode

The development mode switch in the control panel of your whateverweb.com application enables you to easily change, develop and test your application.

When you enable development mode we reconfigure your application so that:
* URIs get a short term expiry time, typically within the minute
* service URLs are opened up, **meaning they can be used from ANY site**. This means you can even test from pages running on your local machine/server setup.
* backend resources, like source CSS and images, are refreshed more frequently
* resources published using the GIT publishing are not obscured (uglified, compressed)

#### Caveats

* You should not leave the development mode on unless you are actually in development, as it leaves your application open for everyone to eat from your transfer/access quota.
* Due to both server and client side caching, frequently changing the development mode setting might not give you the desired effect.


### Details

#### Image server

* **ON**: Images are scaled and served to pages on any host/domain. Images expire after 30 seconds.
* **OFF**: Images are scaled and served for embedding on pages, or in scripts, only on registered domain. Images expire after 7 days. ETag headers are set and checked, if possible.


#### CSS processor

* **ON**: Source CSS refreshed on each request, expires after 3 seconds. Results are not minified. All access allowed.
* **OFF**: Expires after 3 days. Access from registered host/domain only.

#### Device detection

* **ON**: All access allowed.
* **OFF**: Access only from scripts on registered host/domain.

#### Publishing

* **ON**: Javascripts are not uglified and minified. Short, or no, caching of resources both on server and client.
* **OFF**: Javascripts will be uglified and minified. Resources served will be cached by edge server and (quite) long expiry.



