.. # This source file is part of the open source project
   # ExpressionEngine User Guide (https://github.com/ExpressionEngine/ExpressionEngine-User-Guide)
   #
   # @link      https://expressionengine.com/
   # @copyright Copyright (c) 2003-2018, EllisLab, Inc. (https://ellislab.com)
   # @license   https://expressionengine.com/license Licensed under Apache License, Version 2.0

Word Censorship
===============

.. rst-class:: cp-path

**Control Panel Location:** :menuselection:`Settings --> Word Censorship`

.. Overview

This section of the Control Panel allows you to enable word censoring. It is
also where you define the list of censored words.

.. Screenshot (optional)

.. Permissions

Permission Restrictions
-----------------------

* Access settings: General Settings

Settings
--------

.. contents::
  :local:
  :depth: 1

.. Each Action/Section

.. _censor-words-enable-label:

Enable censorship?
~~~~~~~~~~~~~~~~~~

You may enable or disable word censoring. If you select "Yes", the
system will replace any specified words in channel entries, comments,
forum posts, etc. according to your preference below.

.. _censor-replace-label:

Replacement characters
~~~~~~~~~~~~~~~~~~~~~~

You may optionally specify a word or phrase to be used when replacing
censored words. For example, if you set "tisk tisk" as your replacement
word, and "shucks" is in your censored list, then anytime "shucks" is
used it will be replaced with "tisk tisk". If you do not set this
preference, a pound symbol will be used for each character that is
censored, so "shucks" would be converted to "######".

.. _censor-words-label:

Words to censor
~~~~~~~~~~~~~~~

Specify a list of words to censor. Wildcards are allowed. For example,
``test*`` would censor the words "test", "testing", and "tester", while
``*gress`` would censor the words "progress" and "congress".