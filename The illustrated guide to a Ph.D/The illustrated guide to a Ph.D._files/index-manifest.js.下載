var Articles = {} ;

var Cats = 
 { "howto" : "HOWTOs"
 , "writing" : "Writing"
 , "pl" : "Programming Languages"
 , "fp" : "Functional Programming"
 , "compilers" : "Compilation"
 , "ugcs" : "Undergraduate Computer Science"
 , "grad-school" : "Graduate School"
 , "scheme" : "Scheme"
 , "racket" : "Racket"
 , "latex" : "LaTeX"
 , "c": "C"
 , "c++": "C++"
 , "javascript" : "JavaScript"
 , "java" : "Java"
 , "scala" : "Scala"
 , "ml" : "ML"
 , "sql" : "SQL"
 , "haskell" : "Haskell"
 , "perl" : "Perl"
 , "lambda": "Lambda"
 , "lambda-calculus": "Lambda Calculus"
 , "python" : "Python"
 , "perl" : "Perl"
 , "swift" : "Swift"
 , "scripting" : "Scripting"
 , "gadgets" : "Gadgets"
 , "greasemonkey" : "Greasemonkey Hacks"
 , "teaching" : "Teaching"
 , "gaming" : "Gaming"
 , "continuations" : "Continuations"
 , "illustrated" : "Illustrated"
 , "ios" : "iPhone, iPad, iPod"
 , "apple" : "Apple"
 , "unix" : "Unix"
 , "httpd" : "Web servers"
 , "presenting" : "Giving Presentations"
 , "academia" : "Academia"
 , "hacks" : "Hacks"
 , "productivity" : "Productivity"
 , "travel" : "Travel"
 , "static-analysis" : "Static Analysis"
 , "home" : "Home Improvement"
 , "rants" : "Rants"
 , "security" : "Security"
 , "health" : "Health"
 , "math" : "Mathematics"
 , "parsing" : "Parsing"
 , "science" : "Science"
 } ;

var Order =
 [ "illustrated"
 , "fp"
 , "grad-school"
 , "productivity"
 , "ios"
 , "howto"

 , "ugcs"

 , "parsing"
 , "continuations"

 , "compilers"

 , "math"
 , "pl"

 , "writing"
 , "presenting"

 , "lambda-calculus"
 , "c"
 , "c++"
 , "scheme"
 , "racket"
 , "javascript"
 , "swift"
 , "python"
 , "perl"
 , "java"
 , "scala"
 , "latex"
 , "ml"
 , "sql"
 , "haskell"
 , "scripting"

 , "lambda"

 , "apple"
 , "unix"

 , "httpd"
 , "static-analysis"
 , "security"

 , "hacks"
 , "travel"
 , "greasemonkey"

 , "academia"
 , "teaching"
 , "science"

 , "health"
 , "gadgets"
 , "gaming"
 , "home"
 , "rants"
 ];

function AddArticle(tag,id,title) {
 if (!Articles[tag]) Articles[tag] = [] ;
 Articles[tag].push({"id": id, "title": title}) ;
}

for (var i = 0; i < Manifest.length; ++i) {
 var art = Manifest[i]; 
 if (art.tags.length == 0) {
  AddArticle("untagged", art.id, art.title) ;
 }
 for (var j = 0; j < art.tags.length; ++j) {
  AddArticle(art.tags[j], art.id, art.title) ;
 }
}

function RenderArticleLink(a) {
  document.write("<li>") ;
  document.write('<a href="http://matt.might.net/articles/'+a.id+'/">') ;
  document.write(a.title);
  document.write("</a>");
  document.write("</li>") ;
}

function RenderTagLinks(tag) {
 var arts = Articles[tag] ;
 for (var k = 0; k < arts.length; ++k) {
  a = arts[k]; 
  if (a.id == Key) continue ;
  document.write("<li>") ;
  document.write('<a href="http://matt.might.net/articles/'+a.id+'/">') ;
  document.write(a.title);
  document.write("</a>");
  document.write("</li>") ;
 }
}


function RenderTagGroup(tag) {
 if (!Cats[tag]) Cats[tag] = "undefined--" + tag ;
 document.write("<b>" + Cats[tag] + "</b>: <br />") ;
 document.write("<ul>") ;
 var arts = Articles[tag] ;
 for (var k = 0; k < arts.length; ++k) {
  a = arts[k]; 
  document.write("<li>") ;
  document.write('<a href="./'+a.id+'/">') ;
  document.write(a.title);
  document.write("</a>");
  document.write("</li>") ;
 }
 document.write("</ul>");
}


