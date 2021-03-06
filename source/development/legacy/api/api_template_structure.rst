.. # This source file is part of the open source project
   # ExpressionEngine User Guide (https://github.com/ExpressionEngine/ExpressionEngine-User-Guide)
   #
   # @link      https://expressionengine.com/
   # @copyright Copyright (c) 2003-2018, EllisLab, Inc. (https://ellislab.com)
   # @license   https://expressionengine.com/license Licensed under Apache License, Version 2.0

ExpressionEngine Template Structure API
=======================================

.. contents::
  :local:
  :depth: 1

.. highlight:: php

Calling the Class
-----------------

.. class:: Api_template_structure

  The Template Structure class is called with the ``api->instantiate()``
  function::

    ee()->load->library('api'); ee()->legacy_api->instantiate('template_structure');

Function Reference
------------------

Get Group Info
~~~~~~~~~~~~~~

.. method:: get_group_info($group_id)

  Get template group metadata::

    ee()->api_template_structure->get_group_info((int) $group_id);

  :param int $group_id: Integer of the template group
  :returns: Database result object or returns ``FALSE`` on error
  :rtype: Database result object/Boolean

Create Template Group
~~~~~~~~~~~~~~~~~~~~~

.. method:: create_template_group($data[, $duplicate_group = FALSE])

  Creates a new template group::

    ee()->api_template_structure->create_template_group((array) $data, (int) $duplicate_group = FALSE)

  :param array $data: Associative array of template group data must
    include ``group_name``, can include keys below
  :param int $duplicate_group: The ``template_group`` ID to duplicate
  :returns: ID of newly created group or ``FALSE`` on error
  :rtype: Integer/Boolean

  Example Usage::

    $data = array(
        'group_name'        => 'home',
        'group_order'       => 2,     // Defaults to template_group count + 1
        'is_site_default'   => 'n',   // Defaults to 'n'
        'site_id'           => 1      // Defaults to config->item('site_id')
    );

    ee()->api_template_structure->create_template_group($data, 1);

File Extensions
~~~~~~~~~~~~~~~

.. method:: file_extensions($template_type)

  Returns a file extension that corresponds to the template type::

    ee()->api_template_structure->file_extensions((str) $template_type);

  :param string $template_type: Name of the template type
  :returns: File extension if template type exists or an empty string
  :rtype: String

  Template Types:

  - ``webpage``
  - ``static``
  - ``feed``
  - ``css``
  - ``js``
  - ``xml``
