# Lapland specification (Vanilla* JS backend framework) 
*\*the only exception is mongodb module*

Lapland is YAFJSF (yet another fraken JavaScript framework) I'm curious to play in development of.))
Here's the [repo with the main module](https://github.com/UniBreakfast/lapland) itself.
I struggled for some time trying to find the names for my modules that I would actually like. Until I decided to see them as actors working on the common task - in a sense like Santa's elfs. So the whole naming theme goes from there.

## Modular structure

* [Lapland](#lapland) - loader/starter module
* [Santa](#santa) - http server module
* [gild](#gild) - request handler function
* [home](#home) - public folder with client side files
* [apiBox](#apibox) - folder with api routes
* [apiElf](#apielf) - module to load and handle api routes
* [sesElf](#seself) - module to handle sessions
* [passElf](#pasself) - module to handle passwords
* [dataElf](#dataelf) - module to handle data storage (db etc.)

## Lapland
[(structure).](#modular-structure)/lapland.js

The main module to load and start the rest of the framework.
It exports the ```lapland``` object with the method to start it:

#### ```lapland.wish(details)```
an async method that takes ```details``` object with the next properties:

* **`details.PORT`** - a port to run at

## Santa
[(structure).](#modular-structure)/santa/index.js

A server module, includes the request handler [gild](#gild).

### gild
[(structure).](#modular-structure)/santa/index.js

A function where the handling of every child's (client's) request to the [Santa](#santa) (server) happens.

## home
[(structure).](#modular-structure)/home/*.html, *.css, *.js, *.jpg, *.png, ...

Public folder with the front-end files (client side) available on the server for client requests.

## apiBox
[(structure).](#modular-structure)/api/index.js

Aa /api folder with, includes the request handler [gild](#gild)

## apiElf
[(structure).](#modular-structure)/apielf/index.js

A server module, includes the request handler [gild](#gild)

## sesElf
[(structure).](#modular-structure)/seself/index.js

A server module, includes the request handler [gild](#gild)

## passElf
[(structure).](#modular-structure)/pasself/index.js

A server module, includes the request handler [gild](#gild)

## dataElf
[(structure).](#modular-structure)/dataelf/index.js

A server module, includes the request handler [gild](#gild)
