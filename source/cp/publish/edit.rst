.. # This source file is part of the open source project
   # ExpressionEngine User Guide (https://github.com/ExpressionEngine/ExpressionEngine-User-Guide)
   #
   # @link      https://expressionengine.com/
   # @copyright Copyright (c) 2003-2018, EllisLab, Inc. (https://ellislab.com)
   # @license   https://expressionengine.com/license Licensed under Apache License, Version 2.0

Entry Manager
=============

.. rst-class:: cp-path

**Control Panel Location:** :menuselection:`Edit`

.. Overview

In this section you can edit and update previously posted Entries. The list can
be filtered by Channel, Category, Status, or Date range, and it can be sorted
by ID, Title, Comments, Date, and Status. In addition, you can select multiple
entries using the checkboxes on the right, then delete them.

.. Screenshot (optional)

.. figure:: ../../images/edit.png

.. Permissions

Permission Restrictions
-----------------------

* Access settings: Design & Content
* Allowed actions: Create Entries
* Allowed actions: Edit Own Entries
* Allowed actions: Delete Own Entries
* Allowed actions: Edit Entries, By Others
* Allowed actions: Delete Entries, By Others
* Allowed channels

Actions
-------

.. contents::
  :local:

.. Each Action

Search entries
~~~~~~~~~~~~~~

This will search entries by title, respecting the current filters.

Create New
~~~~~~~~~~

This will take you to the :doc:`create form <create>` for the indicated channel.

Title links
~~~~~~~~~~~

This will take you to the :doc:`edit form <create>` for that entry. This is
identical to the Edit_ icon.

Comment links
~~~~~~~~~~~~~

If an entry has comments the number of comments will be a link that will take you to the :doc:`comments/index`.

Manage
~~~~~~

The icons in the manage column perform actions on the entry in its row.

View
^^^^

When a Channel has a defined Preview URL or the Entry has a Page URI this action will be made available and will take you to the :ref:`entry_live_preview`.

Edit
^^^^

This will take you to the :doc:`edit form <create>`.

Bulk Actions
~~~~~~~~~~~~

The checkbox in the right-most column of the table selects a button for a bulk
action. When at least one checkbox is checked the bulk action dropdown menu and
submit button will be made available in the lower righthand corner of the table.

Remove
^^^^^^

The selected entries will be removed. Removing entries will cause a
confirmation modal to appear that will summarize the action.

.. toctree::
	:hidden:
	:titlesonly:

	comments/index
