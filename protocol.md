---
layout: default
---
#Basic datatypes
Basic datatypes are used in the shapes, they serve as building block for shapes.

##Color
Colors are basic structures used in the API and can be used in the fill and stroke properties of shapes. Colors have red/green/blue in the range 0 to 255, and alpha in the range 0.0 to 1.0

####Example
{% highlight json %}
{"r": 255, "g": 255, "b": 255, "a": 1.0}
{% endhighlight %}

##Points
Points are lists of numbers that represent x and y pairs. A points list always contains an even number of items.

####Example
{% highlight json linenos %}
{ "points": [ 10, 0, 10, 10, 0, 10, 0, 0] }
{% endhighlight %}

##Common properties
All shapes have keys for the following properties in their data:

* `scaleX (float)` scales a figure in the x direction
* `scaleY (float)` scales a figure in the y direction
* `rotationDeg (int)` rotates a figure around a given corner for some degrees
* `offset ([int])` specifies the location on the shape to rotate and scale around
* `fill (Color)` fill color of the shape
* `stroke (Color)` stroke color of the shape
* `strokeWidth` width of the shape (in px)

#Shapes

##Line
A line consists of a list of points that will be connected. When scaling or rotating this will happen from the upper left x and y coordinates of the invisible rect incapsulating the line.

####Specific keys

* `points ([int])` List of points that define the line (always divisible by 2)

####Bare Minimum
*White (default) line from (10,0) to (10,10)*
{% highlight json linenos %}
{
    "type": "line",
    "data": {
        "points": [ 10, 0, 10, 10 ]
    }
}
{% endhighlight %}

####Realworld Example
*Red line from (10, 0) to (10, 10)*
{% highlight json linenos %}
{
    "type": "line",
    "data": {
        "points": [ 10, 0, 10, 10 ],
        "stroke": {"r": 255, "g": 0, "b": 0, "a": 1.0},
        "strokeWidth": 2
    }
}
{% endhighlight %}

##Polygon
A polygon is a closed path where the beginning of the path is connected to the end (unlike a Line). When scaling or rotating this will happen from the upper left x and y coordinates of the invisible rect incapsulating the polygon.

####Specific keys
* `points ([int])` List of points that define the line (always divisible by 2)

####Bare Minimum
*White (default) polygon from (73, 192) to (73, 160) to (340, 23) to (500, 109) to (499, 139) to (342, 93) to (73, 192)*
{% highlight json linenos %}
{
    "type": "polygon",
    "data": {
        "points": [73, 192, 73, 160, 340, 23, 500, 109, 499, 139, 342, 93],
    }
}
{% endhighlight %}

####Realworld Example
*Green polygon (semitransparant) with Yellow stroke (2px) from (73, 192) to (73, 160) to (340, 23) to (500, 109) to (499, 139) to (342, 93) to (73, 192)*
{% highlight json linenos %}
{
    "type": "polygon",
    "data": {
        "points": [73, 192, 73, 160, 340, 23, 500, 109, 499, 139, 342, 93],
        "stroke": {"r": 255, "g": 255, "b": 0, "a": 1.0},
        "strokeWidth": 2,
        "fill": {"r":0, "g":255, "b":0, "a":0.75}
    }
}
{% endhighlight %}

##Rect
A rect is a simple rectangle with a width and a height. When scaling or rotating this will happen from the upper left x and y coordinates.

####Specific keys
* `x (int)` the x location of the upper corner of the rect
* `y (int)` the y location of the upper corner of the rect
* `width (int)` the width of the rect
* `height (int)` the height of the rect

####Bare Minimum
*White (default) square from (10, 10) to (20, 30)*
{% highlight json linenos %}
{
    "type": "rect",
    "data": {
        "x": 10,
        "y": 10,
        "width": 10,
        "height": 20,
    }
}
{% endhighlight %}

####Realworld Example
*Green square with blue stroke from (10, 10) to (20, 30)*
{% highlight json linenos %}
{
    "type": "rect",
    "data": {
        "x": 10,
        "y": 10,
        "width": 10,
        "height": 20,
        "stroke": {"r": 255, "g": 0, "b": 0, "a": 1.0},
        "strokeWidth": 2,
        "fill": {"r":0, "g":255, "b":0, "a":0.75}
    }
}
{% endhighlight %}

