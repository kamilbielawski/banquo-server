# Banquo server

Banquo server is a Node Express.js server set to run the [Banquo](http://github.com/mhkeller/banquo) library as a service.

### Installation

`git clone` the repo onto your server.

Run

`cd banquo-server && npm install`

### Configuring

You have the option of uploading a `png` to S3 in addition to returning it as a base64 encoded string. To do this, fill out the fields in `s3_config.json`.


### Starting the service

Install Forever
````
npm install -g forever
````

`cd` to `banquo server` directory.

Start the server, default is port 3000
`forever start app.js`


### Using the service

<<<<<<< HEAD
Let's say your server lives at `banquo.com`, the call has the following stucture:
````
http://banquo.com:3000/:url/:options
````

So

````
banquo.com:3000/america.aljazeera.com/viewport_width=1000&delay=1000&selector=#map-canvas&css_hide=.map-zoom`
````

That won't quite work, though, make sure you wrap your options with [`encodeURIComponent()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/encodeURIComponent).

A full client set up would look something like this:

````
var url = 'america.aljazeera.com',
		options = 'viewport_width=1000&delay=1000&selector=#map-canvas&css_hide=.map-zoom';

function sendScreenshot(url, options){
	return $.ajax({
		url: 'http://banquo.com:3000/' + encodeURIComponent(url) + '/' + encodeURIComponent(options),
    dataType: 'JSONP',
    callback: 'callback'
	});
=======
Let's say your server lives at `banquo.com`, you pass your percent-encoded options in through the URL hash such as:
````
banquo.com:3000/mode=save&url=america.aljazeera.com&viewport_width=2400&delay=1000&selector=%23map-canvas&css_hide=.map-zoom&out_file=map.png
````
>>>>>>> f89cbe7432451995dc11f815bd78bff4f6fef067

}

sendScreenshot(url, options)
	.done(function(response){
		console.log(response.image_data, response.timestamp);
	})
	.fail(function(err){
		console.log(err);
	})

````

Or, if you want to be fancy, store your options as an object and write a function that converts them to a `&` delimited string. But how you set up the client is whatever makes sense for you.

These are your options that you can pass to Banquo.

Key | Options | Description
--- | --- | ---
url | *String* | The website you want to screenshot.
viewport_width | *Number (pixels)* | The desired browser width.
delay | *Number (milliseconds)* | How long to wait after the page has loaded before taking the screenshot. PhantomJS apparently waits for the page to load but if you have a map or other data calculations going on, you'll need to specify a wait time.
selector | *Percent-encoded CSS selector* | The div you want to screenshot. Defaults to 'body' if not specified.
css_hide | *Percent-encoded CSS selector* | Any divs you want to hide, such as zoom buttons on map. Defaults to none.
<<<<<<< HEAD

### The response

Your Banquo Server should now be returning you a JSONP response of image data and a UNIX timestamp. The timestamp is useful if you've uploaded the image to S3 since it will bake out the image with the following format name: `screenshot-1383626366826.png'


### Contact

Any questions? Contact me here:

michael.keller@aljazeera.net
[@mhkeller](http://twitter.com/mhkeller)

Pull requests welcome.
=======
out_file | *String* | For `save` mode, the name of the file to write.
>>>>>>> f89cbe7432451995dc11f815bd78bff4f6fef067
