---
layout: default
---
#Drawing
Drawings produce picture types, all objects used for drawing 'derive' picture.

##Basic datatypes
Basic datatypes are used in the shapes, they serve as building block for shapes.

###Point
Points are basic structures used in the API, a point is a x and y component stored as a JSON object.

####Example
{% highlight json %}
{ "x": 10, "y": 20 }
{% endhighlight %}

###Path
Paths are lists of points and are connected form 1 to 2 to 3 etc.

####Example
{% highlight json linenos %}
{
    "path": [
        { "x":0, "y":0 },
        { "x":100, "y":0 },
        { "x":100, "y":50}
    ]
}
{% endhighlight %}

##Shapes
###Polygon
A polygon is a closed path where the beginning of the path is connected to the end.

####Example
A simple triangle
{% highlight json linenos %}
{
    "shape": "polygon",
    "data": {
        "path": [
            { "x": 10, "y": 0 },
            { "x": 100, "y": 10 },
            { "x": 50, "y": 70 }
        ]
    }
}
{% endhighlight %}

###Line
A line consists of a path just like a polygon, but doesn't connect start with end.

####Example
{% highlight json linenos %}
{
    "shape": "line",
    "data": {
        "path": [
            { "x": 10, "y": 10 },
            { "x": 20, "y": 10 },
            { "x": 10, "y": 20 }
        ]
    }
}
{% endhighlight %}

###Circle
A circle is centerpoint and a radius. The total size of a circle is therefore twice the radius.

####Example
{% highlight json linenos %}
{
    "shape": "circle",
    "data": {
        "center": { "x":10,"y":20 },
        "radius": 100
    }
}
{% endhighlight %}

###Arc
An arc is a segment of a circle, its drawn the same way as a circle but also has a start and endpoint (in degrees counterclockwise). An arc from 90 to 270 would span from the west to the east.

####Example
{% highlight json linenos %}
{
    "shape": "arc",
    "data": {
        "center": { "x":10,"y":20 },
        "radius": 100,
        "start": 90,
        "end": 270,
    }
}
{% endhighlight %}
###Picture
A picture is a shape consisting of shapes, it consists of a list of other picture types. For example, if you want to draw Mickey Mouse you would first draw its head (a circle), and then its ears (two circles).

####Example
{% highlight json linenos %}
{
    "shape": "picture",
    "data": [
        {
            "shape": "circle", 
            "data": { "center": {"x": 100, "y": 100}, "radius": 100 }
        },
        {
            "shape": "circle", 
            "data": { "center": {"x": 50, "y": 50}, "radius": 50 }
        },
        {
            "shape": "circle", 
            "data": { "center": {"x": 150, "y": 50}, "radius": 50 }
        }
    ]
}
{% endhighlight %}

#Modifiers
Modifiers are applied to shapes. A red square with a brown stroke is a square modified to be red and modified to have a brown stroke.

###Translate
A Translation is a picture that is moved by dx an dy. Note that the "move" object is no point as it consist of x and y deltas!

####Example
{% highlight json linenos %}
{
    "modifier": "translate",
    "data":
        {
            "move":  { "dx": 10, "dy":10 },
            "picture": {
                "shape": "circle", 
                "data": { "center": {"x": 50, "y": 50}, "radius": 50 }
            }
        }
}
{% endhighlight %}

###Rotate
Rotate a picture by some amount of degrees (counterclockwise).

####Example
{% highlight json linenos %}
{
    "modifier": "rotate",
    "data":
        {
            "rotate": 90,
            "picture": {
                "shape": "polygon", 
                "data": {
                    "path": [
                        { "x": 10, "y": 0 },
                        { "x": 100, "y": 10 },
                        { "x": 50, "y": 70 }
                    ] 
                }
            }
        }
}
{% endhighlight %}

###Scale
Scale a picture by some x-scale and y-scale.

####Example
{% highlight json linenos %}
{
    "modifier": "scale",
    "data":
        {
            "xscale": 0.5,
            "yscale": 0.5,
            "picture": {
                "shape": "polygon", 
                "data": {
                    "path": [
                        { "x": 10, "y": 0 },
                        { "x": 100, "y": 10 },
                        { "x": 50, "y": 70 }
                    ] 
                }
            }
        }
}
{% endhighlight %}

###Color
Fills a specified picture with a color (r,g,b,a).

