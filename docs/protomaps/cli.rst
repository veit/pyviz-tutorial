pmtiles CLI reference
=====================

``pmtiles show``
----------------

:samp:`$ pmtiles show {FILE}.pmtiles`
    displays the header information and metadata of a local archive.
:samp:`$ pmtiles show https://maps.cusy.io/map.pmtiles`
    displays the header information and metadata of a remote HTTPS archive.
:samp:`$ pmtiles show {FILE}.pmtiles --bucket=s3://{BUCKET}`
    displays the header information and metadata of an archive that is located
    on an S3-compatible bucket.
:samp:`$ pmtiles show {FILE}.pmtiles --header-json`
    outputs a JSON representation of the header.
:samp:`$ pmtiles show {FILE}.pmtiles --metadata`
    outputs the JSON metadata.

.. note::
   URLs with characters such as ``?`` and ``&`` should be escaped with a
   backslash ``\``.

``pmtiles tile``
----------------

:samp:`$ pmtiles tile {FILE}.pmtiles 0 0 0`
    outputs the content of a single tile.

``pmtiles verify``
------------------

:samp:`$ pmtiles verify {FILE}.pmtiles`
    checks whether an archive is correctly organised and contains correct
    header information.

``pmtiles extract``
-------------------

:samp:`$ pmtiles extract`
    creates a smaller archive from a larger one, whereby the source archive must
    be clustered:

    :samp:`$ pmtiles extract {IN}.pmtiles {OUT}.pmtiles --bbox=MIN_LON,MIN_LAT,MAX_LON,MAX_LAT`
        You can determine the bounding box with ``MIN_LON``, ``MIN_LAT``,
        ``AX_LON`` and ``MAX_LAT`` with `bboxfinder.com
        <https://bboxfinder.com/>`_, for example.

    :samp:`$ pmtiles extract {IN}.pmtiles {OUT}.pmtiles --region={REGION}.geojson`
        A GeoJSON ``Polygon``, ``Multipolygon``, ``Feature`` or a
        ``FeatureCollection`` object can be specified with ``--region``.

    :samp:`$ pmtiles extract https://{EXAMPLE.COM}/{IN}.pmtiles {OUT}.pmtiles --maxzoom={MAXZOOM} --download-threads=4`
        ``--maxzoom`` extracts only a subset of the zoom levels.

        ``--download-threads`` specifies the number of parallel requests to
        speed up the downloads.

    :samp:`$ pmtiles extract {IN}.pmtiles {OUT}.pmtiles --maxzoom=MAXZOOM --bucket=s3://{BUCKET}`

    Further options are:

    ``--minzoom``
        extracts only part of the pyramid, but this may require many more
        requests than the default ``--minzoom=0``. As this removes the overview
        zoom levels, it should only be used in certain situations.

    ``--overfetch``
        downloads additional data to bundle small requests: ``0.05`` corresponds
        to 5 %.

``pmtiles serve``
-----------------

:samp:`$ pmtiles serve`
    is an easy way to serve PMTiles together with `pmtiles.js
    <https://www.npmjs.com/package/pmtiles>`_ on the web:

    :samp:`$ pmtiles serve {PATH}`
        serves a :samp:`{TILESET}.pmtiles` file from the :samp:`{PATH}`
        directory at the
        :samp:`http://localhost:8080/{TILESET}/{Z}/{X}/{Y}.mvt|png|jpg|webp|avif`,
        where the suffix must match the tile type in the archive.

    :samp:`$ pmtiles serve . --public-url=localhost`
        allows the output of `TileJSON
        <https://github.com/mapbox/tilejson-spec/tree/master/3.0.0>`_ under the
        URL :samp:`http://localhost:8080/{TILESET}.json`.

``pmtiles convert``
-------------------

:samp:`$ pmtiles convert`
    converts an  `MBTiles <https://docs.mapbox.com/help/glossary/mbtiles/>`_
    archive into PMTiles:

    :samp:`$ pmtiles convert {IN}.mbtiles {OUT}.pmtiles`

    :samp:`--no-deduplication`
        Tile contents should usually be de-duplicated. Use this only if you know
        that the input contains only unique tiles and you want to speed up the
        conversion.
    :samp:`--tmpdir`
        allows you to specify the temporary directory.

``pmtiles cluster``
-------------------

:samp:`pmtiles cluster {IN}.pmtiles`
    clusters an existing archive, optimising the size and layout. Archives
    created with `tippecanoe <https://github.com/felt/tippecanoe>`_, `planetiler
    <https://github.com/onthegomap/planetiler>`_ and pmtiles CLI are already
    clustered.

    :samp:`--no-deduplication`
        Tile contents should usually be de-duplicated. Use this only if you know
        that the input contains only unique tiles and you want to speed up the
        conversion.

``pmtiles upload``
------------------

:samp:`pmtiles upload {IN}.pmtiles {REMOTE}.pmtiles --bucket=s3://{BUCKET}`
    uploads an archive to the cloud storage.

``pmtiles edit``
----------------

:samp:`pmtiles edit NAME.pmtiles --header-json={HEADER}.json --metadata={METADATA}.json`
    changes parts of the archive header, or replaces the JSON metadata of the
    archive. If you only edit the header, the file will be changed in place;
    however, writing the JSON metadata requires writing a new copy of the
    archive, which then replaces :samp:`NAME.pmtiles`.

    .. hint::
       You can write the existing header information and metadata to the
       :samp:`{HEADER}.json` and :samp:`{METADATA}.json` files with:

       :samp:`pmtiles show {NAME}.pmtiles --header-json > {HEADER}.json`

       or

       :samp:`pmtiles show {NAME}.pmtiles --metadata > {METADATA}.json`

    .. hint::
       The fields ``tile_type``, ``tile_compresssion``, ``minzoom``,
       ``maxzoom``, ``bounds`` and ``centre`` of the header can be edited;
       however, other fields cannot be edited.

``pmtiles version``
-------------------

:samp:`pmtiles version`
    outputs the version from pmtiles.