##Circle
A circle is centerpoint and a radius. The total size of a circle is therefore twice the radius. When scaling or rotating this will happen from center x and y of the circle.

####Specific keys
* `x (int)` the x location of the center of the circle
* `y (int)` the y location of the center of the circle
* `radius (int)` the radius of the circle

####Bare Minimum
*White (default) circle with center (20, 20) and radius 5*
{% highlight json linenos %}
{
    "type": "circle",
    "data": {
        "x": 20,
        "y": 20,
        "radius": 5
    }
}
{% endhighlight %}

####Realworld Example
*Black circle with purple stroke (2px) with center (20, 20) and radius 5*
{% highlight json linenos %}
{
    "type": "circle",
    "data": {
        "x": 20,
        "y": 20,
        "radius": 5,
        "stroke": {"r": 255, "g": 0, "b": 255, "a": 1.0},
        "strokeWidth": 2,
        "fill": {"r":0, "g":0, "b":0, "a":1.0}
    }
}
{% endhighlight %}


##Text
Text has some text to display and some properties defining the font/size/etc.

####Specific keys
* `x (int)` the x location of the text (rendering depends on the alignment)
* `y (int)` the y location of the text (rendering depends on the alignment)
* `fontFamily (string)` The font to use for this text, no guarantees are made about availability
* `fontSize (int)` The size of the font used (in px)
* `align (string)` The location of the alignmentpoint (Center, Left, Right)
* `bold (boolean)` Whether the text should be rendered bold
* `italic (boolean)` Whether the text should be rendered italic
* `underline (boolean)` Whether the text should be underlined
* `text (string)` The text to render

####Bare Minimum
*`Hello Protocol!` centered around (20, 20) with default font and size (chosen by the client)*
{% highlight json linenos %}
{
    "type": "text",
    "data": {
        "x": 20,
        "y": 20,
        "text": "Hello Protocol!",
        "align": "center"
    }
}
{% endhighlight %}

####Realworld Example
*`Hello Rotation and Scaling!` in Helvetica (14px) centered around (20, 20) with a rotation of 20 degrees around (20, 20) and a xScale of 2.0*
{% highlight json linenos %}
{
    "type": "text",
    "data": {
        "x": 20,
        "y": 20,
        "text": "Hello Rotation and Scaling!",
        "align": "center",
        "fontFamily": "Helvetica",
        "fontSize": 14,
        "rotationDeg": 20,
        "xScale": 2.0
    }
}
{% endhighlight %}

##Containers
A container is here to provide the scaling, rotation and event binding to multiple objects. The container creates its own coordinate system therefor everything inside is relative to the containers dimentions, location and rotation.

####Example
{% highlight json linenos %}
{
    "type": "container",
    "data": {
        "id": "container_b",
        "x": 10,
        "y": 10,
        "width": 100,
        "height": 200,
        "scaleX": 5.0,
        "scaleY": 10.0,
        "rotationDeg": 180
    },
    "children" : [
        {
            "type": "circle",
            "data": {
                "id": "circle_nr_1",
                "x": 20,
                "y": 20,
                "radius": 5,
                "stroke": {"r": 255, "g": 0, "b": 0, "a": 1.0},
                "strokeWidth": 2,
                "fill": {"r":0, "g":255, "b":0, "a":0.75}
            }
        },
        {
            "type": "polygon",
            "data": {
                "id": "polygon_nr_23",
                "points": [73, 192, 73, 160, 340, 23, 500, 109, 499, 139, 342, 93],
                "stroke": {"r": 255, "g": 0, "b": 0, "a": 1.0},
                "strokeWidth": 2,
                "fill": {"r":0, "g":255, "b":0, "a":0.75},
                "rotationDeg": 90
            }
        }
    ]
}
{% endhighlight %}

##The Canvas

