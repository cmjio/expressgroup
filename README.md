# Express (Route) Grouping

[![Join the chat at https://gitter.im/edgeui/expressgroup](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/edgeui/expressgroup?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

Using underscore or lodash you can now extend your express.js application to now include route grouping.  Group routes with a prefix.  For example if you wanted to group all your API routes, you can now do so.  Have a look at the example below for how to implement.


```js
var express = require('express');
var _ = require("underscore");
var app = express();

_.extend(app, require("expressgroup")(app));

app.get("/", function(req, res){
	res.render("home");
});

app.group({prefix:"/api/v1"}, function(route){
  
  // defaults to GET method
  // this route will be available at host:port/api/v1/foo
  route({url:"/foo", callback:function(req, res){
    res.send("foo");
  }});
  
  // methods can be any of the HTTP methods commonly used
  // the route will be available at host:port/api/v1/hello
  route({method:"get", url:"/hello", callback:function(req, res){
    res.send("hello world");
  }});
  
});

app.listen(3000);
```

