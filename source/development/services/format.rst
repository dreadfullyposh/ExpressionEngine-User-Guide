##############
Format Service
##############

.. contents::
  :local:
  :depth: 1

.. highlight:: php

********
Overview
********

The Format service offers a number of common formatting tasks as a convenience and consolidated way for ExpressionEngine handles these tasks. The Formatter handles common string and number presentational needs.

::

  $display_size = ee('Format')->make('Number', $content)->bytes();

The Format service is a factory to the various formatters available. If you need the factory, use ``ee('Format')``. If you need a Formatter, use ``ee('Format')->make($formatter, $content)``.

Format Factory
--------------

.. namespace:: EllisLab\ExpressionEngine\Service\Formatter

.. class:: FormatterFactory

.. method:: make($formatter_name, $content)

  Makes a Formatter object.

  :param string $formatter_name: Formatter name
  :param mixed $content: The content to be formatted
  :returns: A Formatter object
  :rtype: Formatter

All Formatters
--------------

.. class:: Formatter

.. method:: compile()

  Compiles and returns the URL as a string. Typically this is used when you
  need to use a content as an array key, or want to json_encode() the content.

  :returns: string
  :rtype: The content

.. method:: __toString()

  When accessed as a string simply complile the content and return that.

  :returns: string
  :rtype: The content

.. note:: When using Formatters, if you just need the string and not the object for further processing, you can use PHP's type casting::

    $array = array('size' => (string) ee('Format')->make('Number', $content)->bytes());


Number Formatter
----------------

.. namespace:: EllisLab\ExpressionEngine\Service\Formatter\Formats

.. class:: Number

.. method:: bytes($abbr = TRUE, $include_markup = TRUE))

  Formats a binary byte multiple into a human-readable measure of units, e.g. B, KB, MB, GB.

  :param bool $abbr: Use the abbreviated form of the byte format
  :param bool $include_markup: Output with ``<abbr>`` HTML. Only affects abbreviated forms.
  :returns: A Formatter object
  :rtype: Number

When to use ``compile()``
-------------------------

The Formatter object has a magic ``__toString()`` method that compiles the object
into a string when the object is treated as a string (see: PHP's documentation
on the magic `__toString() method
<http://php.net/manual/en/language.oop5.magic.php#object.tostring>`_ for more
information). The ``compile()`` method exists for those occasions when the
object is treated as an object but you need a string instead. As per `PHP's
documentation on arrays <http://php.net/manual/en/language.types.array.php>`_:
"Arrays and objects can not be used as keys. Doing so will result in a warning:
*Illegal offset type.*" You will also want to compile the object when you want
to JSON encode the content otherwise you will get a JSON object instead of a string.

For example::

  ee()->javascript->set_global(array(
    'form.some_input.value' => ee('Format')->make('String', $content)->attribute_escape()->compile()
  ));