####Example
{% highlight json linenos %}
{
    "modifier": "color",
    "data":
        {
            "R": 255,
            "G": 0,
            "B": 255,
            "A": 255,
            "picture": {
                "shape": "polygon", 
                "data": {
                    "path": [
                        { "x": 10, "y": 0 },
                        { "x": 100, "y": 10 },
                        { "x": 50, "y": 70 }
                    ] 
                }
            }
        }
}
{% endhighlight %}

###Stroke
Sets an outline for a picture type. Has fields for stroketype and width, currently supports solid as stroketype.

####Example
{% highlight json linenos %}
{
    "modifier": "color",
    "data":
        {
            "stroke": "solid",
            "width": 1,
            "picture": {
                "shape": "polygon", 
                "data": {
                    "path": [
                        { "x": 10, "y": 0 },
                        { "x": 100, "y": 10 },
                        { "x": 50, "y": 70 }
                    ] 
                }
            }
        }
}
{% endhighlight %}

#Events
##EventData
All shapes drawn above are not interactive, clicking/dragging/etc. won't trigger events. Eventdata can be added to a shape with the "event" key, when the user presses the mousebutton and the cursor intersects a shape with eventdata a message is sent to the server informing that a specific shape is pressed.

Eventdata consists of an id and a set booleans on which events shapes will react. Currently supported are:
* MouseDown (User presses and holds left mouse button)
* MouseClick (User clicks left mouse button)
* MouseUp (User lets go of left mouse button)
* MouseDoubleClick (User clicks left mouse button twice)
* MouseDrag (User presses leftmousebutton and drags around)
* MouseEnter (Mousecursor enters shape)
* MouseLeave (Mousecursor leaves shape)

####Eventdata example
{% highlight json linenos %}
{
    "shape": "line",
    "event": {
        "id": "someLineIDrew",
        "mousedown": false,
        "mouseclick": true,
        "mouseup": false,
        "mousedoubleclick": true,
        "mousedrag": false,
        "mouseenter": false,
        "mouseleave": false
    }, 
    "data": {
        "path": [
            { "x": 10, "y": 10 },
            { "x": 20, "y": 10 },
            { "x": 10, "y": 20 }
        ]
    }
}
{% endhighlight %}

When an event is triggered, javascript will search for a object that is intersected and is interested in that event, if a object was found, the object key is populated with the ID of that object. The raw event is always sent to the server, even if no object was interested.

##MouseEvents
###MouseDown
Triggered when a user presses and holds the left mousebutton, its location (a point) and an id of a pressed object is transmitted (if any).

####Example
{% highlight json linenos %}
{
    "event":"mousedown",
    "data":{
        "id": null,
        "location": {"x": 150, "y": 150}
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
        "location": {"x": 876, "y": 245}
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
        "id": null,
        "location": {"x": 234, "y": 543}
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
        "id": "thisShapeIsDoubleClickable",
        "location": {"x": 234, "y": 543}
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
        "id": "thisShapeIsDoubleClickable",
        "from": {"x": 234, "y": 543}
        "to": {"x": 200, "y": 512}
    }
}
{% endhighlight %}

###MouseEnter
Triggered when the mouse enters a shape that is interested in that event. Note: only works on shapes that have eventdata and are interested in MouseEnter events.

####Example
{% highlight json linenos %}
{
    "event":"mouseenter"
    "data":{
        "id": "thisShapeIsInterestedInMouseEnters",
        "location": {"x": 234, "y": 543}
    }
}
{% endhighlight %}

###MouseLeave
Same as MouseEnter, but when the mouse leaves a shape

####Example
{% highlight json linenos %}
{
    "event":"mouseleave",
    "data":{
        "id": "thisShapeIsInterestedInMouseLeaves",
        "location": {"x": 234, "y": 543}
    }
}
{% endhighlight %}

##Key Events
Key events are not connected to objects, a key is pressed with some modifiers (Ctrl/Alt/Shift/AltGr/Meta)

###KeyDown
Triggered when a key is pressed and hold down.

####Example
{% highlight json linenos %}
{
    "event":"keydown",
    "data":{
        "keycode": "a",
        "modifiers":{
            "control": true,
            "alt": false,
            "shift": false,
            "altgr": false,
            "meta": false
        }
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
        "keycode": "c",
        "modifiers":{
            "control": true,
            "alt": false,
            "shift": false,
            "altgr": false,
            "meta": false
        }
    }
}
{% endhighlight %}

##Generic events
###Scroll
Scroll events are triggered when a user scrolls in the canvas, has xdistance and ydistance values
####Example
{% highlight json linenos %}
{
    "event":"scroll",
    "data":{
        "xdistance": 20,
        "ydistance": 10
    }
}
{% endhighlight %}
