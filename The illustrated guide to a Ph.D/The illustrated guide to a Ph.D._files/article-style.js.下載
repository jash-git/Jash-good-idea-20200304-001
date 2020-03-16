function InsertAfter(newElement,targetElement) {
    var p = targetElement.parentNode;
    
    if(p.lastchild == targetElement) {
	p.appendChild(newElement);
    } else {
	p.insertBefore(newElement, targetElement.nextSibling);
    }
}


// Back to blog.might.net
Might.registerInitHandler(function () {
    if (!ShouldDisplayHomePageLink || !ShouldDisplayHeaderLinks) {
      return ;
    }

    for (var j = 0; j < Manifest.length; ++j) {
      var item = Manifest[j];
      if (item.id == Key) {
        break ;
      }
    }

    function mod(i, n) {
      if (i >= 0) {
        return i % n ;
      } else if (i == -1) {
        return (n-1) ;
      }
    }

    var r = Math.round(Manifest.length*Math.random(),0) ;

    function linkTo(item) {
      return '<a href="../'+item.id+'/">'+item.title+'</a>' ;
    }

    var homeLink = '<a href="'+Root+'articles/">article index</a>' ;
    var newLink = linkTo(Manifest[0]) ;
    var nextLink = linkTo(Manifest[mod(j+1, Manifest.length)]) ;
    var prevLink = linkTo(Manifest[mod(j-1, Manifest.length)]) ;
    var randLink = linkTo(Manifest[mod(r, Manifest.length)]) ;

    var retLink = document.createElement("div") ;

    var botLinks = document.createElement("div") ;

    var linksText = "<b>Latest:</b> " + newLink + "<br /><b>Next:</b> " +prevLink+ "<br /><b>Prev:</b> " +nextLink  + "<br /><b>Rand:</b> " + randLink ;

 
    retLink.className = "navlinks" ;
    botLinks.className = "navlinks"; 

    retLink.innerHTML = linksText ;
    botLinks.innerHTML = linksText ;


    var content = document.getElementById("content-container") ;

    var top = document.getElementById("abstract-container") ;
    
    if (!top) top = content ;
    top.parentNode.insertBefore(retLink, top) ;

    var bot = document.getElementById("footer-ad") ;

    if (!bot) bot = content ;

    InsertAfter(botLinks, bot) ;

    var h1s = document.getElementsByTagName("h1") ;

    if (h1s) {
      var h1 = h1s[0] ;

      var par = h1.parentNode ;
      
      for (var i in par.childNodes) {
        var child = par.childNodes[i] ;
        if (child === h1) {
          break ;
        }
      }

      ++i ;

      var sibling = par.childNodes[i] ;
      
      var rssLink = '<a href="../feed.rss">rss</a>' ;

      var retLink = document.createElement("div");

      var twitterLink = '<a href="http://twitter.com/mattmight">@mattmight</a>' ;

      var emailMatt = '<a href="mai'+'lto:matt-blog'+'@'+'migh'+'t.net">email:matt.might</a>'

      retLink.innerHTML = "[" +homeLink+ "] "  + " [" + emailMatt + "]" + " [" + twitterLink + "] " + " [" + rssLink + "] ";

      if (window.ArticleVersion && window.ArticleVersion >= 2) {
      } else {
        par.insertBefore(retLink, sibling) ;
      }

    }

  }) ;
