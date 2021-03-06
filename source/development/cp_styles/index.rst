.. # This source file is part of the open source project
   # ExpressionEngine User Guide (https://github.com/ExpressionEngine/ExpressionEngine-User-Guide)
   #
   # @link      https://expressionengine.com/
   # @copyright Copyright (c) 2003-2018, EllisLab, Inc. (https://ellislab.com)
   # @license   https://expressionengine.com/license Licensed under Apache License, Version 2.0

Control Panel Styles
====================

.. contents::
  :local:

.. highlight:: php

Style Guidelines
----------------

For UI we have published the `ExpressionEngine 3.0 CP style-guide
<https://ellislab.com/style-guide>`_ which should be used when
building user interfaces for the Control Panel.

For UX we have published the (link) Human Interface Guidelines for
interactions in the Control Panel so users have a consistent
experience throughout the application.

PHP Related Guidelines
----------------------

External Links
~~~~~~~~~~~~~~

To protect the users control panel URL from ending up in web server
referrer logs, use :meth:`Cp::masked_url` from the Control Panel Class::

  ee()->cp->masked_url('http://www.google.com');

Will result in::

  https://example.com?URL=http://www.google.com

.. _cp_internal_links:

Internal Links
~~~~~~~~~~~~~~

Internal control panel links should be generated with the ``ee('CP/URL')``
helper function which generates control panel URLs based on parameters
passed in.

For example, to link to the ``publish`` controller, pass it in
as the first parameter to ``ee('CP/URL')``::

  ee('CP/URL', 'publish');

To link to a particular method in a controller, add it to the parameter
with a slash::

  ee('CP/URL', 'publish/method_name');

If the method accepts arguments, they can be passed in cleanly by adding
them on the end separated by a slash::

  ee('CP/URL', 'publish/method_name/5');

If the link requires any other GET parameters, they can be passed in via
an associative array in the second parameter::

  ee('CP/URL', 'publish/edit', array('filter_by_channel' => $channel_id));

See :doc:`/development/services/url` for the full documentation.

Control Panel Constants
~~~~~~~~~~~~~~~~~~~~~~~

- ``BASE`` - Name of control panel file with the users session id
- ``AMP`` - Will render ``&amp;``
- ``AJAX_REQUEST`` - Returns Boolean TRUE if a request was made via an Ajax Request
- ``QUERY_MARKER`` - Renders a query marker (``?``)
- ``APPPATH`` - Server path to the ``system/ee/legacy`` directory
- ``PATH_ADDONS`` - Server path to the first-party addons directory
- ``PATH_THIRD`` - Server path to the third-party addons directory
- ``PATH_JQUERY`` - Server path to jQuery files at
  ``themes/ee/javascript/compressed/jquery``
