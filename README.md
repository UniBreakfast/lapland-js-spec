# Lapland specification (Vanilla* JS backend framework) 
*<sup>\*the only exception is mongodb module</sup>*

Lapland is YAFJSF (yet another fraken JavaScript framework) I'm curious to play in development of.))

Here's the [repo with the main module](https://github.com/UniBreakfast/lapland) itself.

I struggled for some time trying to find the names for my modules that I would actually like. Until I decided to see them as actors working on the common task - in a sense like Santa's elfs. So the whole naming theme goes from there.

## Modular structure

* [Lapland](#lapland) - loader/starter module ([repo](https://github.com/UniBreakfast/lapland))
* [Santa](#santa) - http server module ([repo](https://github.com/UniBreakfast/santa))
* [gild](#gild) - request handler function (above)
* [home](#home) - public folder with client side files ([repo](https://github.com/UniBreakfast/home))
* [apiBox](#apibox) - folder with api routes ([repo](https://github.com/UniBreakfast/apibox))
* [apiElf](#apielf) - module to load and handle api routes ([repo](https://github.com/UniBreakfast/apielf))
* [sesElf](#seself) - module to handle sessions ([repo](https://github.com/UniBreakfast/seself))
* [passElf](#pasself) - module to handle passwords ([repo](https://github.com/UniBreakfast/pasself))
* [dataElf](#dataelf) - module to handle data storage (db etc.) ([repo](https://github.com/UniBreakfast/dataelf))

## Flowcharts
Interaction Diagrams are on (this page)[https://github.com/UniBreakfast/lapland-js-spec/blob/master/flowcharts.md#bare-minimum-interactions]

## Lapland
[(structure).](#modular-structure)/lapland.js 
<sub>[(all files in repo)](https://github.com/UniBreakfast/lapland)</sub>

The main module to load and start the rest of the framework.
It exports the ```lapland``` object with the method to start it:

#### ```lapland.wish(details)```
an async method that takes ```details``` object with the next properties:

* **`details.PORT`** - a port to run at

## Santa
[(structure).](#modular-structure)/santa/index.js 
<sub>[(all files in repo)](https://github.com/UniBreakfast/santa)</sub>

A server module, creates an http-server and exports it, includes the request handler [gild](#gild).

### gild
[(structure).](#modular-structure)/santa/index.js
<sub>[(all files in repo)](https://github.com/UniBreakfast/santa)</sub>

A function where the handling of every child's (client's) request to the [Santa](#santa) (server) happens.

## home
[(structure).](#modular-structure)/home/*.html, *.css, *.js, *.jpg, *.png, ...
<sub>[(all files in repo)](https://github.com/UniBreakfast/home)</sub>

Public folder with the front-end files (client side) available on the server for client requests.

## apiBox
[(structure).](#modular-structure)/api/routes/*.js
<sub>[(all files in repo)](https://github.com/UniBreakfast/apibox)</sub>

An /api folder with js files exporting certain api handling functions.

## apiElf
[(structure).](#modular-structure)/apielf/index.js
<sub>[(all files in repo)](https://github.com/UniBreakfast/apielf)</sub>

A module that loads api processing functions from [apiBox](#apibox) into an `api` object, selects and calls the appropriate one when request requires it.

## sesElf
[(structure).](#modular-structure)/seself/index.js
<sub>[(all files in repo)](https://github.com/UniBreakfast/seself)</sub>

A module that handles sessions when it is necessary and allows or denies the execution of the api handler function.


## passElf
[(structure).](#modular-structure)/pasself/index.js
<sub>[(all files in repo)](https://github.com/UniBreakfast/pasself)</sub>

A module that checks passwords when it is necessary and allows or denies the execution of the api handler function.

## dataElf
[(structure).](#modular-structure)/dataelf/index.js
<sub>[(all files in repo)](https://github.com/UniBreakfast/dataelf)</sub>

A module that handles data by on its own or using a database.
