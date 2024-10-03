Integrating bokeh plots into Flask
==================================

As an example, we embed bokeh plots in the `Flask
<https://flask.palletsprojects.com/en/2.3.x/>`_ framework.

#. Creating the virtual environment:

   .. code-block:: sh

    $ mkdir embed
    $ cd !$
    $ pipenv install flask bokeh pandas

#. Embedding bokeh plots in Flask:

   #. A method for a bokeh document is first created in the
      :file:`flask_embed.py` file:

      .. code-block:: python

         from bokeh.layouts import column
         from bokeh.models import ColumnDataSource, Slider
         from bokeh.plotting import figure
         from bokeh.sampledata.sea_surface_temperature import sea_surface_temperature
         from bokeh.server.server import Server
         from bokeh.themes import Theme


         def modify_doc(doc):
             df = sea_surface_temperature.copy()
             source = ColumnDataSource(data=df)

             plot = figure(
                 x_axis_type="datetime",
                 y_range=(0, 25),
                 y_axis_label="Temperature (Celsius)",
                 title="Sea Surface Temperature at 43.18, -70.43",
             )
             plot.line("time", "temperature", source=source)

             def callback(attr, old, new):
                 if new == 0:
                     data = df
                 else:
                     data = df.rolling("{0}D".format(new)).mean()
                 source.data = ColumnDataSource(data=data).data

             slider = Slider(
                 start=0, end=30, value=0, step=1, title="Smoothing by N Days"
             )
             slider.on_change("value", callback)

             doc.add_root(column(slider, plot))

             doc.theme = Theme(filename="theme.yaml")

   #. With ``bokeh.sampledata.sea_surface_temperature``, samples are used that
      are not included in the Bokeh package due to their size. However, after
      installing Bokeh, these can be downloaded with the following command:

       .. code-block:: sh

          $ pipenv run bokeh sampledata

   #. We then create the following :file:`theme.yaml` file for the design of the
      ``Figure`` and ``Grid``:

      .. code-block:: yaml

         attrs:
             Figure:
                 background_fill_color: "gainsboro"
                 outline_line_color: white
                 toolbar_location: above
                 height: 500
                 width: 800
             Grid:
                 grid_line_dash: [6, 4]
                 grid_line_color: white

   #. Now we add a route from the Bokeh app to the Flask server configuration
      object in :file:`flask_embed.py`:

      .. code-block:: python

         from bokeh.embed import server_document
         from flask import render_template


         ...


         @app.route("/", methods=["GET"])
         def bkapp_page():
             script = server_document("http://localhost:5006/bkapp")
             return render_template("embed.html", script=script, framework="Flask")

   #. ``script`` and ``framework`` are then integrated into a `Jinja2
      <https://jinja.palletsprojects.com/en/3.1.x/>`_ template
      :file:`templates/embed.html`, which is to display the plot:

      .. code-block:: html

         <!doctype html>

         <html lang="en">
         <head>
           <meta charset="utf-8">
           <title>Embedding a Bokeh Server in {{framework}}</title>
         </head>

         <body>
           <div>
             This Bokeh app below served by a Bokeh server that has been embedded
             in the web app framework {{framework}}. For more information see the section
             <a  target="_blank" href="https://bokeh.pydata.org/en/latest/docs/user_guide/server.html#embedding-bokeh-server-as-a-library">Embedding Bokeh Server as a Library</a>
             in the User’s Guide.
           </div>
           {{script|safe}}
         </body>
         </html>

   #. A bokeh worker is now defined in :file:`flask_embed.py`:

      .. code-block:: python

         from flask import Flask
         from tornado.ioloop import IOLoop


         ...


         def bk_worker():
             server = Server(
                 {"/bkapp": modify_doc},
                 io_loop=IOLoop(),
                 allow_websocket_origin=["localhost:8000"],
             )
             server.start()
             server.io_loop.start()


   #. Finally, the Flask app is defined:

      .. code-block:: python

         app = Flask(__name__)
         ...
         if __name__ == "__main__":
             print(
                 "Opening single process Flask app with embedded Bokeh application on http://localhost:8000/"
             )
             print()
             print(
                 "Multiple connections may block the Bokeh app in this configuration!"
             )
             print('See "flask_gunicorn_embed.py" for one way to run multi-process')
             app.run(port=8000)

#. If the Bokeh service cannot yet communicate with Flask via WebSocket, this
   should be explicitly permitted with:

   .. code-block:: sh

    $ export BOKEH_ALLOW_WS_ORIGIN=127.0.0.1:5000

#. Finally, Flask can be started with:

   .. code-block:: sh

    $ export FLASK_APP=flask_embed.py
    $ pipenv run flask run

   or, if several bokeh workers are to be started:

   .. code-block:: sh

    $ export FLASK_APP=flask_gunicorn_embed.py
    $ pipenv run flask run

.. seealso::

   * `User Guide/Embedding Plots and Apps/App Sessions
     <https://docs.bokeh.org/en/latest/docs/user_guide/output/embed.html#app-sessions>`_
   * `GnuCash-Expenses-Vis
     <https://github.com/maciek3000/GnuCash-Expenses-Vis>`_
