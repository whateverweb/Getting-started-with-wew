# How it works
This document describes the ins and outs of whateverweb.com and how to configure applications for use on your web site.

## First, register
The rest of this document assumes that you are registered at [whateverweb.com](http://whateverweb.com) and created an application.

## Create an application
When you have registered with and account at [whateverweb.com](http://whateverweb.com), it is time to create an application. An application is "a site" or hostname from where you plan to use the services. You can have multiple applications. Each application can be configured according to your needs.

An application gives you a unique hostname to access the services on wew.io. For example `ddr.<appID>.wew.io` is the [Device Detection service](https://github.com/whateverweb/device-detection) end point.

Adding an application is pretty straight forward, you give it a name and a description for your own convenience, then there are a few important properties:

### Host name
The host name is the domain or url from which you want to use the services. For example, if your site where you want to use the services is google.com, simply input google.com as hostname.

#### Security
The hostname is the basis for access control and security. 

NOTE:
All services are pretty laid back on security. For example, there is no restrictions to where the source files can be located. E.g. you can pull css files or image files through the services from cnn.com even if your hostname is google.com.

A basis for our services is [CORS](http://en.wikipedia.org/wiki/Cross-origin_resource_sharing). Where CORS is not applicable Host or Referrer HTTP headers are used. These are evaluated against the hostname registered with the app.

If debug mode is turned on all origins.

### Alias
By default, your application get a generated ID. You can define an alias to prelace this ID. So instead of `ddr.alongandcrypticstringhere.wew.io` you get `ddr.myapp.wew.io`.

####CNAME
An alternative to alias is CNAME. If you can manage your DNS entries you can define your own CNAME to point to your application. E.g. instead of using `ddr.myapp.wew.io` you can define `myapp.yourdomain.com` point to your Device Detection service. Each service can be separately CNAME-ed, or you can use this scheme (In your DNS config, point your hostname to myapp.wew.io):

* `myapp.yourdomain.com/ddr` for Device Detection service
* `myapp.yourdomain.com/css` for CSS processor
* `myapp.yourdomain.com/img` for image scaling
* `myapp.yourdomain.com` for static content published with git.

### Debug mode
An application can be put in debug mode. This is useful during testing, development and debugging. When debug mode is turned on:

* CSS- and JavaScript files will not be minified and compressed.
* Access control is turned off. (Your applications URLs can be used from anywhere, not limited to what you defined in hostname)

### Customize Device Detection Service
The Device detection service allows some customization.
#### Custom device capabilities
You can't add new devices or User-Agents to the device database, but you can add custom capabilities to existing devices. The custom capabilities will only be available for the current application ID. 
#### Capability sets
The device database contains hundreds of capabilities. However, just a handful of them might be what you need. In this case you can add your favorite capabilities to a set with a specified name. These capabilities is now just a REST call away. Custom made capabilities can also be added to a set. 
### Git publishing
A git repository comes with the application. This is an alternative way to utilize the services for image scaling and CSS processor. Simply push your files to the repository, and the files are available through http on your service URL: `yourAlias.wew.io`. Only static content, such as CSS, JavaScript, images, html etc. can be stored here. No server side programming language is available.
Further, whey files are pushed, a few hooks can be enabled: Automatic compression of JavaScript files, optimizing of images (removing exif data etc.) and preprocessing of SASS files.

#### SSH key
To utilize git publishing, you must be authenticated with your public ssh key.

### Disabling or deleting an application
If an application is disabled, all requests are discarded. The application can re-enabled anytime.
 
Deleting an application will erase all information.

## Cache and proxy strategy
### Application config
The configuration of an application is cached for 1 minute. That means that after you make a change to an application, i.e. turn on or off debug mode, it may take up to one minute before the change is live.
### External files
When you are referring to a file `http://css.demo.wew.io/http://demo.wew.io/styles/style.css` the CSS processor service will cache the file `http://demo.wew.io/styles/style.css` according to its HTTP headers. If the service is not behaving as expected, check that the `Expires`,`Last-Modified`,`Cache-Control`,`ETag` and the usual suspects.

Same goes for the image scaling service.


## Documentation
The official documentation for each service are located on [github.com/whateverweb](https://github.com/whateverweb/):

* [Device Detection Service](https://github.com/whateverweb/device-detection)
* [CSS processor](https://github.com/whateverweb/CSS-processor)
* [Image Server](https://github.com/whateverweb/Image-Server)
* [Git publishing](https://github.com/whateverweb/git-publishing)

## License
[MIT](http://opensource.org/licenses/MIT) is the license for all example code provided.
## Bugs and Issues
If you encounter bugs, issues, improvements or have general suggestions, submit an issue under the respective repository.


