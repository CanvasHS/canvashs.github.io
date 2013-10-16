---
layout: default
---
#Drawing

##Basic datatypes
Basic datatypes are used in the shapes, they serve as building block for shapes.

###Color
Colors are basic structures used in the API and can be used in the fill and stroke properties of shapes.

####Example
{% highlight json %}
{ "fill":  "rgba(255,0,0,1)"}
{% endhighlight %}

###Points
Points are lists of numbers that represent x and y pairs. A points list always contains an even number of items.

####Example
{% highlight json linenos %}
{ "points": [ 10, 0, 10, 10, 0, 10, 0, 0] }
{% endhighlight %}

###Identifiers
The `id` property used in shapes is exclusive and can only be used once.

##Shapes

###Line
A line consists of a list of points just like a polygon, but doesn't connect start with end. When scaling or rotating this will happen from the upper left x and y coordinates of the invisible rect incapsulating the polygon.

####Example
{% highlight json linenos %}
{
    "type": "line",
    "data": {
        "id": "line_nr_23",
        "points": [ 10, 0, 10, 10 ],
        "stroke": "rgba(255,255,255,1)",
        "strokeWidth": 2
    }
}
{% endhighlight %}

###Rect
A rect is a simple rectangle with a width and a height. When scaling or rotating this will happen from the upper left x and y coordinates.

In the example below scaling is also demonstrated.

####Example
{% highlight json linenos %}
{
    "type": "rect",
    "data": {
        "id": "rect_b",
        "x": 10,
        "y": 10,
        "width": 10,
        "height": 20,
        "stroke": "rgba(255,255,255,1)",
        "strokeWidth": 2,
        "fill": "rgba(255,0,0,1)",
        "scale": 1.5
    }
}
{% endhighlight %}

###Polygon
A polygon is a closed path where the beginning of the path is connected to the end. When scaling or rotating this will happen from the upper left x and y coordinates of the invisible rect incapsulating the polygon.

In the example below rotation is also demonstrated.

####Example
A simple triangle
{% highlight json linenos %}
{
    "type": "polygon",
    "data": {
        "id": "polygon_nr_23",
        "points": [73, 192, 73, 160, 340, 23, 500, 109, 499, 139, 342, 93],
        "stroke": "rgba(255,255,255,1)",
        "strokeWidth": 2,
        "fill": "rgba(255,0,0,1)",
        "rotationDeg": 90
    }
}
{% endhighlight %}


###Circle
A circle is centerpoint and a radius. The total size of a circle is therefore twice the radius. When scaling or rotating this will happen from center x and y of the circle.

####Example
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
    }
}
{% endhighlight %}


###Text
Text grows out of the horziontal center x and downward from the y coordinate. It rotates around this x and y, and scales around this x and y.

####Example
{% highlight json linenos %}
{
    "type": "text",
    "data": {
        "id": "text",
        "x": 20,
        "y": 20,
        "text": 'Simple Text',
        "fontSize": 30,
        "fontFamily": "Helvetica",
        fill: "rgba(255,0,0,1)"
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
        "scale": 5,
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
                "stroke": "rgba(255,255,255,1)",
                "strokeWidth": 2,
                "fill": "rgba(255,0,0,1)"
            }
        },
        {
            "type": "polygon",
            "data": {
                "id": "polygon_nr_23",
                "points": [73, 192, 73, 160, 340, 23, 500, 109, 499, 139, 342, 93],
                "stroke": "rgba(255,255,255,1)",
                "strokeWidth": 2,
                "fill": "rgba(255,0,0,1)",
                "rotationDeg": 90
            }
        }
    ]
}
{% endhighlight %}

##Sending the data

All the shapes and containers in the root canvas will be sent in the root objects property "objects". The root object also contains information about the entire canvas such as, if debug is enabled.

####Example
{% highlight json linenos %}
{
    "debug" : true,
    "objects" : [
        {
            "type": "polygon",
            "data": {
                "id": "polygon_nr_23",
                "points": [73, 192, 73, 160, 340, 23, 500, 109, 499, 139, 342, 93],
                "stroke": "rgba(255,255,255,1)",
                "strokeWidth": 2,
                "fill": "rgba(255,0,0,1)",
                "rotationDeg": 90
            }
        },
        {
            "type": "container",
            "data": {
                "id": "container_b",
                "x": 10,
                "y": 10,
                "width": 100,
                "height": 200,
                "scale": 5,
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
                        "stroke": "rgba(255,255,255,1)",
                        "strokeWidth": 2,
                        "fill": "rgba(255,0,0,1)"
                    }
                }
            ]
        }
    ]
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
    "listen" : ["mousedown","mouseclick","mouseup","mousedoubleclick","mousedrag","mouseenter" "mouseleave"]
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
        "id": "myAwesomeShape",
        "x": 150,
        "y": 150
    }
}
{% endhighlight %}

###MouseEnter
Triggered when the mouse enters a shape that is interested in that event. Note: only works on shapes that have eventdata and are interested in MouseEnter events.

####Example
{% highlight json linenos %}
{
    "event":"mouseenter",
    "data":{
        "id": "myAwesomeShape",
        "x": 150,
        "y": 150
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
        "id": "myAwesomeShape",
        "x": 150,
        "y": 150
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

##Generic events
###Scroll
Scroll events are triggered when a user scrolls in the canvas, has xdistance and ydistance values
####Example
{% highlight json linenos %}
{
    "event":"scroll",
    "data":{
        "xdelta": 20,
        "ydelta": 10
    }
}
{% endhighlight %}
