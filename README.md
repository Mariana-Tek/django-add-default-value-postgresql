Django Add Default Value for PostgreSQL
=======================================

Django Migration Operation that can be used to transfer a field's default value
to the database scheme.

Based on [django-add-default-value](https://github.com/3YOURMIND/django-add-default-value/) by [3YOURMIND](https://github.com/3YOURMIND). This variant drops support for other databases, specifically the Azure ODBC driver which does not support current versions of Django.



[![PyPi](https://img.shields.io/pypi/v/django-add-default-value-postgresql.svg?branch=master)](https://pypi.python.org/pypi/django-add-default-value-postgresql/)
[![License](https://img.shields.io/github/license/Mariana-Tek/django-add-default-value-postgresql.svg)](./LICENSE)

[![CI](https://github.com/Mariana-Tek/django-add-default-value-postgresql/workflows/Python%20package/badge.svg)](https://github.com/Mariana-Tek/django-add-default-value-postgresql/actions?query=workflow%3A%22Python+package%22)




Dependencies
------------

* Python 3.6, 3.7, or 3.8
* Django 2.2 or 3.0




Installation
------------
`pip install django-add-default-value-postgresql`

You can then use ``AddDefaultValue`` in your migration file to transfer the default
values to your database. Afterwards, it's just the usual ``./manage.py migrate``.

Usage
-----

Add this manually to an autogenerated Migration that adds a new field:

    AddDefaultValue(
        model_name='my_model',
        name='my_field',
        value='my_default'
    )


### Example

Given the following migration:

    operations = [
        migrations.AddField(
            field=models.CharField(default='my_default', max_length=255),
            model_name='my_model',
            name='my_field',
        ),
    ]

Modify the migration to add a default value:


    +from django_add_default_value import AddDefaultValue
    +
     operations = [
         migrations.AddField(
             field=models.CharField(default='my_default', max_length=255),
             model_name='my_model',
             name='my_field',
         ),
    +    AddDefaultValue(
    +        model_name='my_model',
    +        name='my_field',
    +        value='my_default'
    +    )
     ]

If you check ``python manage.py sqlmigrate [app name] [migration]``,
you will see that the default value now gets set.



## Testing

You can test against multiple versions of Django using `tox`. To test across Python versions, use pyenv to run `tox` under each version.



License
-------

``django-add-default-value-postgresql`` is released under the Apache 2.0 License.


