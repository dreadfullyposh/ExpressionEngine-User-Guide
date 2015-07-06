Model Service
=============

.. contents::
  :local:
  :depth: 1

.. highlight:: php

Simple Example
--------------

ExpressionEngine has a complex set of data types, such as Channels,
Members, and Categories. These have properties and constraints, as well
as relationships and complex storage requirements. The model service
helps smooth out interacting with ExpressionEngine's data types by
providing an API that mimics their natural language description as
closely as is feasible. You do not query for ``channel_data`` joined on
``channel_titles``; instead, you simply get a channel entry::

  $my_first_entry = ee('Model')->get('ChannelEntry')->filter('title', 'Hello World')->first();

  $my_first_entry->title = 'Hello WORLD!!!';
  $my_first_entry->save();

Creating Your Own Models
------------------------

A model class has four requirements. It must ...

- ... extend ``EllisLab\ExpressionEngine\Service\Model\Model``
- ... define a primary key
- ... define a table name
- ... define its properties

::

  use EllisLab\ExpressionEngine\Service\Model\Model;

  class MyModel extends Model {

    protected static $_primary_key = 'id';
    protected static $_table_name = 'my_awesome_table';

    protected $id;
    protected $name;
    protected $email;

  }

.. note:: The properties must be declared as protected.

Events
------

All models automatically support a simple event system.

To listen to an event on a model, use the ``on`` method::

  $my_model->on('boom', function($model)
  {
    echo 'boom event happened on '.$model->getName();
  });

To initiate an event, use the ``emit`` method::

  $my_model->emit('boom');

The first parameter passed to the event handler will always be the
model instance. Any additional parameters passed to emit will also
be passed to the event handler::

  $my_model->on('boom', function($model, $year)
  {
    echo 'boom event happened on '.$model->getName().' in '.$year;
  });

  $my_model->emit('boom', 2015);

Inside your model you can automatically bind to events. To do so, first
create a public method with the format ``on<EventName>``, and then listen
to the event by adding a static ``$_events`` array that lists the event::

  protected static $_events = array('beforeSave');

  public function onBeforeSave()
  {
    echo 'about to save!';
  }

.. note:: Event names typically start with a lowercase letter, but the
  method name will have them as uppercase due to the ``on`` prefix.

Default Events
~~~~~~~~~~~~~~


+----------------+----------------------------------+-------------------------+
| Event Name     | When                             | Parameters              |
+================+==================================+=========================+
| beforeInsert   | Before saving a new model        | None                    |
+----------------+----------------------------------+-------------------------+
| afterInsert    | After saving a new model         | None                    |
+----------------+----------------------------------+-------------------------+
| beforeUpdate   | Before saving an existing model  | Array of changed values |
+----------------+----------------------------------+-------------------------+
| afterUpdate    | After saving an existing model   | Array of changed values |
+----------------+----------------------------------+-------------------------+
| beforeSave     | Before saving a model            | None                    |
+----------------+----------------------------------+-------------------------+
| afterSave      | After saving a model             | None                    |
+----------------+----------------------------------+-------------------------+
| beforeValidate | Before validating                | None                    |
+----------------+----------------------------------+-------------------------+
| afterValidate  | After validating                 | None                    |
+----------------+----------------------------------+-------------------------+
| beforeDelete   | Before deleting                  | None                    |
+----------------+----------------------------------+-------------------------+
| afterDelete    | After deleting                   | None                    |
+----------------+----------------------------------+-------------------------+

Relationships
-------------




Validation
----------

Validation rules are added using the same format as the :doc:`Validation
Service <./validation>`. They should be added as a static property called
``$_validation_rules``::

  protected static $_validation_rules = array(
    'name'  => 'required',
    'email' => 'required|email'
  );

To test a model for errors, call the `->validate()` method. The returned
object will be a result class of the Validation Service::

  $result = $model->validate();

  if ($result->isValid())
  {
    // yay
  }

Getters and Setters
-------------------

By default setting and getting of properties behaves the way it does for
any object. However, you can create your own modifying getters and
setters by creating methods in the format of ``get__<property>`` or
``set__<property>``::

  protected $first_name;
  protected $last_name;

  protected function get__name()
  {
    return $this->first_name.' '.$this->last_name;
  }

  protected function set__name($value)
  {
    list($first, $last) = explode(' ', $value);

    $this->setRawProperty('first_name', $first);
    $this->setRawProperty('last_name', $last);
  }

  $my_model->name = 'Bob Bobson';
  $my_model->first_name; // Bob

.. note:: These methods break the camelCase naming convention in order
  to match the snake_case property names. It also serves as a clear
  indicator that these methods should not be called directly.

