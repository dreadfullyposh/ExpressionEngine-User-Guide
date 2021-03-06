.. # This source file is part of the open source project
   # ExpressionEngine User Guide (https://github.com/ExpressionEngine/ExpressionEngine-User-Guide)
   #
   # @link      https://expressionengine.com/
   # @copyright Copyright (c) 2003-2018, EllisLab, Inc. (https://ellislab.com)
   # @license   https://expressionengine.com/license Licensed under Apache License, Version 2.0

#########################
Prototype User Guide Page
#########################

This page represents all of the various types of documentation needs that we encounter when documenting EllisLab applications. The focus is on readability, user friendliness, and an "I've got your hand, baby" feel. While they can be quite technical, we always write for humans... our grandmothers even!

A table of contents should always be included like the one below. It is created automatically by inserting the ``.. contents::`` directive on a line by itself.

.. contents::

***************
Editor Settings
***************

Install the `Editor Config <http://editorconfig.org>`__ plugin for your specific editor and it will take care of the rest.

*****
Links
*****

When linking to another page in the documentation always use doc references::

  :doc:`Another Page <section/another_page>`
  :doc:`section/another_page`

If you don't insert a page title (e.g. ``Another Page`` above) then the page title from the linked document will be used When linking to a documented method, use the method references::

  :meth:`Api_channel_entries::save_entry`

When linking to an anchor on the page, section links::

  `Section Name on page`_

When linking to an anchor on another page, you **must** use cross-references (always use underscores in the reference definition) ::

  .. _anchor_on_page:

  Anchor on Page
  --------------

  // elsewhere...
  :ref:`Another page's anchor <anchor_on_page>`
  :ref:`anchor_on_page`

When linking to an ExpressionEngine.com page, use the short forms for that::

  // ExpressionEngine.com Pages
  :expressionengine:`ExpressionEngine Community </community>`

  // Forum Topics
  :forum_topic:`Feature Request <12345>`

*****************************************
Page and Section Headings and Subheadings
*****************************************

Headings not only provide order and sections within a page, but they also are used to automatically build both the page and document table of contents. Headings are formed by using certain characters as underlines for a bit of text. Major headings, like page titles and section headings also use overlines. Other headings just use underlines, with the following hierarchy::

  # with overline for page titles
  * with overline for major sections
  = for subsections
  - for subsubsections
  ^ for subsubsubsections
  " for subsubsubsubsections (!)

