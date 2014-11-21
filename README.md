#Timply

Simple system to use themes in your PHP projects.

##Features

Easy way to load data in theme  
Can manage language with several dictionnaries (like en_EN & fr_FR)  

Example
-------
In your theme dir (by default: themes) you must create html pages like this :
```
<!-- Include header.html -->
<p>{title}</p>
<div id="content">
    <!-- Start Content -->
    <h4>{elementtitle}</h4>
    <em>[trad::by] Daniel Douat</em>
    <p>{elementtext}</p>
    <!-- End Content -->
</div>
<!-- Start Tags -->
<span>#{tag}</span>&nbsp;
<!-- End Tags -->
```

For this example header.html :
```
<h1>Header</h1>
```

If you want use language support, create a lang file (here en_EN.php) like :
```
<?php
$lang['by']  = "by";
$lang['for'] = "for"
?>
```

In your php file, call timply class, initialize, populate your object and return html.
```
<?php
require_once 'timply.php';

timply::setUri('themes/default');
timply::setFileName('page.html');
timply::addDictionary('en_EN.php');
// several dictionaries can be loaded
timply::addDictionary('myApp/en_EN.php');
timply::addDictionary('myOtherApp/fr_FR.php');

$page = new timply();

$content[0]['title'] = "Timply script";
$content[0]['text']  = "This script can create pages with basic php elements.";
$content[1]['title'] = "My first page";
$content[1]['text']  = "Hello world ! It's my first page, generated with timply !";

$tags[0] = "timply";
$tags[1] = "first";
$tags[2] = "page";
$tags[3] = "github";

$page->setElement("title", "Timply class test");

foreach ($content as $values) {
    $page->setElement("elementtitle", $values['title'], "Content");
    $page->setElement("elementtext", $values['text'], "Content");
}

foreach ($tags as $value) {
    $page->setElement("tag", $value, "Tags");
}

return $page->returnHtml();
?>
```

The result :
```
<h1>Header</h1>
<p>Timply class test</p>
<div id="content">
    <h4>Timply script</h4>
    <em>by Daniel Douat</em>
    <p>This script can create pages with basic php elements.</p>
    <h4>My first page</h4>
    <p>Hello world ! It's my first page, generated with timply !</p>
</div>
<span>#timply</span>&nbsp;<span>#first</span>&nbsp;<span>#page</span>&nbsp;<span>#github</span>&nbsp;
```

_or_


```
<?php
$content[0]['title'] = "New timply method";
$content[0]['text']  = "Now you can pass array for elements, timply works for you.";
$content[1]['title'] = "Look at this !";
$content[1]['text']  = "A duck is walking on timply !";

$tags[]['tag'] = "duck";
$tags[]['tag'] = "method";
$tags[]['tag'] = "array";
$tags[]['tag'] = "wtf";

$page->setElements($content, "Content");
$page->setElements($tags, "Tags");

return $page->returnHtml();
?>
```

The result :
```
<h1>Header</h1>
<p>Timply class test</p>
<div id="content">
    <h4>New timply method</h4>
    <em>by Daniel Douat</em>
    <p>Now you can pass array for elements, timply works for you.</p>
    <h4>Look at this !</h4>
    <p>A duck is walking on timply !</p>
</div>
<span>#duck</span>&nbsp;<span>#method</span>&nbsp;<span>#array</span>&nbsp;<span>#wtf</span>&nbsp;
```

That's all !

##Licence :

Timply is distributed under the zlib/libpng License :

Copyright (c) 2013-2014 [Daniel Douat](http://daniel.douat.fr)
All rights reserved.
Redistribution and use in source and binary forms, with or without
modification, are permitted provided that the following conditions are met:

* Redistributions of source code must retain the above copyright
  notice, this list of conditions and the following disclaimer.
* Redistributions in binary form must reproduce the above copyright
  notice, this list of conditions and the following disclaimer in the
  documentation and/or other materials provided with the distribution.
* Neither the name of the University of California, Berkeley nor the
  names of its contributors may be used to endorse or promote products
  derived from this software without specific prior written permission.

THIS SOFTWARE IS PROVIDED BY THE REGENTS AND CONTRIBUTORS ``AS IS'' AND ANY
EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED
WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE
DISCLAIMED. IN NO EVENT SHALL THE REGENTS AND CONTRIBUTORS BE LIABLE FOR ANY
DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES
(INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES;
LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND
ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT
(INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS
SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
