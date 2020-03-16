// Debug cover.
if (!window.console) window.console = {log: function () {}} ;

// Config.
var ShouldDisplayHomePageLink = true ;
var ShouldDisplayHeaderLinks = true ;

var Scripts = document.getElementsByTagName("script") ;


// Inclusion mechanism.
var Root ;

for (var i = 0; i < Scripts.length; i++) {
 var path ;
 if ((path = Scripts[i].src.match(/(.*\/?)matt.might.js/))) {
   Root = path[1] ;
 }
} 

var Included = {} ;

function include(filename) {
  if (Included[filename])
    return ;
  else
    Included[filename] = true ;

  if (filename.match(/[.]js/)) {
    document.write('<scr'+'ipt src="'+Root+'js/'+filename+'"></scr'+'ipt>') ;
  }

  if (filename.match(/[.]css/)) {
    document.write('<link rel="stylesheet" type="text/css" media="all" href="' + Root + "css/" + filename + '" />') ;
  }
}

window.isLoaded = false ;



// lib Might 
var Might = {} ;


Might.initHandlers = [] ;

window.onload = function () {
  var hs = Might.initHandlers ;
  for (var i = 0; i < hs.length; ++i) {
    (hs[i])() ;
  }
} ;

Might.registerInitHandler = function (handler) {
  if (window.isLoaded)
    handler() ;
  else
    Might.initHandlers.push(handler) ;
} ;

Might.includeDefaultStyle = function () {
  include("raised-paper-style.js") ;
} ;

// This is busted in IE6 and IE7.
Might.includeGoogleAnalytics = function () {
  var gaJsHost = (("https:" == document.location.protocol) ? "https://ssl." : "http://www.");

  document.write(unescape("%3Cscript src='" + gaJsHost + "google-analytics.com/ga.js' type='text/javascript'%3E%3C/script%3E"));

  document.write('<scr'+'ipt>var pageTracker = _gat._getTracker("UA-3661244-1");pageTracker._initData();pageTracker._trackPageview();</scri'+'pt>') ;
} ;



Might.fetch = function (url, onSuccess, onFail) {
  var req ;

  var async = true ;

  if (!onSuccess) {
    async = false ;
  }

  var answer = null ;

  function processReqChange() {
    if (req.readyState == 4) {
      if (req.status == 200) {
        answer = req.responseText ;
        if (onSuccess) { onSuccess(req.responseText, url, req) ; }
      } else {
        if (onFail) onFail(url, req) ;
      }
    }
  }

  // branch for native XMLHttpRequest object
  if (window.XMLHttpRequest) {
    req = new XMLHttpRequest();
    answer = req ;
    if (async) req.onreadystatechange = processReqChange;
    req.open("GET", url, async);
    req.send(null);
    // branch for IE/Windows ActiveX version
  } else if (window.ActiveXObject) {
    req = new ActiveXObject("Microsoft.XMLHTTP");
    answer = req ;
    if (req) {
      if (async) req.onreadystatechange = processReqChange ;
      req.open("GET", url, async);
      req.send();
    }
  }

  processReqChange() ;

  return answer ;
} ;


Might.inputText = function (url, el) {
  if (typeof el == "string") el = document.getElementById(el) ;

  Might.fetch(url, function (contents) {
      contents = contents.replace(/&/g,"&amp;") ;
      contents = contents.replace(/</g,"&lt;") ;
      contents = contents.replace(/>/g,"&gt;") ;
      contents = contents.replace(/\n/g,"<br/>") ;
      contents = contents.replace(/ /g,"&nbsp;") ;
      contents = contents.replace(/\t/g,"     ") ;
      el.innerHTML = contents ;
    }) ; 
} ;

Might.basename = function (url) {
  var m = url.match(/.*\/([^\/]+)/) ;
  return m[1] ;
} ;

Might.highlightCode = function (filename,style) {
  var fileurl = URLPath+filename ;
  var highlighturl = Root+'/apps/mchighlight/?file='+URLPath+filename ;
  document.write('<p>[<a href="'+fileurl+'">download '+Might.basename(filename)+'</a>]') ;
  document.write(' [<a href="'+highlighturl+'">view '+Might.basename(filename)+'</a>]</p>') ;
  document.write('<iframe style="'+style+'" class="code-frame" src="'+highlighturl+'"></iframe>') ;
} ;

Might.renderCode = function (url, style) {
  if (!style) style = "" ;
  var id = "code:" + url ;
  document.write('<p>[<a href="'+url+'">'+Might.basename(url)+'</a>]</p>') ;
  document.write('<div class="code-fragment" id="'+id+'" style="font-family: Monaco, monospace; font-size: 80%; '+style+'">') ;
  document.write('</div>') ;
  Might.inputText(url, id) ;
} ;