The container that represents the root of the canvas will be sent as the root object. By Default the canvas will resize to the dimentions of the root container. If you want to go FullWindow or FullScreen you should use actions. After going FullWindow or FullScreen you can adjust the positioning of shapes when the `ResizeWindow` event is called. This happens automaticly if you go FullWindow of FullScreen.

####Example
{% highlight json linenos %}
{
    "shape": {
        …
    },
    "actions": [{
        …
    }]
}
{% endhighlight %}

#Events
##EventData
All shapes drawn above are not interactive, clicking/dragging/etc. won't trigger events. Eventdata can be added to a shape with the "event" key, when the user presses the mousebutton and the cursor intersects a shape with eventdata a message is sent to the server informing that a specific shape is pressed.

Eventdata consists of an id and a set booleans on which events shapes will react. Currently supported are:
* Mouse down (User presses and holds left mouse button)
* Mouse click (User clicks left mouse button)
* Mouse up (User lets go of left mouse button)
* Mouse double click (User clicks left mouse button twice)
* Mouse drag (User presses leftmousebutton and drags around)
* Mouse enter (Mousecursor enters shape)
* Mouse out (Mousecursor leaves shape)
* Scroll (User scrolls on shape)

####Eventdata example
{% highlight json linenos %}
{
    "type": "circle",
    "data": {
        "id": "circle_nr_1",
        "x": 20,
        "y": 20,
        "radius": 5,
        "stroke": "rgba(255,255,255,1)",
        "strokeWidth": 2,
        "fill": "rgba(255,0,0,1)"
    },
    "listen" : ["mousedown","mouseclick","mouseup","mousedoubleclick","mousedrag","mouseover" "mouseout"]
}
{% endhighlight %}

When an event is triggered, javascript will search for a object that is intersected and is interested in that event, if a object was found, the object key is populated with the ID of that object. The raw event is always sent to the server, even if no object was interested.

##MouseEvents
###MouseDown
Triggered when a user presses and holds the left mousebutton, its location (a point) and an id of a pressed object is transmitted. If no id can be transmitted the mousedown event will not be sent. The `x` and `y` coordinates are absolute to the intire canvas and not relative to the container of the object referenced by the `id`.

####Example
{% highlight json linenos %}
{
    "event":"mousedown",
    "data":{
        "id": "myAwesomeShape",
        "x": 150,
        "y": 150
    }
}
{% endhighlight %}

###MouseClick
Triggered when the mouse is pressed and released ("clicked"), same data as mousedown.

####Example
{% highlight json linenos %}
{
    "event":"mouseclick",
    "data":{
        "id": "myAwesomeShape",
        "x": 150,
        "y": 150
    }
}
{% endhighlight %}

###MouseUp
Triggered when the mouse is released after it was down for some time, same data as mousedown.

####Example
{% highlight json linenos %}
{
    "event":"mouseclick",
    "data":{
        "id": "myAwesomeShape",
        "x": 150,
        "y": 150
    }
}
{% endhighlight %}

###MouseDoubleClick
Triggered when the mouse is clicked twice, same data as mousedown.

####Example
{% highlight json linenos %}
{
    "event":"mousedoubleclick",
    "data":{
        "id": "myAwesomeShape",
        "x": 150,
        "y": 150
    }
}
{% endhighlight %}

###MouseDrag
Triggered when a shape is pressed and dragged from one point to another, contains start and end locations.

####Example
{% highlight json linenos %}
{
    "event":"mousedrag",
    "data":{
        "id1": "myAwesomeShape",
        "x1": 150,
        "y1": 150,
        "x2": 250,
        "y2": 250
    }
}

{% endhighlight %}

###MouseOver
Triggered when the mouse enters a shape that is interested in that event. Note: only works on shapes that have eventdata and are interested in MouseOver events.

####Example
{% highlight json linenos %}
{
    "event":"mouseover",
    "data":{
        "id": "myAwesomeShape",
        "x": 150,
        "y": 150
    }
}
{% endhighlight %}

###MouseOut
Same as MouseOver, but when the mouse leaves a shape

