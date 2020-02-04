---
title: javascript
categories: 
 - javascript
tags: 
 - javascript
toc: true
---

### pass data to js file via script tag

```javascript
<script type="text/javascript" data-my_var_1="some_val_1" data-my_var_2="some_val_2" src="/js/somefile.js"></script>
...
var this_js_script = $('script[src*=somefile]')
var my_var_1 = this_js_script.attr('data-my_var_1');
if (typeof my_var_1 === "undefined" ) {
   var my_var_1 = 'some_default_value';
}

<script type="text/javascript" data-colCount="<?=$colorCount?>"  src="file-js/RunningATSByDateBal-dt2.js"></script>
...
var this_js_script = $( "script[src*='RunningATSByDateBal-dt2']" );
// var my_var_1 = this_js_script.data("colCount");
var my_var_1 = this_js_script.attr("data-colCount");

/*eslint no-console: "off"*/
// custom console
console.log("a:" + my_var_1);
```
### function parameter

```javascript
function(a,b){}(aobject, bobject));

(function(w, d){
	var b = d.getElementsByTagName('body')[0];
	var s = d.createElement("script"); s.async = true;
	var v = !("IntersectionObserver" in w) ? "8.7.1" : "10.5.2";
	s.src = "https://cdnjs.cloudflare.com/ajax/libs/vanilla-lazyload/" + v + "/lazyload.min.js";
	w.lazyLoadOptions = {}; // Your options here. See "recipes" for more information about async.
	b.appendChild(s);
}(window, document));
```

