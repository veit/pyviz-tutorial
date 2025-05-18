Convert
=======

.. _tippecanoe:

Tippecanoe
----------

`Tippecanoe <https://github.com/felt/tippecanoe>`__ creates vector tiles from
`GeoJSON <https://geojson.org>`_ and `FlatGeobuf
<https://github.com/flatgeobuf/flatgeobuf>`_ files, among others. As of version
2.17, Tippecanoe also supports PMTiles with the option :samp:`-o
{FILENAME}.pmtiles`. To merge several PMTiles files into a single file, you can
use `tile-join
<https://github.com/felt/tippecanoe?tab=readme-ov-file#tile-join>`_, which
comes with Tippecanoe.

Installation
~~~~~~~~~~~~

.. tab:: Debian/Ubuntu

   .. code-block:: console

      $ sudo apt-get install gcc g++ git make libsqlite3-dev zlib1g-dev
      $ git clone https://github.com/felt/tippecanoe.git
      $ cd tippecanoe
      $ make -j
      $ make install

.. tab:: macOS

   .. code-block:: console

      $ brew install tippecanoe

pmtiles CLI
-----------

The command line tool `pmtiles <https://docs.protomaps.com/pmtiles/cli>`_
converts `MBTiles
<https://www.python4data.science/de/latest/data-processing/geodata.html#mbtiles>`_
into PMTiles with the command :samp:`pmtiles convert {INPUT}.mbtiles
{OUTPUT}.pmtiles`.

Installation
~~~~~~~~~~~~

.. code-block:: console

   $ uv add pmtiles

rio-pmtiles
-----------

`rio-pmtiles <https://pypi.org/project/rio-pmtiles/>`_ is a plugin for `Rasterio
<https://rasterio.readthedocs.io/en/stable/>`_ that can be used to convert small
and medium-sized raster data (~1GB).

Installation
~~~~~~~~~~~~

.. code-block:: console

   $ uv add rio-pmtiles

GDAL
----

`GDAL <https://gdal.org/en/stable/>`_ supports PMTiles from version 3.8.0. With
``ogr2ogr``, a wide range of formats can be converted into PMTiles, for example
`shapefiles
<https://enterprise.arcgis.com/de/portal/latest/use/shapefiles.htm>`_ and
:doc:`python4datascience:data-processing/postgresql/postgis/index` tables:

.. code-block:: console

   $ ogr2ogr -dsco MINZOOM=10 -dsco MAXZOOM=15 -f "PMTiles" FILENAME.pmtiles MY_SHAPES.shp
   $ ogr2ogr -dsco MINZOOM=0 -dsco MAXZOOM=15 -f "PMTiles" FILENAME.pmtiles "PG:host=MY_HOST port=MY_PORT dbname=MY_DATABASE user=MY_USERNAME password=MY_PASSWORD schemas=MY_SCHEMA"

.. tip::
   ``ogr2ogr`` for creating vector PMTiles is only recommended for smaller data
   sets: :ref:`tippecanoe` generates overview tiles much more efficiently.

.. seealso::
   * `GDAL documentation
     <https://gdal.org/en/stable/drivers/vector/pmtiles.html>`_

Installation
~~~~~~~~~~~~

.. tab:: Debian/Ubuntu

   .. code-block:: console

      $ sudo apt install libgdal20

.. tab:: macOS

   The Apache Arrow library of the current homebrew distribution is defective.
   To build GDAL successfully, configure CMake so that the Arrow package is not
   found. Also, Boost is no longer bundled with libkml, so libkml should be
   disabled when building under macOS:

   .. code-block:: console

      $ cmake -DCMAKE_DISABLE_FIND_PACKAGE_Arrow=ON ..
      $ cmake -DGDAL_USE_LIBKML=OFF ..
      $ brew install gdal

protomaps/basemaps
------------------

The Protomaps basemap is based on `OpenStreetMap
<https://www.openstreetmap.org/>`_- and `Natural Earth
<https://www.naturalearthdata.com>`_ data. It does not include all of OSM’s
data and tags; instead, it is designed to provide a balance between tile size
and completeness to be used as a general context map.

The organisation of layers and tags is derived from the open source project
`Tilezen <https://tilezen.readthedocs.io/en/latest/layers/>`_. The amount of
content and selection of data included at certain zoom levels is reflected in
the reference implementations of Tilezen styles such as `Bubble Wrap
<https://tangrams.github.io/bubble-wrap/>`_.

