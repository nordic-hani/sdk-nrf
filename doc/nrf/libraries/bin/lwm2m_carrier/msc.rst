.. _lwm2m_msc:

Message sequence charts
#######################

The following message sequence chart shows the initialization of the LwM2M carrier library:

.. figure:: /libraries/bin/lwm2m_carrier/images/lwm2m_carrier_msc_init.svg
    :alt: LwM2M carrier library initialization

    LwM2M carrier library initialization



The following message sequence chart shows the ``lwm2m_carrier_thread_run`` thread up until we register with the device management server:

.. figure:: /libraries/bin/lwm2m_carrier/images/lwm2m_carrier_msc_bootstrap.svg
    :alt: LwM2M library bootstrap and register procedure

    LwM2M library bootstrap and register procedure

The following message sequence chart shows FOTA updates:

.. figure:: /libraries/bin/lwm2m_carrier/images/lwm2m_carrier_msc_fota_success.svg
    :alt: LwM2M server initiated FOTA

    LwM2M server initiated FOTA

The following message sequence chart shows a successful CA certificate initialization:

.. msc::
    hscale = "1.1";
    Modem,Application,"LwM2M carrier Library";
    |||;
    ---                                    [label="LwM2M carrier library is initializing"];
    |||;
    Application<<="LwM2M carrier Library"  [label="LWM2M_CARRIER_EVENT_CERTS_INIT"];
    ...;
    Application rbox Application           [label="Write CA certificates to modem security tags"];
    Modem<<=Application                    [label="modem_key_mgmt_write(...)"];
    ...;
    Modem->Application                     [label="Success"];
    Application rbox Application           [label="Provide LwM2M carrier library the security tags for CA certificates"];
    Application rbox Application           [label="LwM2M carrier event data set to ca_cert_tags_t"];
    Application->"LwM2M carrier Library"   [label="Success"];
    ...;

The following message sequence chart shows that the CA certificate initialization fails if the application fails to provision the keys to the modem:

.. msc::
    hscale = "1.1";
    Modem,Application,"LwM2M carrier Library";
    |||;
    ---                                         [label="LwM2M carrier library is initializing"];
    |||;
    Application<<="LwM2M carrier Library"       [label="LWM2M_CARRIER_EVENT_CERTS_INIT"];
    ...;
    Application rbox Application                [label="Write CA certificates to modem security tags"];
    Modem<<=Application                         [label="modem_key_mgmt_write(...)"];
    ...;
    Modem->Application                          [label="Failure"];
    Application->"LwM2M carrier Library"        [label="Failure"];
    "LwM2M carrier Library" rbox "LwM2M carrier Library" [label="LwM2M carrier library fails to initialize"];
    Application<-"LwM2M carrier Library"        [label="Failure"];
    ...;

The following message sequence chart shows that FOTA fails at run time if an invalid CA certificate is provided during the initialization:

.. figure:: /libraries/bin/lwm2m_carrier/images/lwm2m_carrier_msc_fota_fail_cert.svg
    :alt: FOTA CA certificate failure

    FOTA CA certificate failure
