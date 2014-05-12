---
layout: page
title: Welcome here!
tagline: Growth record about Zugzug.de
---
{% include JB/setup %}

##Project in May
---------------
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

###process.nextTick()
	On the next loop around the event loop call this callback. This is not a simple alias to setTimeout(fn, 0), it's much more efficient
，process.nextTick()的意思就是定义出一个动作，并且让这个动作在下一个事件轮询的时间点上执行。防止了一些情况下因为时间顺序导致的一些动作已经执行完，下面的被忽略的情况，[这里](http://www.cnblogs.com/lengyuhong/archive/2013/03/31/2987745.html)的例子很好

###Express.render and sender


emails
nasser.jazdi@ias.uni-stuttgart.de