.. seealso::
   * `Basemap Layers
     <https://docs.protomaps.com/basemaps/layers#basemap-layers>`_

The `basemaps <https://github.com/protomaps/basemaps>`_ repository in tiles
contains a `Planetiler <https://github.com/onthegomap/planetiler>`_ profile for
generating planetary-level PMTiles from OpenStreetMap. The layers in this
tileset are documented in `Basemap Layers
<https://docs.protomaps.com/basemaps/layers>`__ and daily builds can be
downloaded for free from `maps.protomaps.com/builds
<https://maps.protomaps.com/builds/>`_.

The pipeline for generating this daily basemap is `open source
<https://github.com/protomaps/basemaps/tree/main/tiles>`_ and based on the
Planetiler Java Tiling Engine. It can be run for your local city or country in a
matter of minutes.

The advantages of a self-generated basemap include

Up-to-date basemaps
    Create tiles from specific OpenStreetMap snapshots, for example from the
    latest data from `SliceOSM <https://slice.openstreetmap.us/>`_.

Extracts
    Create customised, focused area maps. Extracting an area from the daily
    planetary map contains additional data in tiles with a low zoom factor, as
    shown in the image below:

    .. figure:: basemap.png
       :alt: Base map of Berlin-Reinickendorf

       Base map of Berlin-Reinickendorf

    #. You need a Java runtime environment ≥21 and Maven:

       .. tab:: Debian/Ubuntu

          .. code-block:: console

             $ apt-install openjdk-21-jdk maven

       .. tab:: macOS

          .. code-block:: console

             $ brew install openjdk maven

    #. An OpenStreetMap section that covers your area of interest, for example
       an on-demand download from `SliceOSM <https://slice.openstreetmap.us/>`_
       or a pre-generated download from `Geofabrik Downloads
       <https://download.geofabrik.de>`_.
    #. The district boundaries of Berlin as a GeoJSON file, downloaded from
       `ODIS <https://daten.odis-berlin.de>`_ or from `Who’s On First Spelunker
       <https://spelunker.whosonfirst.org>`_.
    #. Check out the basemaps project and build the JAR file:

       .. code-block:: console

          $ git clone https://github.com/protomaps/basemaps
          $ cd basemaps/tiles
          $ mvn clean package

    #. Create your tiles:

       .. code-block:: console

          $ java -jar  target/protomaps-basemap-HEAD-with-deps.jar --clip='~/reinickendorf.geojson' --area=reinickendorf --download

       Resources such as pre-processed OSM water and land polygons, `Natural
       Earth <https://www.naturalearthdata.com>`_ and data sets for language
       support and ranking are also downloaded.

    #. Finally, you can display the new map by dragging the
       :file:`{REGION}.pntiles` file into the `Basemaps Viewer
       <https://maps.protomaps.com/>`_.

    You can build a customised map of the entire planet with for example:

    .. code-block:: console

       $ java -Xmx20g -jar target/protomaps-basemap-HEAD-with-deps.jar --nodemap-type=array --osm_path=~/planet-latest.osm.pbf --output=/data/planet.pmtiles --bounds=planet --tmpdir=/var/scratch

    ``-Xmx20g``
        Provide 20 GB of heap space to the Java runtime environment.
    ``--nodemap-type=array``
        A build option that is best suited for creating planet tiles.
    ``--tmpdir=/var/scratch``
        Be sure to have at least 512 GB of scratch space.

    .. tip::
       For a calculation in less than three hours, we recommend as many CPU
       cores as possible on an Intel Core i9, AMD Ryzen 9 or similar, 64 GB RAM
       and at least 1 TB NVMe SSD storage.

Custom tags
    You can use the ``extra_name_tags`` option to add additional tags from
    OpenStreetMap to the output file.

Tilemaker
---------

`Tilemaker <https://github.com/systemed/tilemaker>`_ is a programme for creating
basemap tiles from OpenStreetMap, but not ones that match the `Basemap Layers
<https://docs.protomaps.com/basemaps/layers>`__ of Protomaps. In addition, the
PMTiles archives generated by Tilemaker are not clustered, which can lead to
large, slow retrievals when decoding in a web browser. For production use, you
should therefore optimise the archive with `pmtiles cluster
<https://docs.protomaps.com/pmtiles/cli#cluster>`_.
