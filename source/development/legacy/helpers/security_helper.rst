.. # This source file is part of the open source project
   # ExpressionEngine User Guide (https://github.com/ExpressionEngine/ExpressionEngine-User-Guide)
   #
   # @link      https://expressionengine.com/
   # @copyright Copyright (c) 2003-2018, EllisLab, Inc. (https://ellislab.com)
   # @license   https://expressionengine.com/license Licensed under Apache License, Version 2.0

###############
Security Helper
###############

.. highlight:: php

The Security Helper file contains security related functions. This helper is loaded using the following code::

	ee()->load->helper('security');

*******************
Available Functions
*******************

.. function:: xss_clean($str[, $is_image = FALSE])

	:param	string	$str: Input data
	:param	bool	$is_image: Whether we're dealing with an image
	:returns:	XSS-clean string
	:rtype:	string

	Provides Cross Site Script Hack filtering.

	This function is an alias for :meth:`Security::xss_clean()`.

.. function:: sanitize_filename($filename)

	:param	string	$filename: Filename
	:returns:	Sanitized file name
	:rtype:	string

	Provides protection against directory traversal.

	This function is an alias for :meth:`Security::sanitize_filename()`.

.. function:: strip_image_tags($str)

	:param	string	$str: Input string
	:returns:	The input string with no image tags
	:rtype:	string

	This is a security function that will strip image tags from a string. It leaves the image URL as plain text.

	Example::

		$string = strip_image_tags($string);

.. function:: encode_php_tags($str)

	:param	string	$str: Input string
	:returns:	Safely formatted string
	:rtype:	string

	This is a security function that converts PHP tags to entities.

	.. note:: :func:`xss_clean()` does this automatically, if you use it.

	Example::

		$string = encode_php_tags($string);
