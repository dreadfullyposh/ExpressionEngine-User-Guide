.. # This source file is part of the open source project
   # ExpressionEngine User Guide (https://github.com/ExpressionEngine/ExpressionEngine-User-Guide)
   #
   # @link      https://expressionengine.com/
   # @copyright Copyright (c) 2003-2018, EllisLab, Inc. (https://ellislab.com)
   # @license   https://expressionengine.com/license Licensed under Apache License, Version 2.0

Member Module Registration Extension Hooks
==========================================

.. contents::
  :local:
  :depth: 1

.. highlight:: php

member_member_register
----------------------

.. function:: member_member_register($data, $member_id)

  Additional processing when a member is registering through the user
  side of ExpressionEngine.

  How it's called::

    ee()->extensions->call('member_member_register', $data, $member_id);
    if (ee()->extensions->end_script === TRUE) return;

  :param array $data: Array of data about the new member like username,
    email, screen_name
  :param int $member_id: The new member's id
  :rtype: Void

  .. versionadded:: 1.4.0

member_member_register_errors
-----------------------------

.. function:: member_member_register_errors($this)

  Add additional error checking to the member registration form.

  How it's called::

    ee()->extensions->call('member_member_register_errors', $this);
    if (ee()->extensions->end_script === TRUE) return;

  :param object $this: The current Member_register object
  :rtype: Void

  .. versionadded:: 2.5.0

member_member_register_start
----------------------------

.. function:: member_member_register_start()

  Additional processing prior to/take control of member registration
  routine.

  How it's called::

    ee()->extensions->call('member_member_register_start');
    if (ee()->extensions->end_script === TRUE) return;

  :rtype: Void

  .. versionadded:: 1.4.2

member_register_validate_members
--------------------------------

.. function:: member_register_validate_members($member_id)

  Additional processing when member(s) are self validated

  How it's called::

    ee()->extensions->call('member_register_validate_members', $member_id);
    if (ee()->extensions->end_script === TRUE) return;

  :param int $member_id: the ID of the member
  :rtype: Void

  .. versionadded:: 1.5.2
