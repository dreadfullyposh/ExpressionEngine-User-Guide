#############
Hello, World!
#############

Congratulations! You have installed ExpressionEngine... now what? Why not say 
"Hello"!

Visit :menuselection:`Design --> Templates --> Edit --> Create Group`

Fill in the field for **Template Group Name**, for this example use "site". 
Ignore **Duplicate an Existing Template Group?** for now and check the 
box for **Make the index template in this group your site's home page?**. Now, 
click `Submit`.

What you've done is created a template group and set that group's index template 
as your site's home page.

After creating the group, you'll be taken to the 
:doc:`Template Manager </cp/design/templates/templates>`.

|Template Group|

Click `Index` in the **Edit Template** column. This will take you to the 
:doc:`Template Editor </cp/design/templates/edit_template>`.

|Template Edit|

You should see a completely blank slate. That's rather uninteresting... let's 
add some code! ::

  <!DOCTYPE html>
  <html lang="en">
	<head>
		<meta charset="UTF-8">
		<title>Hello, World!</title>
	</head>
  
	<body>
 		<h1>Hello, World!</h1>
 		<p>
 		This is an excellent way to see our work.
 		</p>
	</body>
  </html>

To save your changes, click `Update`. 

Ready to admire your work? Click `View Rendered Template` in the 
upper-right area above the **Template Editor**. You'll be taken to your site 
to see what the world will see.

Have a look at the URL - ``example.com/index.php/site``.
ExpressionEngine uses :doc:`URL Segments </templates/globals/url_segments>` to 
do its magic, and here you can see ``site`` in Segment 1. That 
tells ExpressionEngine to look for a Template Group named "site" and the lack of 
Segment 2 (since there is nothing past ``site/``) let's ExpressionEngine know to 
use the group's "index" template.

Try a couple of other URLs:

	- ``http://example.com/index.php/site/index``
	- ``http://example.com/``

You'll see the same output as before. In the fist example, adding Segment 2
(``index``), alerts ExpressionEngine to precisely the template we want from the
group "site". In the second example, going straight to the root URL should bring
up the home page. Remember, we set ExpressionEngine to use the "index" template 
from the group "site" as our site's home page.

You can add more HTML to your template and have some fun. Create a few other
templates in this group, or some new groups altogether. Spend some time playing 
with how ExpressionEngine uses the URL.

Now that you're' comfortable with static ExpressionEngine templates, how about 
:doc:`Building a Simple Site <building_a_simple_news_site>`? 

.. |Template Group| image:: ../images/template-manager-hw.png
.. |Template Edit| image:: ../images/template-editor-hw.png