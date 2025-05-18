Publish
=======

HTTPS
    You can easily publish your map service via HTTPS.

    HTTPS is also required for `HTTP/2
    <https://developer.mozilla.org/en-US/docs/Glossary/HTTP_2>`_, which also
    speeds up the map display by allowing more requests at once.

CORS
    `Cross-Origin Resource Sharing
    <https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP>`_ restricts the
    websites that are allowed to embed your hosted resources.

    .. warning::
       Avoid wildcards ``*`` for ``Access-Control-Allow-Origin`` in productive
       use.

Map resources
    Even if your PMTiles archives or tile endpoints originate from your own
    infrastructure, other resources on a web map may originate from external
    providers. These include JavaScript libraries, CSS stylesheets and fonts.

Content security policy
    By defining a content security policy via an HTTP header or an HTML meta
    tag, you can ensure that all resources on the HTML page come from the same
    source, for example for MapLibre:

    .. code-block:: html

       <meta
         http-equiv="Content-Security-Policy"
         content="default-src 'self' 'nonce-n0nce' 'nonce-n0nce1'; worker-src blob: ; child-src blob: ; img-src data: blob: ;" />

Example
-------

Below you will find a complete example of a map application in which third-party
sources are avoided:

.. literalinclude:: berlin.html
   :language: html
   :linenos:
   :emphasize-lines: 7-10, 18, 26-27, 32

Lines 7–10
    :file:`maplibre-gl.js` and :file:`maplibre-gl.css` are JavaScript and CSS
    for the `MapLibre GL <https://maplibre.org/maplibre-gl-js/docs/>`_ rendering
    library.

    :file:`pmtiles.js` is a JavaScript file for decoding PMTiles archives in the
    browser.

    :file:`basemaps.js` is a JavaScript file for creating a MapLibre GL style
    for a base map tile set.

Line 18
    :file:`mapbox-gl-rtl-text.min. js`  a MapLibre plugin for supporting
    languages written from right to left.

Lines 26–27
    :file:`fonts/{fontstack}/{range}.pbf` are font glyphs for the display of
    labels, available under `protomaps/basemaps-assets
    <https://github.com/protomaps/basemaps-assets>`_.

    :file:`sprites/{version/{flavor_name}` are `Sprites
    <https://de.wikipedia.org/wiki/Sprite_(Computergrafik)>`_ for basemap icons,
    available under  `protomaps/basemaps-assets
    <https://github.com/protomaps/basemaps-assets>`__.
Line 32
   :file:`pmtiles://berlin.pmtiles` is the archive file with the map data.

Cloud storage
-------------

PMTiles works on any S3-compatible cloud storage platform that supports `HTTP
Range Requests
and `Cross-Origin Resource Sharing (CORS)
<https://developer.mozilla.org/en-US/docs/Web/HTTP/Guides/CORS>`_.

Upload
~~~~~~

The `pmtiles <https://github.com/protomaps/go-pmtiles>`_ command line tool has
the ``pmtiles upload`` command to transfer files to a cloud storage. `RClone
<https://rclone.org>`_ is another tool for managing large files on S3-compatible
storage:

:samp:`rclone copyto {FILENAME} {CONFIGURATION}:{BUCKET}/{FOLDER}/{FILENAME}.pmtiles --progress --s3-chunk-size=256M`

.. seealso::
   * `Recommended Platforms
     <https://docs.protomaps.com/pmtiles/cloud-storage#recommended-platforms>`_

Web-Server
----------

.. _caddy:

Caddy
~~~~~

`Caddy <https://caddyserver.com/>`_ is highly recommended for the provision of
PMTiles due to its built-in HTTPS support. Uses the ``file_server``
configuration to deploy :file:`*.pmtiles` from a static directory with the
following CORS configuration:

.. code-block:: javascript

   header {
     Access-Control-Allow-Methods GET,HEAD
     Access-Control-Expose-Headers ETag
     Access-Control-Allow-Headers Range,If-Match
     Access-Control-Allow-Origin https://www.cusy.io
   }

Alternatively, you can use the `pmtiles_proxy
<https://caddyserver.com/docs/modules/http.handlers.pmtiles_proxy>`_ for Caddy.

.. seealso::
   * `Protomaps Docs: Set up a Server: Caddy
     <https://docs.protomaps.com/deploy/server#caddy>`_

.. _nginx:

nginx
~~~~~

`nginx <https://nginx.org>`_ supports HTTP range requests, whereby the CORS
headers and support for CORS preflight requests should be set in the
configuration file:

.. code-block:: javascript

   if ($request_method = 'OPTIONS') {
     add_header 'Access-Control-Max-Age' 3600;
     add_header 'Content-Type' 'text/plain charset=UTF-8';
     add_header 'Access-Control-Allow-Origin' '*' always;
     add_header 'Access-Control-Allow-Headers' 'DNT,User-Agent,X-Requested-With,If-Modified-Since,Cache-Control,Content-Type,Range' always;
     add_header 'Content-Length' 0;
     return 204;
   }
