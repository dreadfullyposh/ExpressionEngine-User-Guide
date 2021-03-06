.. # This source file is part of the open source project
   # ExpressionEngine User Guide (https://github.com/ExpressionEngine/ExpressionEngine-User-Guide)
   #
   # @link      https://expressionengine.com/
   # @copyright Copyright (c) 2003-2018, EllisLab, Inc. (https://ellislab.com)
   # @license   https://expressionengine.com/license Licensed under Apache License, Version 2.0

CP/URL Service
===============

.. contents::
  :local:
  :depth: 1

.. highlight:: php

Simple Example
--------------

Building URLs in the Control Panel is a common, but exacting task. We have a
CP/URL Service to make building these URLs simple. For example::

  $url = ee('CP/URL', 'publish/create/1');

The service automatically takes care of appending the session ID when it is
required. For more complex URLs we also provide means of adding arbitrary query string variables using the ``make`` method::

  $url = ee('CP/URL')->make('publish/edit', array('filter_by_channel' => 1));

Or::

  $url = ee('CP/URL', 'publish/edit')
  	->setQueryStringVariable('filter_by_channel', 1);

When to use ``compile()``
-------------------------

The CP/URL object has a magic ``__toString()`` method that compiles the object
into a string when the object is treated as a string (see: PHP's documentation
on the magic `__toString() method
<http://php.net/manual/en/language.oop5.magic.php#object.tostring>`_ for more
information). The ``compile()`` method exists for those occasions when the
object is treated as an object but you need a string instead. As per `PHP's
documentation on arrays <http://php.net/manual/en/language.types.array.php>`_:
"Arrays and objects can not be used as keys. Doing so will result in a warning:
*Illegal offset type.*" You will also want to compile the object when you want
to JSON encode the URL otherwise you will get a JSON object instead of a string.

For example::

  $breadcrumb = array(
    ee('CP/URL', 'addons/settings/fortune_cookie')->compile() => lang('fortune_cookie_management')
  );

  ee()->javascript->set_global(array(
    'fortune_cookie.autosave.URL' => ee('CP/URL', 'addons/settings/fortune_cookie/autosave/')->compile()
  ));


CP/URL Service Methods
-----------------------

.. namespace:: EllisLab\ExpressionEngine\Library\CP

.. class:: URLFactory

.. method:: make($path, $qs = array(), $cp_url = '', $session_id = NULL)

  Makes a URL object.

  :param string $path: The path of the url (ie. 'publish/edit/2')
  :param array $qs: An associative array of query string variables to append to the rendered URL.
  :param string $cp_url: The base URL to which all else will be appended (ie. 'admin.php')
  :param string|NULL $session_id: A session ID to append to the rendered URL
  :returns: A URL object
  :rtype: URL

.. method:: makeFromString($url)

  Makes a URL object from a string.

  :param string $url: The URL to be parsed into a URL object
  :returns: A URL object
  :rtype: URL

.. method:: getCurrentUrl()

  Makes a URL object representing the requested URL.

  :returns: A URL object
  :rtype: URL

.. method:: decodeUrl($url)

  Decodes a base64 encoded, seralized URL object.

  :returns: A URL object
  :rtype: URL

CP/URL Object Methods
-----------------------

.. class:: URL

.. method:: setQueryStringVariable($key, $value)

  Sets a key and value which will become the Query String of the request

  :param string $key: The name of the query string variable
  :param string $value: The value of the query string variable
  :returns: $this
  :rtype: URL

.. method:: addQueryStringVariables($values)

  Sets a values in bulk which will become the Query String of the request

  :param array $values: An associative array of keys and values
  :returns: $this
  :rtype: URL

.. method:: compile()

  Compiles and returns the URL as a string. Typically this is used when you
  need to use a URL as an array key, or want to json_encode() a URL.

  :returns: string
  :rtype: The URL

.. method:: __toString()

	When accessed as a string simply complile the URL and return that.

  :returns: string
  :rtype: The URL
