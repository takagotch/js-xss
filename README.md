### DOMPurify
---
https://github.com/leizongmin/js-xss

```
npm install xss
bower install xss
bower install https://github.com/leizongmin/js-xss.git

xss -i <input_file> -o <output_file>
xss -i origin.html -o target.html

xss -t

```

```js
var xss = require("xss");
var html = xss('<script>alert("xss");</script>');
console.log(html);


options = {};
html = xss('<script>alert("xss");</script>', options);

options = {};
myxss = new xss.FilterXSS(options);
html = myxss.process('<script>alert("xss");</script>');

var options = {
  whiteList: {
    a: ["href", "title", "target"]
  }
};

function onTag(tag, html, options){
}

function onTagAttr(tag, name, value, isWhiteAttr){
}

function onIgnoreTag(tag, html, options){
}

funciton onIgnoreTagAttr(tag, name, value, isWhiteAttr){
}

function escapeHtml(html){
  return html.replace(/</g, "&lt;").replace(/>/g, "&gt;");
}

function escapeHtml(tag, name, value){
}

myxss = new xss.FilterXSS({
  css: {
    whiteList: {
      position: /^fixed|relative$/,
      top: true,
      left: true
    }
  }
});
html = myxss.process('<script>alert("xss");</script>');

myxss = new xss.FilterXSS({
  css: false
});

code:alert(/xss/);

var source = '<div a="1" b="2" data-a="3" data-b="4"></div>';
var html = xss(
  onIgnoreTagAttr: function(tag, name, value, isWhiteAttr){
    if(name.substr(0, 5) === "data-"){
      return name + '="' + xss.escapeAttrValue(value) + '"';
    }
  }
);
console.log("%s\nconvert to:\n%s", source, html);

var source = "<x><x-1><x-2 checked><x-2></x-1><a>";
var html = xss(
  onIgnoreTag: function(tag, html, options){
    if(tag.substr(0, 2) === "x"){
      return html;
    }
  }
);
console.log("%s\nconvert to:\n%s", source, html);

var source = 
  '<img src="img1"><img src="img2"><img src="img3"><img src="img4">';
var list = [];
var html = xss(source, {
  onTagAttr: function(tag, name, value, isWhiteAttr){
    if(tag === "img" && name === "src"){
      list.push(xss.friendlyAttrValue(value));
    }
  }
});
console.log("image list:\n%s", list.join(", "));

var source = "<strong></strong><script></script>";
var html = xss(source, {
  whiteList: [],
  stripIgnoreTag: true,
  stripIgnoreTagBody: ["script"]
});
console.log("text: %s", html);
```

```
<script src="https://rawgit.com/leizongmin/js-xss/master/dist/xss.js"></script>
<script>
  var html = filterXSS('<script>alert("xss");</src' + 'ipt>);
  alert(html);
</script>

<script>
require.config({
  baseUrl: './',
  paths: {
    xss: 'https://rawgit.com/leizongmin/js-xss/master/dist/xss.js'
  },
  shim: {
    xss: {exports: 'filterXSS'}
  }
})
require(['xss'], function(xss){
  var html = xss('<script>alert("xss");</scr; + 'ipt>');
  alert(html);
});
</script>

code:<script>alert(/xss/);</script>

<div a ="1" b="2" data-a="3" data-b="4"></div>
<div data-a="3" data-b="4"></div>
```
