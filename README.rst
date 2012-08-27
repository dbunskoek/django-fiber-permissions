Fiber Permissions Example
=========================

This example project shows what could be a per-object permission implementation for Fiber.


Getting started
---------------

Install the requirements:

::

    pip install -r requirements.txt

Load the fixtures:

::

    python manage.py syncdb --migrate  # don't generate an admin user
    python manage.py loaddata fixtures/example_initial_data.json
    python manage.py loaddata fixtures/auth_and_guardian_data.json

The initial data comes with two users::

    admin/admin
    example-user/test

Login as example-user. You'll now have limited rights to edit / move / delete pages and content items.


Assigning permissions
---------------------

You can assign object-level permissions to a user as follows::

    from django.contrib.auth.models import User
    u = User.objects.get(username='example-user')
    from guardian.shortcuts import assign
    from fiber.models import Page
    p = Page.objects.get(title='A')
    assign('change_page', u, p)

Via the admin give staff permission to 'example-user' and give him all permissions associated to Fiber.