####Example
{% highlight json linenos %}
{
    "event":"mouseout",
    "data":{
        "id": "myAwesomeShape",
        "x": 150,
        "y": 150
    }
}
{% endhighlight %}

###Scroll
Scroll events are triggered when a user scrolls an element, id, xdelta and ydelta's are sent to the client
####Example
{% highlight json linenos %}
{
    "event":"scroll",
    "data":{
        "id": "myAwesomeShape",
        "xdelta": 20,
        "ydelta": 10
    }
}
{% endhighlight %}

##Key Events
Key events are not connected to objects, a key is pressed with some modifiers (Ctrl/Alt/Shift/Super). The super key is equal to the windows key.

###KeyDown
Triggered when a key is pressed and hold down.

####Example
{% highlight json linenos %}
{
    "event":"keydown",
    "data":{
        "key": "a",
        "control": true,
        "alt": false,
        "shift": false,
        "super": false
    }
}
{% endhighlight %}

###KeyUp
Triggered when a key is released.

####Example
{% highlight json linenos %}
{
    "event":"keyup",
    "data":{
        "key": "c",
        "control": true,
        "alt": false,
        "shift": false,
        "super": false
    }
}
{% endhighlight %}

## Other Events

###Upload
Event triggered when a file is uploaded after drop-in or selection in the file dialog. To open the fill dialog send a `PresentFileOpenDialog` action.
####Example
{% highlight json linenos %}
{
    "event":"upload",
    "data":{
        "file": "data base 64 string"
    }
}
{% endhighlight %}

###ResizeWindow
Event triggered when the window resizes. This event is also triggerd on first time launch.
####Example
{% highlight json linenos %}
{
    "event":"resizewindow",
    "data":{
        "width": 800,
        "height": 600
    }
}
{% endhighlight %}

###Prompt
Simple event to return entered values in a prompt.

####Example
{% highlight json linenos %}
{
    "event":"prompt",
    "data":{
        "value": "John Doe"
    }
}
{% endhighlight %}

#Action
Actions are messages that trigger certain javascript functions from the server. So it is like events but from server to client, from haskell to javascript.
####Example
{% highlight json linenos %}
{
    "shape": {
        …
    },
    "actions": [{
        …
    }]
}
{% endhighlight %}

###WindowDisplayType
Type is an enumeration where 0 is `FizedSize` 1 is `FullWindow` and 2 is `FullScreen`. Width and height are required with `FixedSize` and are ignored with the other types.

####Example
{% highlight json linenos %}
{
    "action":"windowdisplaytype",
    "data":{
        "type": 0,
        "width": 800,
        "height": 600
    }
}
{
    "action":"windowdisplaytype",
    "data":{
        "type": 1
    }
}
{% endhighlight %}

###Debugger
Simple action to enable or disable the canvas debugger.

####Example
{% highlight json linenos %}
{
    "action":"debugger",
    "data":{
        "enabled": true
    }
}
{% endhighlight %}

###Prompt
Simple action to prompt the user for string input. Placeholder is optional. After entering the action will return a prompt event. Prompting is blocking so while entering the interface will halt.

####Example
{% highlight json linenos %}
{
    "action":"prompt",
    "data":{
        "message": "Please enter your name…",
        "placeholder": "John Doe"
    }
}
{% endhighlight %}

##File Actions

###RequestUpload
Simple action to present a file select dialog box. The `multiple` parameter indicates that multiple files can be uploaded.

####Example
{% highlight json linenos %}
{
    "action":"requestupload",
    "data": {
        "multiple": true
    }
}
{% endhighlight %}

###Download
Action to sava a file, this will trigger the browser to download.

####Example
{% highlight json linenos %}
{
    "action":"download",
    "data":{
        "file": "data base 64 string"
    }
}
{% endhighlight %}

###AcceptFileDragNDrop
Simple action to enable drag'n'drop file uploads. The `multiple` parameter indicates that multiple files can be uploaded.

####Example
{% highlight json linenos %}
{
    "action":"acceptfiledragndrop",
    "data":{
        "enabled": true,
        "multiple": true
    }
}
{% endhighlight %}


