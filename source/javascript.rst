Javascript
##########

Usefull Libraries
=================

D3.js is a JavaScript library for manipulating documents based on data. http://d3js.org/

Closures
========

    Function that returns a function

Object Orientation
==================

    * Object Orientation in Javascript is somewhat broken, thats why
    functional programming is really hip

    * We rather use factory-functions than classes to create objects

    * http://stackoverflow.com/questions/1809914/oo-javascript-constructor-pattern-neo-classical-vs-prototypal

Methods for creating an object in javascript
============================================

.. code-block:: js

    // Object literal
    var place = {
        name: "Vienna",
        position: [48.2, 16.4]
    }

    // Method 2: 'Factory' function
    var element = document.createElement('div');

    // Method 3: new Keyword with constructor function, only in there to look like Java, dont use it
    var now = new Date();
    console.log(now.getFullYear());

    var map = new google.maps.Map(element); // have to use it for google maps api


Execution Order & Hoisting
==========================

.. code-block:: js

    var place = {name: 'Vienna'};

    function sayPlaces() {
        // var place; gets 'hoisted' here from below, or:
        // namespace is created for the whole function and does not have an order
        console.log(place.name); // outputs undefined since var place is not assigned a value
        var place = {name: "Dresden"} // if i uncomment this, the function will output vienna
        console.log(place.name);
    }

    sayPlaces();

Hoisting fun with functions
---------------------------

.. code-block:: js
    sayHello();
    // 'Hello' works, whole function is hoisted from Bewllow

    function sayHello() {
        console.log("Hello");
    }

    sayHello2();
    // does not work!

    var sayHello = function() {
        console.log("Hello");
    }

D3.js
=====


Load data, select element by css id
-----------------------------------

.. code-block:: js

    // load data, call function when loaded
    d3.csv('places-AT-cleaned.csv', function(data) {
        // .on captures the event (in this case click)
        d3.select('#populationButton').on('click', function(){  // ''#'' css selector for id, '.' selector for class
            console.log("population")
        })
        )
    });

.. code-block:: js

    selection.enter() // what to do with NEW objects
    selection.transition() // what to do with ALL objects
    pathGenerator // geogrpahical geometry to screen geopgraphy


Path generator
--------------



.. code-block:: js

    function setup_projection(projection, geometry) {

        projection.translate([0,0]).scale(1);

        //  generates array with [[left, top], [right, bottom]]
        var bounds = d3.geo.path().projection(projection).bounds(geometry);


        // calculate scaling factor
        // width and height are hard-coded dimensions of the viewing window
        // (fe 400px and 800px)
        var scale = 0.95 / Math.max(
            (bounds[1][0] - bounds[0][0]) / width, // geom.width / viewport.width
            (bounds[1][1] - bounds[0][1]) / height
        );

        var translate = [
            (width / 2 - (bounds[0][0] + bounds[1][0]) / 2 * scale),
            (height / 2 - (bounds[0][1] + bounds[1][1]) / 2 * scale)
        ];

        projection
            .scale(scale)
            .translate(translate);

    }
