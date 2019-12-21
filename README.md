# lapland-js-spec - LaplandJS backend framework specification

Lapland is YAFJSF (yet another fraken JavaScript framework) I'm curious to play in development of.))
Here's the [repo with the main module](https://github.com/UniBreakfast/lapland) itself.
I struggled for some time trying to find the names for my modules I would actually like. Until I decided to see them as actors working on the common task - in a sense like Santa's elfs. So the whole naming theme goes from there.

## Modular structure

* [Lapland](#lapland) - loader/starter module
* [Santa](#santa) - http server module
* gild - request handler function
* home - public folder with client side files
* apiBox - folder with api routes
* apiElf - module to load and handle api routes
* sesElf - module to handle sessions
* passElf - module to handle passwords
* dataElf - module to handle data storage (db etc.)

## Lapland
[(structure).](#modular-structure)/lapland.js

The main module to load and start the rest of the framework.
It exports the ```lapland``` object with the method to start it:

#### ```lapland.wish(details)```
an async method that takes ```details``` object with the next properties:

* **`details.PORT`** - a port to run at

## Santa
[(structure).](#modular-structure)/santa/index.js

A server module, includes the request handler [gild](#gild)
