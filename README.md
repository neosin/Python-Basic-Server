# Python-Basic-Server
This is a useful tool I think for Kiosk applications on Raspberry PI

### Requires Python 3.7+

### Expanded from:
https://gist.github.com/earonesty/ab07b4c0fea2c226e75b3d538cc0dc55

This tool sets up a basic framework for a web application one might use on a small device like a Raspberry PI.

This could be done using Node.js of course however, my current boss was already working in Python so I am as well.

I went ahead and included jQuery mostly because I had an Ajax closure I like to use and didn't feel like reinventing the wheel. To lighten things up even more it's of course entirely possible to use vanilla JS.

The Python side can grab and export an HTML file from a folder to server however I mostly am just thinking that this is a scaffolding for JS to build based on JSON via AJAX. I may build in a system to retrieve HTML template files.

The CSS and JS files are loaded through their own routes. There can be only one of each currently so it makes sense to use Grunt to combine all your files (included).

* NOTE * - Compass is also included to compile SASS.

The program allows for GET and POST however currently I have it setup so that GET is simply used to call the methid and POST is for the actual data.

Example:
```javascript
// jquery ready
$(document).ready(function(){
  // click event
	$('#ajaxtest').on('click',function(){
    // call the method 'test' with a variable 'name'
		Ajax.get('test',{
			name:$('#ajaxtext').val()
		},function(data) {
      // on success the result is returned from the server
			$('#response').html(data);
		});
	});
}); 
```
On error an alert will be thrown with the response from the server

### Starting the server
Currently the server is set to port 35730

You can change this in apiserver.py on the last line:
```python
MyServer("127.0.0.1",35730).serve_forever()
```

![alt text](https://raw.githubusercontent.com/061375/Python-Basic-Server/master/images/p-server-screen.jpg)

Here's a basic rundown of the events. Note that the CSS and Javascript load via the AJAX portal by essentially the same method as any other request however, these special cases can be called from HTML through the /js and /css routes.

![alt text](https://raw.githubusercontent.com/061375/Python-Basic-Server/master/images/p-server-flow.png)
