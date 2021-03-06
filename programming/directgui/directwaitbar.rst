.. _directwaitbar:

DirectWaitBar
=============

DirectWaitBars are similar to status bars; use them to indicate a slow process
gradually completing (e.g. a loading screen). It has various options for both
the background bar and the loading bar that fills up as the process progresses.
You can call finish() to automatically fill up the bar, or use the following to
set the value (it ranges from 0 to 100 by default):

.. code-block:: python

   wait_bar['value'] = number

============== ============================================================================================= ================================
Keyword        Definition                                                                                    Value
============== ============================================================================================= ================================
value          Initial value of the loading bar (from 0 to 100)                                              Number
range          The maximum value of the loading bar                                                          Number
barColor       The color of the loading bar                                                                  (R,G,B,A)
barTexture     An image to be display on the loading bar                                                     image filename or Texture object
barRelief      The relief appearance of the loading bar                                                      SUNKEN or RAISED
barBorderWidth If barRelief is SUNKEN, RAISED, GROOVE, or RIDGE, changes the size of the loading bar's bevel (Width, Height)
relief         The relief appearance of the background bar                                                   SUNKEN or RAISED
============== ============================================================================================= ================================

Example
-------

.. code-block:: python

   from direct.showbase.ShowBase import ShowBase
   from direct.gui.DirectGui import DirectButton, OnscreenText, DirectWaitBar
   from panda3d.core import TextNode


   class MyApp(ShowBase):

       def __init__(self):
           ShowBase.__init__(self)

           # Add some text
           self.textObject = OnscreenText(
               text='This is my demo',
               pos=(0.95, -0.95),
               scale=0.07,
               fg=(1, 0.5, 0.5, 1),
               align=TextNode.ACenter,
               mayChange=1
           )

           # Add wait bar
           self.wait_bar = DirectWaitBar(
               text='',
               value=50,
               pos=(0, 0.4, 0.4)
           )

           # Add 2 buttons
           button_1 = DirectButton(
               text='+1',
               scale=0.07,
               pos=(-0.3, 0.6, 0),
               command=self.incBar,
               extraArgs=[1]
           )

           button_2 = DirectButton(
               text='-10',
               scale=0.07,
               pos=(0.3, 0.6, 0),
               command=self.incBar,
               extraArgs=[-10]
           )

       # Callback function to set text
       def incBar(self, arg):
           self.wait_bar['value'] += arg
           self.textObject.setText(
               'Progress is: {0} %'.format(self.wait_bar['value']))


   app = MyApp()
   app.run()