The TextMate EEDocs Bundle can help you create these with the following tab triggers::

  title->

    ##########
    Page Title
    ##########

  sec->

    *************
    Major Section
    *************

  sub->

    Subsection
    ==========

  sss->

    SubSubSection
    -------------

  ssss->

    SubSubSubSection
    ^^^^^^^^^^^^^^^^

  sssss->

    SubSubSubSubSection (!)
    """""""""""""""""""""""


*******************
Control Panel Pages
*******************

.. rst-class:: cp-path

**Control Panel Location:** :menuselection:`Design --> Templates --> Global Preferences`

To style the above properly, assign a class of *cp-path* and use the \:menuselection\: role with hyphen-arrows::

  .. rst-class:: cp-path

  **Control Panel Location:** :menuselection:`Design --> Templates --> Global Preferences`

|Global Template Preferences|

This section of the Control Panel allows you to define global preferences which globally affect all Templates.


*****************
exp:module:method
*****************

A tag has all parameters and variables documented. Subsections are used to separate required parameters from optional parameters. Parameters and variables within their subsections are always listed in alphabetical order.

Required Parameters
===================

The following parameters are *required* by the ``{exp:module:method}`` tag.
channel=
--------

::

  channel="news"

From which channel to show the meta data information.


Optional Parameters
===================

show_expired=
-------------

::

  show_expired="yes"

You can determine whether you wish for entries that have "expired" to be included.

username=
---------

::

  username="petunia"

This parameter limits the query by username. You can use the pipe character to query by multiple usernames::

  username="tom|dick|harry"

Or you can add "not" to exclude usernames::

  username="not tom|dick|harry|fred"

You can also use the constant "CURRENT\_USER" to show entries from only the currently logged in user::

  username="CURRENT_USER"

This allow each logged-in user to get only their entries. Users who are not logged in won't see anything. Alternatively, you can use the constant ``NOT_CURRENT_USER`` to show entries **except** from the currently logged in user::

  username="NOT_CURRENT_USER"

Variables
=========

The following variables are available to the ``{exp:module:method}`` tag.

{absolute_results}
------------------

This variable will always display the absolute total number of results that are returned by the tag, regardless of pagination.

{author}
--------

The author's screen name, if it exists; otherwise, this variable will display the username.

{comment_auto_path}
-------------------

This variable is replaced by the URL set in the "Comment Page URL" preference under :menuselection:`Admin --> Channel Management`. No entry id, URL Title, or other information is included; this is the exact URL from the preference.

{custom_field}
--------------

Any custom field can be displayed by using its shortname as a variable within the tag.

{email}
-------

The email address of the entry author.


********************
Method Documentation
********************

When documenting class methods for third party developers, Sphinx provides directives to assist and keep things simple. For example, consider the following ReST:

.. code-block:: rst

  .. php:class:: Some_class

  some_method()
  =============

    .. php:method:: some_method ( $foo [, $bar [, $bat]])

      This function will perform some action. The ``$bar`` array must contain a something and something else, and along with ``$bat`` is an optional parameter.

      :param int $foo: the foo id to do something in
      :param mixed $bar: A data array that must contain aa something and something else
      :param bool $bat: whether or not to do something
      :returns: FALSE on failure, TRUE if successful
      :rtype: Boolean

      Example Usage::

        <?php

        ee()->load->library('some_class');

        $bar = array(
          'something'   => 'Here is this parameter!',
          'something_else'  => 42
        );

        $bat = ee()->some_class->should_do_something();

        if (ee()->some_class->some_method(4, $bar, $bat) === FALSE)
        {
          show_error('An Error Occurred Doing Some Method');
        }

      See also :php:meth:`Some_class::should_do_something`

      .. note:: Here is something that you should be aware of when using some_method(). For real.

  should_do_something()
  =====================

    .. php:method:: should_do_something()

      :returns: whether or something should be done or not
      :rtype: Boolean


It creates the following display:

.. php:class:: Some_class

some_method()
=============

  .. php:method:: some_method ( $foo [, $bar [, $bat]])

    This function will perform some action. The ``$bar`` array must contain a something and something else, and along with ``$bat`` is an optional parameter.

    :param int $foo: the foo id to do something in
    :param mixed $bar: A data array that must contain aa something and something else
    :param bool $bat: whether or not to do something
    :returns: FALSE on failure, TRUE if successful
    :rtype: Boolean

    Example Usage::

      <?php

      ee()->load->library('some_class');

      $bar = array(
        'something'   => 'Here is this parameter!',
        'something_else'  => 42
      );

      $bat = ee()->some_class->should_do_something();

      if (ee()->some_class->some_method(4, $bar, $bat) === FALSE)
      {
        show_error('An Error Occurred Doing Some Method');
      }

    See also :php:meth:`Some_class::should_do_something`

    .. note:: Here is something that you should be aware of when using some_method(). For real.

should_do_something()
=====================

  .. php:method:: should_do_something()

    :returns: whether or something should be done or not
    :rtype: Boolean


******
Tables
******

Tables are hard...

+-----------------------+-----------+-----------------------------------------------+-------------------------------------------------------------------+
| Preference            | Default   | Options                                       |    Description                                                    |
+=======================+===========+===============================================+===================================================================+
| **template**          | None      | None                                          | A string containing your calendar template.                       |
|                       |           |                                               | See the template section below.                                   |
+-----------------------+-----------+-----------------------------------------------+-------------------------------------------------------------------+
| **local\_time**       | time()    | None                                          | A Unix timestamp corresponding to the current time.               |
+-----------------------+-----------+-----------------------------------------------+-------------------------------------------------------------------+
| **start\_day**        | sunday    | Any week day (sunday, monday, tuesday, etc.)  | Sets the day of the week the calendar should start on.            |
+-----------------------+-----------+-----------------------------------------------+-------------------------------------------------------------------+
| **month\_type**       | long      | long, short                                   | Determines what version of the month name to use in the header.   |
|                       |           |                                               | long = January, short = Jan.                                      |
+-----------------------+-----------+-----------------------------------------------+-------------------------------------------------------------------+
| **day\_type**         | abr       | long, short, abr                              | Determines what version of the weekday names to use in            |
|                       |           |                                               | the column headers.                                               |
|                       |           |                                               | long = Sunday, short = Sun, abr = Su.                             |
+-----------------------+-----------+-----------------------------------------------+-------------------------------------------------------------------+
| **show\_next\_prev**  | FALSE     | TRUE/FALSE (boolean)                          | Determines whether to display links allowing you to toggle        |
|                       |           |                                               | to next/previous months. See information on this feature below.   |
+-----------------------+-----------+-----------------------------------------------+-------------------------------------------------------------------+
| **next\_prev\_url**   | None      | A URL                                         | Sets the basepath used in the next/previous calendar links.       |
+-----------------------+-----------+-----------------------------------------------+-------------------------------------------------------------------+

********
404 Page
********

This determines which template should be displayed when someone tries to access an invalid URL. If you choose "None", a standard 404 message and server header will be shown.

Please note that ExpressionEngine **only** validates the first two segments of your URLs when determining whether to show a 404 page, since these segments will correlate to a Template Group and Template name (which represent your site's "pages"). Anything beyond the first two segments can not be used to show a 404 page (with one notable exception, using the `require\_entry= <../../../modules/channel/parameters.html#par_req_entry>`_ parameter).

For an explanation regarding how ExpressionEngine interprets your URLs, please see `ExpressionEngine URLs <../../../general/urls.html>`_ page.

.. important:: **BONUS:** Since the Search module utilizes channel variables, ``{absolute_count}`` is also available to the Search Results tag.

***********************
Save Template Revisions
***********************

If this preference is set to "Yes", then any changes you make to one of your `Templates <edit_template.html>`_ will be saved. This allows you to keep a record of all changes made so that you can easily revert back to an earlier version of a Template if you need to do so.

***********************************
Maximum Number of Revisions to Keep
***********************************

The maximum number of revisions that should be kept for **each** template. For example, if you set this to 5, only the most recent 5 revisions will be saved for any given template. This setting helps ensure that your database does not get too large due to storing Template revisions.

*************************************
Allow Templates to be Saved as Files?
*************************************

This determines whether your Templates are saved out to a flat text file when you save them. See the `Flat File Templates <../../../templates/flat_file_templates.html>`_ section for specific information.

*********************************
Basepath to Doesn't Exist Anymore
*********************************

This is the *server path* to the folder you have created to hold the Template files. It is important that you use the server path for the preference and not a URL. A server path often looks similar to:

:dfn:`/home/usr/domain.com/http\_docs/system/user/some\_where/`

Server paths will vary from server to server, so you should contact your Host or server admin if you are unsure of what your setting should be.

See the `Flat File Templates <../../../templates/flat_file_templates.html>`_ section for more information.

.. |Global Template Preferences| image:: /images/global_template_preferences.png
