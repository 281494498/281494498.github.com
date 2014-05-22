---
layout: page
title: Welcome here!
tagline: Growth record about Zugzug.de
---
{% include JB/setup %}

##from “I don’t care about performance, I just want it to work” to “thousands of people could be playing simultaneously, how do I scale?”

##Project in May
=========
###using HTML template to generate pages
- Like using [EJS](http://embeddedjs.com/), but it is just too simple to use, not recommeded by `single page web application p207`
- using handlerbar.js(mustache.js), it cost about 120k, but with [hogan.js](http://twitter.github.io/hogan.js/), it only cost 2.5k 
- last very popular way is to use jadeJs, which is defaultly embedded into node.js, also be supported natively by webstorm

###Markdown is a good language to simply write something
- markdown file is the most used text file in github,  which has a suffix of `md`
- [Wikipedia](http://zh.wikipedia.org/wiki/Markdown) and [Github](https://help.github.com/articles/markdown-basics) have clear explanation, plus there are quick introduction [here](http://jianshu.io/p/q81RER)

###Connect to MongoDB
- It is very convenient to connect to it in Heroku's control panel
- Use Robomongo to access to it, here is a good [tutorial](http://scotch.io/quick-tips/mongodb/connecting-to-mongodb-using-robomongo).
- There is `_v` in mongodb database, which means version key [explanation](http://aaronheckmann.tumblr.com/post/48943525537/mongoose-v3-part-1-versioning)
	The version key is only incremented after operations that could cause a conflict, modifying array positions. Other updates won't increment it.

###Build Express module to support Auth
- Mainly according to the tutorial [here](http://scotch.io/tutorials/javascript/easy-node-authentication-setup-and-local)
- Where I need to install body-parser from `npm install`, but here is a [article](http://andrewkelley.me/post/do-not-use-bodyparser-with-express-js.html) says it may be create too much temp files.
- Maybe you should not use body-parser anymore due to [safty reason](http://stackoverflow.com/questions/20228203/how-to-get-post-fields-in-express-without-using-bodyparser-middleware)
- express-flash:define a flash message and render it without redirecting the request, require session and cookie-parser, which is just a flash show the info add to the screen, like formerlly you hide something and then it occurs, one difference in express4.0 is req.flash() (just use sessions: req.session.messages = `['foo']` or similar).  I have thought about useing socket.io instead, but actually this flash use messages stored in `session`
- bcrypt-nodejs [API](https://www.npmjs.org/package/bcrypt-nodejs).bcrypt是一个跨平台的文件加密工具。由它加密的文件可在所有支持的操作系统和处理器上进行转移。它的口令必须是8至56个字符，并将在内部被转化为448位的密钥。然而，所提供的所有字符都具有十分重要的意义。密码越强大，您的数据就越安全。

###Passport Js
**authentication and authorization**
authentication 仅仅是认证是本人  authorization 是授权可以做本人做的任何事

- 一旦认证成功，session将被建立，cookie将保存在客户端
- Each subsequent request will not contain credentials, but rather the unique cookie that identifies the session. In order to support login sessions, Passport will `serialize` and `deserialize` user instances to and from the session.之后的请求将都不会被要求认证，而是直接利用保存在客户端的cookie来确认身份，为了支持session，服务器端需要serialize and deserialize某些特定信息来确认是那一个用户（已认证成功的），‘’
	- passport.serializeUser(function(user, done) {
	  done(null, user.id);
	});

	passport.deserializeUser(function(id, done) {
	  User.findById(id, function(err, user) {
	    done(err, user);
	  });
	});

When Passport authenticates a request, it parses the credentials contained in the request. It then invokes the verify callback with those credentials as arguments, in this case username and password. If the credentials are valid, the verify callback invokes done to supply Passport with the user that authenticated.
	return done(null, user);

Here is a great [stackoverflow answer](http://stackoverflow.com/questions/15711127/express-passport-node-js-error-handling) on error handling. It explains how to use done() and how to be more specific with your handling of a route.

#####some problems:
[how to signup with detailed information??](http://stackoverflow.com/questions/11784233/using-passportjs-how-does-one-pass-additional-form-fields-to-the-local-authenti)

[how to make html as response without the index.html on the link path??](http://expressjs.com/api.html#app.engine)

	app.get('/', function(req,res) {
	  res.sendfile('public/index.html');
	});

###process.nextTick()
	On the next loop around the event loop call this callback. This is not a simple alias to setTimeout(fn, 0), it's much more efficient
，process.nextTick()的意思就是定义出一个动作，并且让这个动作在下一个事件轮询的时间点上执行。防止了一些情况下因为时间顺序导致的一些动作已经执行完，下面的被忽略的情况，[这里](http://www.cnblogs.com/lengyuhong/archive/2013/03/31/2987745.html)的例子很好

###Express.render and sender

###Use Handlebars as html template in Express
- use `npm install handlerbars --save` to install it
- use `npm install consolidate --save` to install consolidate, where in express official API doc has recommended.

	Some template engines do not follow this convention, the consolidate.js library was created to map all of node's popular template engines to follow this convention, thus allowing them to work seemlessly within Express.

then in our server.js

	var engines = require('consolidate');
	app.set('view engine', 'html')
	app.engine('html', engines.handlebars, function(err, html) {
	    if (err) throw err;
	    console.log("successful load handlebars engine");
	});
	//or direct use 
	//app.engine('html', engines.handlebars);

here is a good [tutorial](http://expressjs-book.com/forums/topic/how-to-use-alternative-non-jade-template-engines-with-express/)

=======
###How to use key value map in javascript
No standard method available. You need to iterate and you can create a simple helper:

	Object.prototype.getKeyByValue = function( value ) {
	    for( var prop in this ) {
	        if( this.hasOwnProperty( prop ) ) {
	             if( this[ prop ] === value )
	                 return prop;
	        }
	    }
	}
	
	var test = {
	   key1: 42,
	   key2: 'foo'
	};
	
	test.getKeyByValue( 42 );  // returns 'key1'
	
One word of caution: Even if the above works, its generally a bad idea to extend any host or native object's .prototype. I did it here because it fits the issue very well. Anyway, you should probably use this function outside the .prototype and pass the object into it instead.

Another way is illustrate in this basic [article](http://mckoss.com/jscript/object.htm)  

	var associativeArray = {};
	associativeArray["one"] = "First";
	associativeArray["two"] = "Second";
	associativeArray["three"] = "Third";

###Express Page 404 Error Handling

basically 

	app.use(function(req, res, next){
	  res.status(404);

	  // respond with html page
	  if (req.accepts('html')) {
	    res.render('404', { url: req.url });
	    return;
	  }

	  // respond with json
	  if (req.accepts('json')) {
	    res.send({ error: 'Not found' });
	    return;
	  }

	  // default to plain-text. send()
	  res.type('txt').send('Not found');
	});

For more detail on 500 and so on see [here](https://github.com/visionmedia/express/blob/master/examples/error-pages/index.js)

###My questions about [comparison bewteen HTTP protocal and web socket](http://stackoverflow.com/questions/23642778/http-post-and-socket-io)

###Express req.locals
Response local variables are scoped to the request, thus only available to the view(s) rendered during that request / response cycle, if any. Otherwise this API is identical to app.locals.

This object is useful for exposing request-level information such as the request pathname, authenticated user, user settings etcetera.

	app.use(function(req, res, next){
	  res.locals.user = req.user;
	  res.locals.authenticated = ! req.user.anonymous;
	  next();
	});

###Ligth box & Fancy box  
use light box for some simple modal (min 9kb)  
while fancy box is suitable for image gallery because it could use mouse wheel to wheel over the pictures.(min 23kb)  
Here we may use [leanModal](http://leanmodal.finelysliced.com.au/) totally instead of lightbox, coz it is only 1kb :)  

