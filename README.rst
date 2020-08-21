dj-stripe
=========

.. image:: https://travis-ci.org/dj-stripe/dj-stripe.svg?branch=master
   :alt: Build Status
   :target: https://travis-ci.org/dj-stripe/dj-stripe

.. image:: https://readthedocs.org/projects/dj-stripe/badge/
   :alt: Documentation Status
   :target: https://dj-stripe.readthedocs.io/

Stripe Models for Django.


Introduction
------------

dj-stripe implements all of the Stripe models, for Django.
Set up your webhook and start receiving model updates.
You will then have a copy of all the Stripe models available in Django models, no API traffic required!

Features
--------

* Subscriptions
* Individual charges
* Stripe Sources
* Stripe v2 and v3 support
* Supports SCA regulations, Checkout Sessions, and Payment Intents
* Tested with Stripe API `2019-09-09` (see https://dj-stripe.readthedocs.io/en/latest/api_versions.html )

Requirements
------------

* Django >= 2.2
* Python >= 3.6
* Supports Stripe exclusively. See "Similar Libraries" below for other solutions.
* PostgreSQL engine (recommended): >= 9.4
* MySQL engine: MariaDB >= 10.2 or MySQL >= 5.7

Similar libraries
-----------------

* `dj-paypal <https://github.com/HearthSim/dj-paypal>`_ (`PayPal <https://www.paypal.com/>`_)
* `dj-paddle <https://github.com/dj-paddle/dj-paddle>`_ (`Paddle <https://paddle.com/>`_)

Quickstart
----------

Install dj-stripe:

.. code-block:: bash

    pip install dj-stripe

Add ``djstripe`` to your ``INSTALLED_APPS``:

.. code-block:: python

    INSTALLED_APPS =(
        ...
        "djstripe",
        ...
    )

Add to urls.py:

.. code-block:: python

    path("stripe/", include("djstripe.urls", namespace="djstripe")),

Tell Stripe about the webhook (Stripe webhook docs can be found `here <https://stripe.com/docs/webhooks>`_) using the full URL of your endpoint from the urls.py step above (e.g. ``https://example.com/stripe/webhook``).

Add your Stripe keys and set the operating mode:

.. code-block:: python

    STRIPE_LIVE_PUBLIC_KEY = os.environ.get("STRIPE_LIVE_PUBLIC_KEY", "<your publishable key>")
    STRIPE_LIVE_SECRET_KEY = os.environ.get("STRIPE_LIVE_SECRET_KEY", "<your secret key>")
    STRIPE_TEST_PUBLIC_KEY = os.environ.get("STRIPE_TEST_PUBLIC_KEY", "<your publishable key>")
    STRIPE_TEST_SECRET_KEY = os.environ.get("STRIPE_TEST_SECRET_KEY", "<your secret key>")
    STRIPE_LIVE_MODE = False  # Change to True in production
    DJSTRIPE_WEBHOOK_SECRET = "whsec_xxx"  # Get it from the section in the Stripe dashboard where you added the webhook endpoint

Add some payment plans via the Stripe.com dashboard.

Run the commands::

    python manage.py migrate

    python manage.py djstripe_init_customers

    python manage.py djstripe_sync_plans_from_stripe

See https://dj-stripe.readthedocs.io/en/latest/stripe_elements_js.html for notes about
usage of the Stripe Elements frontend JS library.

Running the Tests
------------------

Assuming the tests are run against PostgreSQL::

    createdb djstripe
    pip install tox
    tox

Follows Best Practices
======================

.. image:: https://twoscoops.smugmug.com/Two-Scoops-Press-Media-Kit/i-C8s5jkn/0/O/favicon-152.png
   :name: Two Scoops Logo
   :align: center
   :alt: Two Scoops of Django
   :target: https://www.twoscoopspress.org/products/two-scoops-of-django-1-11

This project follows best practices as espoused in `Two Scoops of Django: Best Practices for Django 1.11`_.

.. _`Two Scoops of Django: Best Practices for Django 1.11`: https://twoscoopspress.org/products/two-scoops-of-django-1-11
