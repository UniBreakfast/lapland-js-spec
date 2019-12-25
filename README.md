# Lapland specification (Vanilla* JS backend framework)
*<sup>\*the only exception is mongodb module</sup>*

Lapland is YAFJSF (yet another fraken JavaScript framework)
I'm curious to play in development of.))

Here's the [repo with the main module](https://github.com/UniBreakfast/lapland)
itself.

I struggled for some time trying to find the names for my modules
that I would actually like. Until I decided to see them as actors
working on the common task - in a sense like Santa's elfs.
So the whole naming theme goes from there.

![Santa's Workshop sketch by Cécile Carre](https://raw.githubusercontent.com/UniBreakfast/lapland-js-spec/master/C%C3%A9cile%20Carre%20-%20Santa's%20Workshop.jpg)

<sup>kind of inspired by [Santa's Workshop artwork by Cécile Carre](https://www.behance.net/gallery/68806033/Santas-Workshop)</sup>


## Modular structure

* [Lapland](#lapland) - loader/starter module
    ([repo](https://github.com/UniBreakfast/lapland))
* [Santa](#santa) - http server module
    ([repo](https://github.com/UniBreakfast/santa))
* [shop](#shop) - request handler function (above)
* [home](#home) - public folder with client side files
    ([repo](https://github.com/UniBreakfast/home))
* [apiBox](#apibox) - folder with api routes
    ([repo](https://github.com/UniBreakfast/apibox))
* [apiElf](#apielf) - module to load and handle api routes
    ([repo](https://github.com/UniBreakfast/apielf))
* [sesElf](#seself) - module to handle sessions
    ([repo](https://github.com/UniBreakfast/seself))
* [passElf](#pasself) - module to handle passwords
    ([repo](https://github.com/UniBreakfast/pasself))
* [dataElf](#dataelf) - module to handle data storage (db etc.)
    ([repo](https://github.com/UniBreakfast/dataelf))


### Flowcharts
Interaction Diagrams are on [this page](https://github.com/UniBreakfast/lapland-js-spec/blob/master/flowcharts.md#bare-minimum-interactions)


## Lapland
[(structure).](#modular-structure)/lapland.js
<sub>[(all files in repo)](https://github.com/UniBreakfast/lapland)</sub>

The main module to load and start the rest of the framework.
It exports the `lapland` object with the method to start it:

#### `lapland.wish(details)`
an async method that takes `details` object with the next properties:

* **`details.PORT`** - a port to run at


## Santa
[(structure).](#modular-structure)/santa/index.js
<sub>[(all files in repo)](https://github.com/UniBreakfast/santa)</sub>

A server module, creates an http-server and exports it,
includes the request handler function [shop](#shop).

### shop
[(structure).](#modular-structure)/santa/index.js
<sub>[(all files in repo)](https://github.com/UniBreakfast/santa)</sub>

A shop (as in "Santa's workshop where elves are making and wrapping gifts
for the children") is the function where the handling of every client's request
to the [Santa](#santa) (server) happens.


## home
[(structure).](#modular-structure)/home/*.html, *.css, *.js, *.jpg, *.png, ...
<sub>[(all files in repo)](https://github.com/UniBreakfast/home)</sub>

Public folder with the front-end files (client side) available on the server
for client requests.


## apiBox
[(structure).](#modular-structure)/api/routes/*.js
<sub>[(all files in repo)](https://github.com/UniBreakfast/apibox)</sub>

An /api folder with js files exporting certain api handling functions.


## apiElf
[(structure).](#modular-structure)/apielf/index.js
<sub>[(all files in repo)](https://github.com/UniBreakfast/apielf)</sub>

A module that loads api processing functions from [apiBox](#apibox)
into an `api` object, selects and calls the appropriate one
when request requires it.


## sesElf
[(structure).](#modular-structure)/seself/index.js
<sub>[(all files in repo)](https://github.com/UniBreakfast/seself)</sub>

A module that handles sessions when it is necessary and allows
or denies the execution of the api handler function.
It provides methods to start or end sessions, list them, label, limit by time.

It exports a `sesElf` object with one method
to acquaint with the `passElf` and `dataElf` objects it needs to do its job:

#### `sesElf.attach(dataElf)`
a method that takes a reference to the `dataElf` object it should use.
That makes more methods available on the `sesElf` object and returns it.

#### `sesElf.start(userid)`
a method that takes `userid` number and creates a session for that user.
It then returns an object `{sid, token}` with the `id` of session created and
a `token` to check its validity.
If user with `userid` isn't found it returns`false`.

#### `sesElf.check({sid, token})`
an async method that takes a `ses` object with session id and `token`
and checks if that session exists and if `token` is valid.
Returns new token if session is confirmed and `false` if otherwise.

#### `sesElf.end(sid)`
an async method that takes a `sid` number and deletes the session with that id.
Returns `true` if session was found and deleted and `false` otherwise.

#### `sesElf.label(sid, label)`
an async method that takes a `sid` number and a `label` string
and names the session found by that id with that `label`.
Returns `true` if successful and `false` if session not found.

#### `sesElf.limit(sid, timeout)`
an async method that takes `sid` and `timeout` numbers and sets the idle
life limit for the corresponding session (counting from the last check).
It disables the limit if `timeout` is falsy.
Returns `true` if successful and `false` if session not found.

#### `sesElf.limitAll(userid, timeout)`
an async method that takes `userid` and `timeout` numbers and sets the idle
life limit all the sessions current and future for the user with that id.



## passElf
[(structure).](#modular-structure)/pasself/index.js
<sub>[(all files in repo)](https://github.com/UniBreakfast/pasself)</sub>

A module that checks passwords when it is necessary and allows
or denies the execution of the api handler function.
It also registers new users and allows the password change if necessary.

It exports a `passElf` object with one method
to acquaint with the `dataElf` object it needs to do its job:

#### `passElf.attach(dataElf)`
a method that takes a reference to the `dataElf` object it should use.
That makes more methods available on the `dataElf` object and returns it.

#### `passElf.reg(login, pass)`
an async method that takes non empty strings `login` and `pass` and
registers a new user with password hashed.
If login is already occupied it should return `false`.
If successful it should return the `id` of newly made user record.

#### `passElf.check(id | login, pass)`
an async method that takes an `id` number or a `login` string and
a `pass` string, checks if it is the correct password according to hash.
Returns `true` if positive, `false` if not, `null` if brute force suspected.

#### `passElf.change(id | login, pass)`
an async method that takes an `id` number or a `login` string and
a `pass` string, and saves this new password hashed for the user.
Returns `true` if successful, `false` if not (old password).
Fails if `id`/`login` not found.


## dataElf
[(structure).](#modular-structure)/dataelf/index.js
<sub>[(all files in repo)](https://github.com/UniBreakfast/dataelf)</sub>

A module that handles data on its own or by using a database.
Multiple convenient methods to run complex queries on the db
are supposed to be added to it after linking.

It exports a `dataElf` object with one method to make it useful:

#### `dataElf.link(dbStr)`
an async method that takes a connect string and makes more methods available
on the `dataElf` object to work with the database.
It also returns the `dataElf` object.

#### `dataElf.db`
a property reference to the database client object
with the corresponding methods to query it directly.

#### `dataElf.addArr(name [,...names])`
an async method that adds one or more new arrays (collections) to the database.
That is if they are do not exist yet.

#### `dataElf.user(id | {...props})`
an async method that returns a record from the `users` collection,
if finds one by `id` or option property (like `login`).
`id` supposed to be an integer, options object supposed to have property
(or more) with values to find matching record.
Returns `{id: Number, login: String, hash: String}` or `null` if nothing found.

#### `dataElf.addUser(login, hash)`
an async method that adds a record to the `users` collection in the database.
`login` and `hash` are supposed to be non empty strings.
It should return `false` if there is already a record with that `login`.
If successful it will return an `id` of created record.

#### `dataElf.updUser(id | {...props}, {...newProps})`
an async method that updates a record in the `users` collection in the database.
It supposed to find the record by `id` or by properties provided as an object.
It should return `false` if record not found
or `true` if record found and updated.
