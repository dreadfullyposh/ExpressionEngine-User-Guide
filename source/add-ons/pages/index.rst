.. # This source file is part of the open source project
   # ExpressionEngine User Guide (https://github.com/ExpressionEngine/ExpressionEngine-User-Guide)
   #
   # @link      https://expressionengine.com/
   # @copyright Copyright (c) 2003-2018, EllisLab, Inc. (https://ellislab.com)
   # @license   https://expressionengine.com/license Licensed under Apache License, Version 2.0

#####
Pages
#####

.. contents::
   :local:

.. warning:: Used sparingly, the Pages Module is a very useful tool, but
  when overused it can create an unmaintainable site. A site built using
  ExpressionEngine's :doc:`default URL behavior </urls/url_structure>`
  will be much easier to create and maintain than a site that forces
  every entry into a page. If you've created more than 10 pages,
  carefully consider your other options before adding more pages because
  there's probably a much better way to do what you want to do.

************
Introduction
************

The Pages Module allows you to create special "page" entries for
holding content that is more static than dynamic. The entries are
displayed via the Channel Entries tag and can be displayed at virtually
any URL desired.


*********************
Managing Page Content
*********************

The :doc:`Pages Module Control Panel <control_panel/index>` allows you
to create, edit, view and delete your Pages.

.. note:: In order to allow content authors full access to create and modify
   pages through both the Pages tab of the Publish area and the Pages module
   itself, it is necessary to give those authors' respective member groups the
   appropriate Control Panel access for publishing and editing content, access
   to post and edit entries in the particular Channel in question, access to
   Modules in general, and access to the Pages module specifically.

****************************************************
Displaying Page Content with the Channel Entries Tag
****************************************************

Displaying Page content is as easy as displaying normal Channel entries.
The primary difference is that when a Page URI is requested, the URL
segments do not correlate to a template group and template, as that is
determined by the template that the particular "page" entry was assigned
to use on the :doc:`Pages tab </cp/publish/create>` of the Publish
form.

Additionally, the page will automatically be treated as a single entry
page for that page entry, so other tags on the template will need to use
the dynamic="no" parameter (if available) to display other content.

In the Template chosen on the :doc:`Pages tab </cp/publish/create>` of
the Page entry, use a normal :doc:`Channel Entries tag
</channel/channel_entries>` with any parameters and variables
that you desire to display the entry, e.g.::

	{exp:channel:entries channel="personnel"}
		<h2>{title}</h2>
		<h3>Position</h3>
		<p>{position}</p>
		<h3>Background</h3>
		<p>{background}</p>
	{/exp:channel:entries}

.. note:: Spanning an entry across multiple pages is not possible when
   using Page URLs, as content is only displayed for exact URI matches.

Parameters
==========

The Pages Module adds the following parameters for use in the
{exp:channel:entries} tag.

-  :ref:`channel_entries_show_pages`

Variables
=========

The Pages Module adds the following variables for use in the
{exp:channel:entries} tag.

-  :ref:`channel_entries_page_uri`
-  :ref:`channel_entries_page_url`


*********************
Multiple Site Manager
*********************

If you are using the :doc:`Multiple Site Manager </cp/msm/index>`,
page data are only available for the current site. If you wish to show
the {page\_uri} or {page\_url} for an entry from a different site, you
will need to use the {exp:pages:load\_site\_pages} tag on the relevant
template. This tag has one required parameter: site. For example, if
your weblog tag is pulling in pages from sites default\_site and
corporate\_site, your tag should look like:

::

    {exp:pages:load_site_pages site="default_site|corporate_site"}

*************
Control Panel
*************

See the :doc:`Pages Module Control Panel <control_panel/index>` page.

.. toctree::
	:glob:
	:titlesonly:
	:hidden:

	control_panel/index
