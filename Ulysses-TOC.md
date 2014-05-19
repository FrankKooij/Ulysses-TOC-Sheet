### Table of Contents
%% Paste this text into empty Ulysses sheet, and place it after front matter,
%% or as first sheet, if no main heading or introduction
~~<div id="toc" class="toc">
~~</div>
----
~~ <div class="contents" id="contents">
%% 
%% This TOC sheet can be added just after frontmatter as it is. It can also be inserted anywhere in the  document structure, but then make sure that the <div id="contents"> tag is inserted above first heading to be included in the TOC.
%% Works with any of Ulysses HTML-styles and preview, but not with Rich Text-styles.
%% 
%% if you want heading links without decoration (underlined), uncomment following section:
~~ <!--
~~ <style type="text/css">
~~ h1 a, h2 a, h3 a, h4 a, h5 a, h6 a  {
~~ 	text-decoration: none; 
~~ 	 color:black; }
~~ </style>
~~ -->
%% 
%% If you need valid XHTML, a </div> closing tag should be put at the end of last sheet. 
%% But this script works also fine without it. 
%% 
%% Variables: maxLevel;  listType "ul" or "ol"; tocTag "li" or "p"; 
%% can be changed to modify look and feel of the TOC (See in script below)
%% You can also add styles for: ul.toc, ol.toc, li.toc, and p.toc in CSS style sheet.
%% 
%% Added style for multi level numbering of <ol><li> tags
%% Also CSS for auto numbering of headings corresponding to TOC
%% This can just be commented out if you dont want nubered headings
%% This could be added to your CSS-style sheet, but more flexibel if inline like this:
~~ <!-- CSS for auto multi level TOC numbering : -->
~~ <style type="text/css">
~~ /* hide original list counter */
~~ol li {display:block;}
~~ /* OR */
~~ /* ol {list-style:none;}  */
~~ 
~~ ol > li:first-child {counter-reset: item;} /* reset counter */
~~ ol > li {counter-increment: item;} /* increment counter */
~~ ol > li:before {content:counters(item, ".") ". "; font-weight:bold;} /* print counter */
~~</style>
%% [stackoverflow.com]
%% 
~~ <!-- CSS for auto numbering of headings: -->
~~ <!-- If not wanted, just MOVE this comment's closing tag after: </style>-->
~~ <style type="text/css">
~~ div.contents {counter-reset: h1c;}
~~   h1 {counter-reset: h2c;}
~~   h2 {counter-reset: h3c;}
~~   h3 {counter-reset: h4c;}
~~   h4 {counter-reset: h5c;}
~~ 
~~   div.contents h1:before {counter-increment: h1c; content: counter(h1c) ". ";}
~~   div.contents h2:before {counter-increment: h2c; content: counter(h1c) "." counter(h2c) ". ";}
~~   div.contents h3:before {counter-increment: h3c; content: counter(h1c) "." counter(h2c) "." counter(h3c) ". ";}
~~   div.contents h4:before {counter-increment: h4c; content: counter(h1c) "." counter(h2c) "." counter(h3c) "." counter(h4c) ". ";}
~~ </style>
%% 
~~<!-- Java script for making TOC "on the fly": -->
~~<script type="text/javascript" language="javascript">
~~<!-- // JavaScript-code in XML comment block, to parse as valid XML. 
~~        // </div>-tag is then also needed at the end of last sheet! 
~~ window.onload = function () {
~~     var maxLevel = 4;  // Max Header level in TOC
~~     var listType = "ol";  // Use: "ul" or "ol" only! (ul = bullets, ol = numbers)
~~     var tocTag ="li";   // Use: "li" or "p" only! (p = plain TOC, no bullets or numbers)
~~     var toc = "";
~~     var level = 0;
~~     var tocId = 0;
~~     document.getElementById("contents").innerHTML =
~~         document.getElementById("contents").innerHTML.replace(
~~         /<h(\d)>(.+?)<\/h(\d)>/gi,
~~         function (str, openLevel, titleText, closeLevel) {
~~             if (openLevel != closeLevel) {
~~                 return str;
~~             }
~~ 
~~ 	if (openLevel > maxLevel) {
~~                   return str;
~~              }
~~ 
~~             if (openLevel > level) {
~~                 toc += (new Array(openLevel - level + 1)).join("<"+ listType +" class='toc'>");
~~             } 
~~             else if (openLevel < level) {
~~                 toc += (new Array(level - openLevel + 1)).join("</"+ listType +">");
~~             }
~~ 
~~             level = parseInt(openLevel);
~~             tocId++;
~~             var anchor = "h-id-" + tocId;
~~             var tocAnchor = "toc-" + tocId;
~~ 
~~             toc += "<"+tocTag+" class='toc'><a href=\"#" + anchor 
~~                    + "\" id='" + tocAnchor + "'>" 
~~                    + titleText + "</a></"+tocTag+">";
~~ 
~~             return "<h" + openLevel + ">"
~~                 + "<a id=\"" + anchor + "\" href='#" + tocAnchor + "'>"
~~                 + titleText + "</a></h" + closeLevel + ">"; 
~~         }
~~     );
~~ 
~~     if (level) {
~~         toc += (new Array(level + 1)).join("</ul>");
~~     }
~~ 
~~     document.getElementById("toc").innerHTML += toc;
~~ };
~~ //-->
~~ </script>
%% Script copied from: 
%% http://stackoverflow.com/questions/187619
%% answer at Oct 9 2008 at 15:59 by: 
%% http://stackoverflow.com/users/23501/ates-goral 
%% Modified by RoyRogers56, 2014-05-14