Might.enableSyntaxHighlighting = function (brushes,theme) {
 if (!theme) theme = "Default" ;
 if (typeof brushes == "string") brushes = [brushes] ;
 include("xregexp-min.js") ;
 include("syntaxhighlighter/src/shCore.js") ;
 for (var i = 0; i < brushes.length; ++i) {
  include("syntaxhighlighter/scripts/shBrush"+brushes[i]+".js") ;  
 }
 include("syntaxhighlighter/styles/shCore.css") ;
 include("syntaxhighlighter/styles/shTheme"+theme+".css") ;
};


Might.codeSnippets = 0 ;

Might.printCode = function (url, options) {
 if (!options) options = {} ;

 if (!options.language) {
  var parts = url.split(/[.]/) ;
  var ext = parts[parts.length-1] ;
  options.language = ext ;
 }

 if (options.overflow) {

  if (!options.width)  options.width = "500px;" ;
  if (!options.height) options.height = "700px;" 

 } else {
   options.overflow = "default" ;
 }

 if (!options.fontSize) options.fontSize = "100%" ;

 var language = options.language ;

 var codeId = "code-snippet-" + (++Might.codeSnippets) ;
 var dlLink = '[<a href="'+url+'">Download '+Might.basename(url)+'</a>]' ;
 var dims = "" ;
 if (options.overflow) {
  dims = "width: " + options.width + "; height: " + options.height + "; " ;
 }
 document.write('<p>' + dlLink + '</p><div id="'+codeId+'-container" class="syntax-highlighted-code" style="overflow: '+options.overflow+'; font-size: '+options.fontSize+' ; '+dims+'"><pre class="brush: '+language+'" id="'+codeId+'"></pre></div>') ;
 Might.fetch (url, function (contents) {
  var el = document.getElementById(codeId) ;
  if (navigator.userAgent && !navigator.userAgent.match(/MSIE/)) {
   el.innerHTML = contents ;
  } else {
    document.getElementById(codeId + "-container").style.display = "none" ;
  }
  SyntaxHighlighter.highlight(undefined,el) ;
 }) ;
} ;


Might.enableAds = function () {

  function AddAdModule() {
    var adModule = document.createElement("div") ;

    adModule.className = "module ad-module" ;
    adModule.id = "ad1-container" ;

    var adArea = document.createElement("div") ;
    adArea.id = "ad1" ;

    adModule.appendChild(adArea) ;

    document.getElementById("body").appendChild(adModule) ;
  
    StyleModules() ;
  }


  Might.registerInitHandler(function() { AddAdModule() ; }) ;
} ;



/*
  Emitting "Jump to" blocks.
 */

Might.installJumpTo = function() {
  if (window.isArticleIndexPage)
    return ;

  var h2s = document.getElementsByTagName("h2") ;

  var jumpText = "<p>Jump to:<ul>" ;
  for (var i = 0; i < h2s.length; i++) {
    var h2 = h2s[i] ;
    var aname = document.createElement("a") ;
    aname["name"] = "sec" + i ;
    h2.parentNode.insertBefore(aname,h2) ;
    jumpText += ('<li><a href="#sec'+i+'">'+h2.innerHTML+'</a></li>\n') ;
  }
  jumpText += ("</ul></p>") ;

  var jumpDiv = document.getElementById("jumpto") ;

  if (!jumpDiv && h2s.length > 0) {
    jumpDiv = document.createElement("div") ;
    h2s[0].parentNode.insertBefore(jumpDiv,h2s[0]) ;
  }

  if (jumpDiv)
    jumpDiv.innerHTML = jumpText ;
} ;


/* Helper functions for obscuring email. 

   Most spam-crawlers don't seem to use javascript. */

Might.emailme = function (text) {
  if (!text) text = 'mi' + 'ght' + '@ua' + 'b.ed' + 'u' ;
  document.write('<a href="mai'+'lto:'+'mi'+'ght@'+'ua'+'b'+'.ed'+'u">'+text+'</a>');
} ;

Might.email = function (account,domain,text) {
  document.write('<a href="mailto:'+account+'@'+domain+'">'+text+'</a>') ;
} ;


// Query string.

var URLParts = location.href.split(/[?]/) ;
Might.queryString = "" ;

var URLPathParts = URLParts[0].match(/(^.*\/)[^\/]*$/) ;

var URLPath = URLPathParts[0] ;

if (URLParts[1])
  Might.queryString = URLParts[1] ;

var QueryParts = Might.queryString.split(/&/) ;

Might.query = {} ;

for (var i = 0; i < QueryParts.length; ++i) {
  var param = QueryParts[i].split ("=") ;
  Might.query[decodeURIComponent(param[0])] = decodeURIComponent(param[1]) ;
}
