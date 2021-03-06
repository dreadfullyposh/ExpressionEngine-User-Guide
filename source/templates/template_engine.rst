.. # This source file is part of the open source project
   # ExpressionEngine User Guide (https://github.com/ExpressionEngine/ExpressionEngine-User-Guide)
   #
   # @link      https://expressionengine.com/
   # @copyright Copyright (c) 2003-2018, EllisLab, Inc. (https://ellislab.com)
   # @license   https://expressionengine.com/license Licensed under Apache License, Version 2.0

The Template Engine
===================

At a basic level, :ref:`Templates <getting_started_templates>` contain
almost everything you want displayed on the front-end of the site. When
ExpressionEngine serves up each Template, the system must go through a
rendering process to parse out the Tags, Variables, Template Partials, and Embeds
being used in the Template.

.. note:: The information in this article applies only to rendering
   Templates. It doesn't apply to rendering theme files such as those
   used for :doc:`Member Profiles
   </cp/design/members/index>`, or the :doc:`Discussion
   Forum </add-ons/forum/forum_themes>` module.

ExpressionEngine goes through several stages to fully process each
Template, and this article exposes the order of those rendering stages.
Understanding how the system renders a template can help immensely when
building pages and troubleshooting problems.

.. note:: As of 2.9.0 conditional tags evaluate *when ready*.

Rendering Stages
----------------

The Template Engine processes the selected template fully from top to
bottom through each rendering stage.

#. Determine template to process based on request :doc:`URI </urls/url_structure>`

#. Get **template from database**, check :doc:`template access permissions </cp/design/template/edit>`, and increment the :doc:`hit counter </templates/hit_counter>`

#. If it exists, get :doc:`template from file </templates/templates_as_files>`

#. If template type is :doc:`static </cp/design/template/create>`, return template and end parsing

#. Parse (as a group, so order is irrelevant):

   * {freelancer_version}
   * :doc:`Template partials </templates/globals/template_partials>`
   * :ref:`MSM variables <msm_variables>`: {site_id}, {site_label}, {site_shortname}
   * :ref:`{last_segment} <global_last_segment>`
   * :ref:`Member variables <member_variables>`

#. Parse :doc:`segment variables </templates/globals/url_segments>`

#. Parse :ref:`embed variables <embed_variables>`

#. Parse :ref:`layout variables <layout_variables>`

#. Parse :ref:`date formatting string constants <template_date_formatting_constants>`

#. Parse :ref:`{template_edit_date} <global_template_edit_date>`

#. Parse :ref:`{current_time} <global_current_time>`

#. If present, get :ref:`cached template <caching_template_caching>`, then skip to the **advanced
   conditionals** parsing stage

#. Parse :ref:`PHP on Input <php_parsing_stage>`

#. Parse :doc:`conditional tags <conditionals>`

#. Assign and parse :doc:`preload_replace variables </templates/globals/preload_replacement>`

#. Parse **module and plugin tags**

   * See notes on how :ref:`nested plugins <templates_nested_plugins>` are parsed.
   * If any module's :ref:`{if no_results} <channel_entries_if_no_results>` tag pair evaluates true, a :ref:`{redirect} <global_redirect>` variable within the tag pair will be processed immediately.

#. Parse :ref:`PHP on Output <php_parsing_stage>`

#. Write **template to cache file**

#. Parse :doc:`conditional tags <conditionals>`

#. Process :doc:`template layouts </templates/layouts>`

#. Process :doc:`embedded templates </templates/embedding>`

#. Process :ref:`redirect variable <global_redirect>`

#. Parse :doc:`template-variables
   </templates/globals/template_variable>`

#. Parse some :doc:`standard global variables </templates/globals/single_variables>` (separately, in order given):

   * {hits}
   * {ip_address}
   * {ip_hostname}
   * {homepage}
   * {cp_url}
   * {site_name}
   * {site_url}
   * {site_index}
   * {webmaster_email}
   * {stylesheet}
   * {encode}
   * {debug_mode}
   * {gzip_mode}
   * {app_version}
   * {version}
   * {app_build}
   * {build}
   * {charset}
   * {lang}
   * {doc_url}
   * {password_max_length}
   * {theme_folder_url}
   * {member_profile_link}
   * {captcha}

#. Add :ref:`CSRF tokens <dev_guidelines_csrf_protection>` to forms and parse :ref:`{csrf_token} <global_csrf_token>`

#. Parse remaining :doc:`standard global variables </templates/globals/single_variables>` (separately, in order given):

   * {member_id}
   * {group_id}
   * {group_description}
   * {group_title}
   * {member_group}
   * {username}
   * {screen_name}
   * {email}
   * {ip_address}
   * {location}
   * {total_entries}
   * {total_comments}
   * {private_messages}
   * {total_forum_posts}
   * {total_forum_topics}
   * {total_forum_replies}

#. Parse :doc:`path variables </templates/globals/path>` (including :doc:`{route=...} paths </urls/template_routes>`)
