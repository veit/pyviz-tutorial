Protomaps
=========

`Protomaps <https://protomaps.com>`_ is an open source project for the creation
and use of vector maps. It was developed as a lightweight alternative to
conventional map providers and offers a number of advantages.

Open Source
    Fully open source code for maximum transparency and customisability.
Self-hosting
    Maps can be hosted on your own servers without dependence on external
    services.
Privacy
    The maps can be published securely and in a privacy-friendly manner, without
    using tracking mechanisms like many commercial map services.
Compact format
    The map data is stored in the efficient `PMTiles
    <https://docs.protomaps.com/pmtiles/>`_ format.
Offline use
    The maps can be used completely offline so that they can be used reliably
    even in crisis areas.

Areas of application
--------------------

Protomaps is particularly suitable for:

- web developers who want to integrate maps into their applications
- projects with limited bandwidth or in regions with limited internet connection
- privacy-sensitive applications that should not send data to third parties
- map applications that should function independently of commercial providers

Technology stack
----------------

Protomaps can be used with various JavaScript libraries:

- `Maplibre GL JS <https://maplibre.org/maplibre-gl-js/docs/>`_
- `Leaflet <https://leafletjs.com>`_
- `OpenLayers <https://openlayers.org>`_

Data sources
------------

The map data comes mainly from `OpenStreetMap
<https://www.openstreetmap.org/>`_, but can be supplemented with your own data.

.. toctree::
    :hidden:
    :titlesonly:
    :maxdepth: 0

    extract
    convert
    publish
    cli
