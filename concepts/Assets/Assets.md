# Assets

### 静态文件

Assets 参考静态文件 [static files](http://en.wikipedia.org/wiki/Static_web_page) (js, css, images, etc) on your server that you want to make accessible to the outside world. In Sails, these files are placed in the [`assets/`]() directory, where they are processed and synced to a hidden temporary directory ([`.tmp/public/`]()) when you lift your app. The contents of this [`.tmp/public`]() folder are what Sails actually serves - roughly equivalent to the "public" folder in [express](http://www.expressjs.com), or the "www" folder you might be familiar with from other web servers like Apache.  This middle step allows Sails to prepare/pre-compile assets for use on the client - things like LESS, CoffeeScript, SASS, spritesheets, Jade templates, etc.

### 静态中间件

Behind the scenes, Sails uses the [static middleware](http://www.senchalabs.org/connect/static.html) from Express to serve your assets. You can configure this middleware (e.g. cache settings) in [`/config/express.js`]().

##### `index.html`
Like most web servers, Sails honors the `index.html` convention.  For instance, if you create `assets/foo.html` in a new Sails project, it will be accessible at [`http://localhost:1337/foo.html`]().  But if you create `assets/foo/index.html`, it will be available at both [`http://localhost:1337/foo/index.html`]() and [`http://localhost:1337/foo`]().

##### 优先级
It is important to note that the static [middleware](http://stephensugden.com/middleware_guide/) is installed **after** the Sails router.  So if you define an [explicit route](), but also have a file in your assets directory with a conflicting path, the explicit route will intercept the request before it reaches the static middleware. For example, if you create `assets/index.html`, with no routes defined in your [`config/routes.js`]() file, it will be served as your home page.  But if you define an explicit route, `'/': 'FooController.bar'`, that route will take precedence.


<docmeta name="uniqueID" value="Assets220313">
<docmeta name="displayName" value="Assets">

