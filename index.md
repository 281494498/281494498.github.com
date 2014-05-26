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

###My questions about 
[comparison bewteen HTTP protocal and web socket](http://stackoverflow.com/questions/23642778/http-post-and-socket-io)

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

###JavaScript understanding

###Funtion overloading
	for(var prop in obj){
		obj[prop] = i //set the key value property pari for "prop: i"
	}

Check if a argument is offered by 
If(parameter === undefined)

arguments used for present all the input variable of a function.

It is a array, which is using by arguments[i]

####hasOwnProperty()

Which could be used for check the property in the object, but not the prototyped property.

###The difference between setInterval() and setTimeout() is large.
Should remember to use these two method to make asynchronous loading and heavy processing.

The HTML5 attribute async and defer only affect to asychronous downloading

But not affect to the asynchronous loading

###Full page animation fullpage.js
	Overwriting [fullPage](https://github.com/alvarotrigo/fullPage.js).js tooltip color

	.fullPage-tooltip{
		color: #AAA;
	}
	#fullPage-nav span, .fullPage-slidesNav span{
		border-color: #AAA;
	}
	#fullPage-nav li .active span, .fullPage-slidesNav .active span{
		background: #AAA;
	}

here is CSS way to hidden scrollbar

	.outer{
	    position: absolute;
	    bottom: 0;
	    top:0;
	    width: 100%;
	    overflow: hidden;
	}
	.inner{
	    width: 100%;
	    height: 100%;
	    padding-right: 15px;
	    overflow: scroll;
	}
see examples on [jsfiddle](http://jsfiddle.net/uB6Dg/1/) here

###URI.JS
learn it maybe for the further use
=======
But not affect to the asynchronous loading,

###Difference between slice and substring
Notes on substring():

If start equals stop, it returns an empty string.
If stop is omitted, it extracts characters to the end of the string.
If start > stop, then substring will swap those 2 arguments.
If either argument is greater than the string's length, either argument will use the string's length.
If either argument is less than 0 or is NaN, it is treated as if it were 0.
Notes on slice():

If start equals stop, it returns an empty string, exactly like substring().
If stop is omitted, slice extracts chars to the end of the string, exactly like substring().
If start > stop, slice() will NOT swap the 2 arguments.
If either argument is greater than the string's length, either argument will use the string's length, exactly like substring().
If start is negative, slice() will set char from the end of string, exactly like substr() in Firefox. This behavior is observed in both Firefox and IE.
If stop is negative, slice() will set stop to: (string.length – 1) – Math.abs(stop) (original value).

In short, that is
-slice和substring在正确使用的情况下用法相同
-substring 会自动转换错误的前后顺序，会自动调整超出的范围，slice也会调整，但是遇到`负数`的情况，会有特殊处理。即从后往前数。
