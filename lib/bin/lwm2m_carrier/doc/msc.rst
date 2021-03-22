.. _lwm2m_msc:

Message sequence charts
#######################

The below message sequence chart shows the initialization of the LwM2M carrier library:


.. msc::
    hscale = "1.1";
    Application,"LwM2M carrier Library";
    Application=>"LwM2M carrier Library"       [label="lwm2m_carrier_init()"];
    Application<<="LwM2M carrier Library"      [label="LWM2M_CARRIER_EVENT_BSDLIB_INIT"];
    Application<<="LwM2M carrier Library"      [label="LWM2M_CARRIER_EVENT_CONNECTING"];
    Application<<="LwM2M carrier Library"      [label="LWM2M_CARRIER_EVENT_CONNECTED"];
    Application<<"LwM2M carrier Library"       [label="Success"];
    Application=>"LwM2M carrier Library"       [label="lwm2m_carrier_run()"];
    |||;
    "LwM2M carrier Library" :> "LwM2M carrier Library" [label="(no return)"];
    ...;



The following message sequence chart shows the bootstrap process:

.. msc::
    hscale = "1.1";
    Application,"LwM2M carrier Library";
    |||;
    ---                                       [label="Device is not bootstrapped yet"];
    |||;
    Application<<="LwM2M carrier Library"      [label="LWM2M_CARRIER_EVENT_DISCONNECTING"];
    Application<<="LwM2M carrier Library"      [label="LWM2M_CARRIER_EVENT_DISCONNECTED"];
    "LwM2M carrier Library" rbox "LwM2M carrier Library" [label="Write keys to modem"];
    Application<<="LwM2M carrier Library"      [label="LWM2M_CARRIER_EVENT_CONNECTING"];
    Application<<="LwM2M carrier Library"      [label="LWM2M_CARRIER_EVENT_CONNECTED"];
    Application<<="LwM2M carrier Library"      [label="LWM2M_CARRIER_EVENT_BOOTSTRAPPED"];
    Application<<="LwM2M carrier Library"      [label="LWM2M_CARRIER_EVENT_LTE_READY"];
    Application<<="LwM2M carrier Library"      [label="LWM2M_CARRIER_EVENT_REGISTERED"];


The following message sequence chart shows FOTA updates:

.. msc::
    hscale = "1.1";
    Application,"LwM2M carrier Library";
    |||;
    ---                                       [label="Carrier initiates modem update"];
    |||;
    Application<<="LwM2M carrier Library"      [label="LWM2M_CARRIER_EVENT_FOTA_START"];
    ...;
    Application<<="LwM2M carrier Library"      [label="LWM2M_CARRIER_EVENT_DISCONNECTING"];
    Application<<="LwM2M carrier Library"      [label="LWM2M_CARRIER_EVENT_DISCONNECTED"];
    Application<<="LwM2M carrier Library"      [label="LWM2M_CARRIER_EVENT_CONNECTING"];
    Application<<="LwM2M carrier Library"      [label="LWM2M_CARRIER_EVENT_CONNECTED"];
    Application<<="LwM2M carrier Library"      [label="LWM2M_CARRIER_EVENT_LTE_READY"];
    Application<<="LwM2M carrier Library"      [label="LWM2M_CARRIER_EVENT_REGISTERED"];
    ...;


The following message sequence chart shows successfull CA certificate initialization:

.. msc::
    hscale = "1.1";
    Modem,Application,"LwM2M carrier Library";
    |||;
    ---                                        [label="LwM2M carrier library is initializing"];
    |||;
    Application<<="LwM2M carrier Library"      [label="LWM2M_CARRIER_EVENT_CERTS_INIT"];
    ...;
    Application rbox Application               [label="Write CA certificates to modem security tags"];
	Modem<<=Application                        [label="modem_key_mgmt_write(...)"];
    ...;
	Modem->Application                         [label="success"];
	Application rbox Application               [label="Inform LwM2M carrier library of security tags for CA certificates"];
    Application rbox Application               [label="lwm2m_carrier_event_t data set to ca_cert_tags_t"];
	Modem->Application                         [label="success"];
    ...;

The following message sequence chart shows that the app fails CA certificate initialization:

.. msc::
    hscale = "1.1";
    Modem,Application,"LwM2M carrier Library";
    |||;
    ---                                        [label="LwM2M carrier library is initializing"];
    |||;
    Application<<="LwM2M carrier Library"      [label="LWM2M_CARRIER_EVENT_CERTS_INIT"];
    ...;
    Application rbox Application               [label="Write CA certificates to modem security tags"];
	Modem<<=Application                        [label="modem_key_mgmt_write(...)"];
    ...;
	Modem->Application                         [label="error"];
	Application->"LwM2M carrier Library"       [label="error"];
    ...;

The following message sequence chart shows that the app fails CA certificate initialization:

.. msc::
    hscale = "1.1";
    Application,"LwM2M carrier Library";
    |||;
    ---                                        [label="LwM2M carrier library is initializing"];
    |||;
    Application<<="LwM2M carrier Library"      [label="LWM2M_CARRIER_EVENT_FOTA_START"];
    ...;
    "LwM2M carrier Library" rbox "LwM2M carrier Library" [label="Write CA certificates to modem security tags"];
    Application<<="LwM2M carrier Library"      [label="LWM2M_CARRIER_ERROR_FOTA_CONN (NRF_ECONNREFUSED)"];
    ...;