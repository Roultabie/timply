#Timply

Simple system to use themes in your PHP projects.

##Features

Easy way to load data in theme  
Can manage language with several dictionnaries (like en_EN & fr_FR)  

Example
-------
In your theme dir (by default: themes) you must create html pages like this :
```
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

timply::setDir('themes/default');
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

That's all !

##Licence :

Timply is distributed under the zlib/libpng License :

Copyright (c) 2013 Daniel Douat, [Aélys Informatique](http://aelys-info.fr)

This software is provided 'as-is', without any express or implied warranty. In no event will the authors be held liable for any damages arising from the use of this software.  

Permission is granted to anyone to use this software for any purpose, including commercial applications, and to alter it and redistribute it freely, subject to the following restrictions :  

1. The origin of this software must not be misrepresented; you must not claim that you wrote the original software. If you use this software in a product, an acknowledgment in the product documentation would be appreciated but is not required.  

2. Altered source versions must be plainly marked as such, and must not be misrepresented as being the original software.  

3. This notice may not be removed or altered from any source distribution.