When setting properties manually you should take care to use
`setRawProperty`, which will correctly track changes to the property.

Typed Columns
-------------

Model properties can have basic type constraints set on them. These
constraints allow for simple get/set typecasting of common values. They
are defined in a static property called ``$_typed_columns``::

  protected static $_typed_columns = array(
    'model_id' => 'int',
    'created_at' => 'timestamp'
  );

  $my_model->model_id = '5'; // set to int 5
  $my_model->model_id; // always returns an integer

  $my_model->created_at; // returns a DateTime object
  $my_model->created_at = new DateTime('2015-01-30'); // sets an int timestamp
  $my_model->created_at = 1421558529; // also ok

The available options include:

+------------+-------------------+------------------+
| Name       | Setting           | Getting          |
+============+===================+==================+
| bool       | Cast to boolean   | Cast to boolean  |
+------------+-------------------+------------------+
| int        | Cast to integer   | Cast to integer  |
+------------+-------------------+------------------+
| float      | Cast to float     | Cast to float    |
+------------+-------------------+------------------+
| string     | Cast to string    | Cast to string   |
+------------+-------------------+------------------+
| boolString | Cast to y/n       | Cast to boolean  |
+------------+-------------------+------------------+
| boolInt    | Cast to 0/1       | Cast to boolean  |
+------------+-------------------+------------------+
| timestamp  | Cast to timestamp | Cast to DateTime |
+------------+-------------------+------------------+

Composite Columns
-----------------

Sometimes a database column may contain serialized data. Instead of
treating this data merely as a string or array (using getters and setters),
you can automatically turn it into sub-objects by defining a composite
column.

First, add a static ``$_composite_columns`` array to your model where the
key is the name of the column and the value is the name of the composite
class you wish to use.

::

  protected static $_composite_columns = array(
    'coordinates' => 'Coordinates'
  );

Next, create a class that describes the composite column. Place it under
``<your\model\namespace>\Column\``::

  use EllisLab\ExpressionEngine\Service\Model\Column\Composite;

  class Coordinates extends Composite {

    protected $latitude;
    protected $longitude;

  }

Lastly, define two methods - ``serialize`` and ``unserialize`` on your
composite column to describe how it should be saved and loaded::

  protected function serialize($data)
  {
    return json_encode($data);
  }

  protected function unserialize($data)
  {
    return json_decode($data);
  }

Now you can access your composite column by calling
``get<CompositeName>`` and modify it as you see fit. Saving the parent
model will automatically synchronize any changes to the column::

  $coordinates = $my_model->getCoordinates();

  $coordinates->latitude = 42.3550496;
  $coordinates->longitude = -71.0656267;

  $my_model->save();

If you don't wish to implement your own, a few common serializations are
included in the ``EllisLab\ExpressionEngine\Service\Model\Column\``
namespace:

+----------------------------------+---------------------------------+
| Class                            | Serialization                   |
+==================================+=================================+
| Composite (parent class)         | None, must implement your own   |
+----------------------------------+---------------------------------+
| JsonComposite                    | json_encode($data)              |
+----------------------------------+---------------------------------+
| SerializedComposite              | serialize($data)                |
+----------------------------------+---------------------------------+
| Base64EncodedSerializedComposite | base64_encode(serialize($data)) |
+----------------------------------+---------------------------------+


Multiple Tables
---------------


Model Methods
-------------

.. class:: EllisLab\\ExpressionEngine\\Service\\Model\\Model

.. method:: getId()

  Get the primary key value

  :returns: The primary key value
  :rtype: Int (or null if not yet saved)

.. method:: getName()

  Get the model alias that was registered with ExpressionEngine.

  :returns: The model alias
  :rtype: String

.. method:: getPrimaryKey()

  Get the primary key name

  :returns: The primary key name
  :rtype: String

.. method:: getProperty($name)

  Get a model property, calling any getters that were defined by
  the model.

  :param string $name: The name of the property
  :returns: The value of the property
  :rtype: Mixed

.. method:: setProperty($name, $value)

  Set a model property and track its dirty state. Calls any setters that
  were defined by the model.

  :param string $name: The name of the property
  :param mixed $value: The value to set the property to
  :returns: $this
  :rtype: Model

.. method:: getRawProperty($name)

  Get a model property, *without* calling any getters that were defined
  by the model.

  :param string $name: The name of the property
  :returns: The value of the property
  :rtype: Mixed

.. method:: setRawProperty($name, $value)

  Set a model property and track its dirty state. Does not call any
  setters that were defined by the model.

  :param string $name: The name of the property
  :param mixed $value: The value to set the property to
  :returns: $this
  :rtype: Model