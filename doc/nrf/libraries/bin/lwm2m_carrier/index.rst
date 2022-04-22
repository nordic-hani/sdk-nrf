.. _liblwm2m_carrier_readme:

LwM2M carrier
#############

.. contents::
   :local:
   :depth: 2

.. important::

   It is *mandatory* to include the LwM2M carrier library in any AT&T, T-Mobile, or Verizon certified products.

Several mobile network carriers specify their own (LwM2M) device management.
The nrf91 device is expected to connect to these device management servers, regardles of what else the user application may be doing.
This autonomy is facilitated by the LwM2M carrier library.

.. figure:: /libraries/bin/lwm2m_carrier/images/lwm2m_carrier_overview.svg
    :alt: LwM2M carrier library working together with the user application

    LwM2M carrier library working together with the use application

For the applicable carriers (`Mobile network operator certifications`_), this library is mandatory to include in your application to be able to certify your end product.

The :ref:`lwm2m_carrier` sample demonstrates how to run this library in an application.
The LwM2M carrier library is also used in the :ref:`asset_tracker_v2` application.

.. note::

  If you are looking to use LwM2M for other purposes, please see :ref:`lwm2m_interface`.

.. toctree::
    :maxdepth: 1
    :caption: Subpages:

    certification
    app_integration
    requirements
    msc
    API_documentation
    CHANGELOG
