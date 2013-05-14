TIMPLY
======

Example
-------
In your theme dir (by default themes) you must create html pages like this :
``<p>{title}</p>
<div id="content">
    <!-- Start Content -->
    <h4>{elementtitle}</h4>
    <p>{elementtext}</p>
    <!-- End Content -->
</div>
<!-- Start Tags -->
<span>#{tag}</span>&nbsp;
<!-- End Tags -->``

In your php file, call timply class, initialize, populate your object and return result. That's all !
``
<?php
//Optional
//TIMPLY_DIR = 'themes/default/'
require_once 'timply.php';

$page = new timply('page.html');

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
    $page->setElement("tag", $value, "Tags", TRUE);
}

return $page->returnHtml();
?>``