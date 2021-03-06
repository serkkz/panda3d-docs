.. _directframe:

DirectFrame
===========

A frame is a container object for multiple DirectGUI objects. This allows for
the control over several objects that are reparented to the same frame. When
DirectGUI objects are parented to a frame, they will be positioned relative to
the frame.

DirectFrame has no unique keywords, since it is mostly used to arrange other
objects.

Like any other DirectGUI object, the DirectFrame is called as such:

.. code-block:: python

    DirectFrame(keyword=value, keyword=value, ...)

For a basic frame, the most used keywords are
``frameSize``,
``frameColor`` and
``pos``. For a full list of
keywords available for this object you can click, see the :ref:`directgui`
page.

As we established above, the most common keywords are:

========== ==================================== =======================
Keyword    Definition                           Value
========== ==================================== =======================
frameSize  Sets the size of the frame           (Left,Right,Bottom,Top)
frameColor sets the color of the object’s frame (R,G,B,A)
pos        sets the position of the object      (X,Y,Z)
========== ==================================== =======================

Example
-------

.. code-block:: python

   from direct.showbase.ShowBase import ShowBase
   from direct.gui.DirectGui import DirectFrame


   class MyApp(ShowBase):

       def __init__(self):
           ShowBase.__init__(self)

           # Add frame
           frame = DirectFrame(
               frameSize=(-1, 1, -1, 1),
               frameColor=(0, 0, 0, 1),
               pos=(1, -1, -1)
           )


   app = MyApp()
   app.run()

Keep in mind, if your screen is non-square you will see the background color
you have set (or the default one if you have not set any) where there is no
frame on screen.

By default, as with any DirectGUI object, DirectFrame is reparented to
aspect2d so the will stay fixed on-screen even when your camera moves. Newly
created objects usually are drawn on top of already existing ones, unless you
change it manually.

You can also position the frame using the ``set_pos()`` method and use other 
methods to access properties, such as scaling.

Example
-------

.. code-block:: python

   from direct.showbase.ShowBase import ShowBase
   from direct.gui.DirectGui import DirectFrame


   class MyApp(ShowBase):

       def __init__(self):
           ShowBase.__init__(self)

           # Add frame
           frame = DirectFrame(
               frameSize=(-1, 1, -1, 1)
           )

           frame.set_pos(1, -1, -1)
           frame.set_scale(1.5)
           frame.set_color(0, 0, 0, 1)


   app = MyApp()
   app.run()


Usually one would decide on one of the ways to read and write values for
DirectGUI objects a third way to access and change properties is the
following:

Example
-------

.. code-block:: python

   from direct.showbase.ShowBase import ShowBase
   from direct.gui.DirectGui import DirectFrame


   class MyApp(ShowBase):

       def __init__(self):
           ShowBase.__init__(self)

           # Add frame
           frame = DirectFrame(
               frameSize=(-1, 1, -1, 1)
           )

           frame.set_pos(1, -1, -1)
           frame.set_scale(1.5)
           frame.set_color(0, 0, 0, 1)


   app = MyApp()
   app.run()
