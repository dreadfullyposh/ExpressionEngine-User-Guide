Security & Privacy
==================

.. rst-class:: cp-path

**Control Panel Location:** :menuselection:`Settings --> Security & Privacy`

.. Screenshot (optional)

.. Overview

This section of the Control Panel allows you to define the basic
security-related settings for your website. These are security settings that
apply throughout the website/system.

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

CP session type
~~~~~~~~~~~~~~~

This determines how sessions are handled for the Control Panel. You may
use cookies, session IDs, or a combination. The available options are:

- **Cookies and session ID**: Both cookies and URL session ID
  parameters are used to track the admin user. This is the default
  setting, and is the most secure since it relies on two individual
  cookies and a URL session ID.
- **Cookies only**: Only cookies are used to track the admin user. When
  this setting is used a "remember me" checkbox will appear next to the
  Control Panel login page, enabling users to stay permanently logged
  in.
- **Session ID only**: Only URL session IDs are used to track the admin
  user. This option should only be used if your desktop computer
  prevents you from accepting cookies in the event you are behind a
  firewall or due to some other technical issue.

Website Session type
~~~~~~~~~~~~~~~~~~~~

This determines how sessions are handled for the front-end of the site.
You may use cookies, session IDs, or a combination. The available
options are:

- **Cookies and session ID**: Both cookies and URL session ID
  parameters are used to track the user throughout their visit.
- **Cookies only**: Only cookies are used to track the user throughout
  their visit. This is the default setting, and generally the best
  option since it prevents URLs from showing session IDs.
- **Session ID only**: Only URL session IDs are used to track the user
  throughout their visit.

Domain
~~~~~~

Optionally specify a domain the cookie is available to. By default, the
exact hostname of the requested page is set as the cookie domain. For
example, if the page at ``http://www.example.com/blog/an-entry-title``
is loaded and the cookie domain is left blank in ExpressionEngine's
configuration, the browser will use ``www.example.com`` as the cookie
domain. The browser will only make these cookies available when the
page's hostname is *exactly* ``www.example.com``.

If the cookie domain is explicitly specified, however, the browser will
make the cookie available whenever the requested page's hostname
*contains* the cookie domain. For example, setting the cookie domain to
``.example.com`` will ensure the cookie is shared whenever the requested
page's hostname includes ``example.com``, ``www.example.com``,
``admin.example.com``, ``blog.example.com``, and so on.

If you're running multiple subdomains on a single ExpressionEngine
installation and want member sessions to be valid across all subdomains,
you should explicitly set the cookie domain.

.. note:: There's an important difference between ``example.com`` and
    ``.example.com``. When the cookie domain begins with a dot, browsers
    match any hostname that *includes* the cookie domain. Without the
    dot prefix, browsers are looking for an exact hostname match in the
    URL, which means cookies will not be available to subdomains. A
    cookie set by PHP with an explicitly specified cookie domain will
    always include the dot prefix, whether or not one is included in
    this ExpressionEngine setting. For clarity's sake, the examples here
    include a leading dot when the cookie domain is being explicitly
    set.

.. note:: Browsers will not save cookies if the specified cookie domain
    isn't included in the request's hostname. In other words, a site can
    only set cookies for ``.example.com`` if its hostname actually
    includes ``example.com``.

Path
~~~~

Optionally specify a cookie path. When a cookie path is set, the browser
will only share cookies with ExpressionEngine when the beginning of the
URL path matches the cookie path. For example, if the cookie path is set
to ``/blog/``, a cookie for the domain ``example.com`` will only be sent
by the browser if the URL begins with ``http://example.com/blog/``. This
can be useful if you have ExpressionEngine installed in a sub-directory
and want to ensure that only that particular installation has access to
the cookies it sets.

Prefix
~~~~~~

Specify a prefix for the cookie name set by ExpressionEngine. This
protects against collisions from separate ExpressionEngine installations
on the same cookie domain.

Send cookies over HTTP only?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Send cookies securely?
~~~~~~~~~~~~~~~~~~~~~~

Allow members to change username?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

As the name suggests, this setting determines whether or not members are
allowed to change their own usernames after registration. (Members will
always be able to change their own screen names.)

Minimum username length
~~~~~~~~~~~~~~~~~~~~~~~

You may specify the minimum length required for a member username during
new member registration. Specify the minimum number of characters
required.

Allow multiple logins?
~~~~~~~~~~~~~~~~~~~~~~

Set whether an account can have multiple active sessions at one time.

.. note::

   This feature is incompatible with the "Cookies Only" session type.

Require user agent and IP for login?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

If this preference is set to "Yes", then users will not be able to log
in unless their browser (or other access device) correctly supplies
their IP address and User Agent (browser) information. Having this set
to "Yes" can help prevent hackers from logging in using direct socket
connections or from trying to access the system with a masked IP
address.

Enable password lock out?
~~~~~~~~~~~~~~~~~~~~~~~~~

When this preference is set to "Yes", the system will lock a member
account if more than four invalid login attempts are made within a
specified time period (see next setting). This preference is designed to
deter hackers from using collision attacks to guess poorly chosen
passwords. The account remains locked for the duration of the time
period. Once the period expires it becomes unlocked.

Password lock out interval
~~~~~~~~~~~~~~~~~~~~~~~~~~

This setting is used together with the previous preference. Here you can
determine, in minutes, the time interval over which more than four
invalid login attempts will trigger a lockout. You may use decimals to
indicate fractions of a minute: e.g. 1.5 equals one and a half minutes.

Require secure passwords?
~~~~~~~~~~~~~~~~~~~~~~~~~

If this preference is set to "Yes", then users will be required to
choose a minimally "secure" password. In this case, a password
containing at least one uppercase character, one lowercase character,
and one numeric character. Passwords that follow this basic formula are
much more difficult to guess.

Minimum password length
~~~~~~~~~~~~~~~~~~~~~~~

You may specify the minimum length required for a member password during
new member registration. Specify the minimum number of characters
required. It is common practice to require passwords at least eight (8)
characters long.

Allow dictionary words in passwords?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Set whether words commonly found in the dictionary can be used as
passwords. Disabling will make "dictionary attacks" by hackers much more
difficult.

.. note:: In order to be able to use this setting you must have :ref:`a dictionary file <dict-passwds-file-label>` installed.

Dictionary file
~~~~~~~~~~~~~~~

This is the filename of the dictionary file used for the previous
preference. Download the `dictionary file
<https://ellislab.com/asset/file/dictionary.zip>`__, unzip, and upload
the text file (:file:`dictionary.txt`) to
:file:`system/expressionengine/config/`.

Enter only the filename of the file (:file:`dictionary.txt`) in this
field.

Deny duplicate data?
~~~~~~~~~~~~~~~~~~~~

This option prevents data submitted by users (such as comments) from
being processed if it is an exact duplicate of data that already exists.
This setting is designed to deter automated spam attacks as well as
multiple accidental submissions.

Require user agent and IP for posting?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Similar to the previous setting, when turned on, this setting requires
IP address and user agent information to be supplied when submitting
comments.

Apply XSS filtering?
~~~~~~~~~~~~~~~~~~~~

Checks all file uploads for code injection attempts before finalizing the upload.
Superadmins are exempt from image XSS filtering.