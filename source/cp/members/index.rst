.. # This source file is part of the open source project
   # ExpressionEngine User Guide (https://github.com/ExpressionEngine/ExpressionEngine-User-Guide)
   #
   # @link      https://expressionengine.com/
   # @copyright Copyright (c) 2003-2018, EllisLab, Inc. (https://ellislab.com)
   # @license   https://expressionengine.com/license Licensed under Apache License, Version 2.0

Member Manager
==============

.. rst-class:: cp-path

**Control Panel Location:** :menuselection:`Members`

.. Overview

This page is used both to search and to browse through active members within
your ExpressionEngine installation. Also, you can filter the members by member
group and search members.

.. Screenshot (optional)

.. figure:: ../../images/members.png

.. Permissions

Permission Restrictions
-----------------------

* Access settings: Members
* Member Groups Allowed actions: Create New Groups
* Members Allowed actions: Create New Members
* Members Allowed actions: Edit Members
* Members Allowed actions: Delete Members


Actions
-------

.. contents::
  :local:
  :depth: 1

.. Each Action

.. include:: /cp/members/_header.rst

Sidebar
~~~~~~~

All Members
^^^^^^^^^^^

Display all the members. This is the default view.

New Member
^^^^^^^^^^

This will take you to the :doc:`create member form <create>`.

Pending Activation
^^^^^^^^^^^^^^^^^^

This will display only pending members.

Ban Settings
^^^^^^^^^^^^

This will take you to :doc:`bans`.

Member Groups
^^^^^^^^^^^^^

This will allow you to :doc:`manage your member groups <groups/index>`.

New Member Group
~~~~~~~~~~~~~~~~

This will take you to the :doc:`create member group form <groups/form>`.

Member Fields
^^^^^^^^^^^^^

This will allow you to :doc:`manage your custom member fields <fields/index>`.

Username Links
~~~~~~~~~~~~~~

This will take you to the member's :doc:`profile <profile/index>`.

Username Email Links
~~~~~~~~~~~~~~~~~~~~

This will allow you to email the member using your default mail client.

Manage
~~~~~~

The icons in the manage column perform actions on the member in its row.

Edit
^^^^

This will take you to the member's :doc:`profile <profile/index>`.

Bulk Actions
~~~~~~~~~~~~

The checkbox in the right-most column of the table selects a button for a bulk
action. When at least one checkbox is checked the bulk action dropdown menu and
submit button will be made available in the lower righthand corner of the table.

Remove
^^^^^^

The selected members will be removed. Removing a member will cause a
confirmation modal to appear that will summarize the action.

.. toctree::
  :glob:
  :hidden:
  :titlesonly:

  *
  */index
