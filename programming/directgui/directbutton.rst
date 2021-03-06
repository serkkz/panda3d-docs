.. _directbutton:

DirectButton
============

DirectButton is a DirectGui object that will respond to the mouse and can
execute an arbitrary function when the user clicks on the object. This is
actually implemented by taking advantage of the "state" system supported by
every DirectGui object.

Each DirectGui object has a predefined number of available "states", and a
current state. This concept of "state" is completely unrelated to Panda's
:ref:`FSM <finite-state-machines>` object. For a DirectGui object, the current
state is simply as an integer number, which is used to select one of a list of
different NodePaths that represent the way the DirectGui object appears in
each state. Each DirectGui object can therefore have a completely different
appearance in each of its states.

Most types of DirectGui objects do not use this state system, and only have
one state, which is state 0. The DirectButton is presently the only predefined
object that has more than one state defined by default. In fact, DirectButton
defines four states, numbered 0 through 3, which are called ready, press,
rollover, and disabled, in that order. Furthermore, the DirectButton
automatically manages its current state into one of these states, according to
the user's interaction with the mouse.

With a DirectButton, then, you have the flexibility to define four completely
different NodePaths, each of which represents the way the button appears in a
different state. Usually, you want to define these such that the ready state is
the way the button looks most of the time, the press state looks like the button
has been depressed, the rollover state is lit up, and the disabled state is
grayed out. In fact, the DirectButton interfaces will set these NodePaths up for
you, if you use the simple forms of the constructor (for instance, if you
specify just a single text string to the ``text`` parameter).

Sometimes you want to have explicit control over the various states, for
instance to display a different text string in each state. To do this, you can
pass a 4-tuple to the text parameter (or to many of the other parameters, such
as relief or geom), where each element of the tuple is the parameter value for
the corresponding state, like this:

.. code-block:: python

   button = DirectButton(text=('caption', 'click!', 'rollover', 'disabled'))

The above example would create a DirectButton whose label reads "caption" when it is
not being touched, but it will change to a completely different label as the
mouse rolls over it and clicks it.

You can create buttons as geometry in the 3D editor and apply them to four different states, like this:

.. code-block:: python

   caption = loader.loadModel('button_caption')
   click = loader.loadModel('button_click')
   rollover = loader.loadModel('button_rollover')
   disabled = loader.loadModel('button_disabled')

   button = DirectButton(geom=(caption, click, rollover, disabled))

You can also access one of the state-specific NodePaths after the button has
been created with the interface:

.. code-block:: python

   button.stateNodePath[stateNumber]

The following are the DirectGui keywords that are specific to a DirectButton.
(These are in addition to the generic DirectGui keywords described on the
:ref:`previous page <directgui>`.)

============== ==================================================== ==========================
Keyword        Definition                                           Value
============== ==================================================== ==========================
command        Command the button performs when clicked             Function
extraArgs      Extra arguments to the function specified in command [Extra Arguments]
commandButtons Which mouse button must be clicked to do the command LMB, MMB, or RMB
rolloverSound  The sound made when the cursor rolls over the button AudioSound instance
clickSound     The sound made when the cursor clicks on the button  AudioSound instance
pressEffect    Whether or not the button sinks in when clicked      <0 or 1>
state          Whether or not the button is disabled                DGG.NORMAL or DGG.DISABLED
============== ==================================================== ==========================

Like any other :ref:`DirectGui <directgui>` widget, you can change any of the
properties by treating the element as a dictionary:

.. code-block:: python

   button['state'] = DGG.DISABLED
   
Example
-------

.. code-block:: python

   from direct.showbase.ShowBase import ShowBase
   from direct.gui.DirectGui import DirectButton, OnscreenText, DGG
   from panda3d.core import TextNode


   class MyApp(ShowBase):

       def __init__(self):
           ShowBase.__init__(self)

           # Add some text
           self.message = OnscreenText(
               text='This is my demo',
               pos=(0.95, -0.95),
               scale=0.07,
               fg=(1, 0.5, 0.5, 1),
               align=TextNode.ACenter
           )

           # Add button
           self.button = DirectButton(
               text=('caption', 'click!', 'rollover', 'disabled'),
               scale=0.07,
               command=self.my_function
           )

       # Function to set text message and disabled button
       def my_function(self):
           self.message.setText('Button clicked')
           self.button['state'] = DGG.DISABLED


   app = MyApp()
   app.run()

When you are positioning your button, keep in mind that the button's vertical
center is located at the base of the text. For example, if you had a button with
the word "Apple", the vertical center would be aligned with the base of the
letter "A".
