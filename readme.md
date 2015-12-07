# verb [![NPM version](https://img.shields.io/npm/v/verb.svg)](https://www.npmjs.com/package/verb) [![Build Status](https://img.shields.io/travis/jonschlinkert/verb.svg)](https://travis-ci.org/jonschlinkert/verb)

> Documentation generator


## Install
Install with [npm](https://www.npmjs.com/)

```sh
$ npm i verb --save
```

## Usage
## toc

<!-- toc -->

**TODO**

- [x] publish a fast, composable, highly extendable project app with a user-friendly and expressive API
- [x] support sub-apps (to any level of nesting)
- [x] support streams, tasks, and plugins compatible with both [gulp][] and [assemble][assemble-core]
- [x] make it super easy to run specific tasks from any app or sub-app, programmatically or via CLI 
- [x] support _instance plugins_ that allow you to easily add functionality and features to verb
- [x] support any template engine
- [x] support using any number of template engines at once, so that different file types can simultaneously be handled by the engine that was registered for that file type
- [x] support templates as [vinyl][] files, simple to use template collections and lists (for pagination, sorting, groups etc)
- [x] support middleware that can be run on all files or specific files, and at specific points during the _build process_ (like `onLoad`, `preRender`, `postRender`, etc) 
- [x] 820+ unit tests
- [ ] create and publish apps (we created a handful of apps that we've been using locally, these will be published shortly)
- [ ] CLI docs (started)
- [ ] User help (e.g. when the user does `verb help` or just `verb`)
- [ ] API docs
- [ ] App guidelines and conventions

## Install

To get started, you'll first need to install `verb` globally using [npm][], along with any apps you'd like to run.

**Install verb**

Install globally with [npm](https://www.npmjs.com/)

```sh
$ npm i -g verb
```

**Install a verb app**

If you aren't familiar with verb, just take the `node` app for a test drive:

```sh
$ npm i -g verb-node
```

**Run a app**

If everything installed correctly, you should now be able to verb a new project with the following command (make sure you run the command from an empty directory!):

```sh
$ verb node
```

***

## Usage

```sh
$ verb <command> [args]
```

## CLI

_(WIP)_

### help

_(TODO)_

Get started with Verb. 

```js
$ verb help
```

### init

_(TODO)_

Get started with Verb. 

```js
$ verb init
```

Upon running `init`, verb will prompt you for answers to the following questions:


### Run apps

```sh
$ verb <app name> [options]
```

**Example**

Run app `abc`

```sh
$ verb abc
```

### Run tasks

To run a task on the `base` app, just pass the name of the task to run.

```sh
$ verb <task name> [options]
```

Unless overridden by the user, the `base` app is the default app that ships with Verb. This app doesn't really "verb" anything, but it will prompt you for a few answers (if you choose), to store data that's commonly needed by templates, like `author.name`, GitHub `username`, etc. 

**Example**

Run task `bar`:

```sh
$ verb bar
```

### Run sub-apps

> Sub-apps are normal apps that are called from (or registered by) other apps.

Dot-notation is used for getting and runing sub-apps. 

```sh
$ verb <app name>.<sub-app name> [options]
```

**Examples**

Run sub-app `b` on app `a`:

```sh
$ verb a.b [options]
```

Run sub-app `c`:

```sh
$ verb a.b.c [options]
```

And so on...


### Run a app's tasks

```sh
$ verb <app name>:<task name> [options]
```

**Example**

Run task `bar` on app `foo`.

```sh
$ verb foo:bar 
```

### Run a sub-app's tasks

```sh
$ verb <app name>.<sub-app name>:<task name> [options]
```

**Example**

Run task `foo` on sub.app `a.b.c`.

```sh
$ verb a.b.c:foo 
```

## API


### .getConfig

Static method that first tries to get the `verbfile.js` in the root of the current project, then if not found, falls back to the default `verbfile.js` in this project. 

Once resolved, the verbfile will be loaded and used to create the "base" instance of verb. All other instances will be stored on the base instance's `apps` object.

**Params**

* `filename` **{String}**: Then name of the config file to lookup.
* `returns` **{Object}**: Returns the "base" instance.

**Example**

```js
var verb = Verb.getConfig('verbfile.js');
```

### .getTask

Get task `name` from the `verb.tasks` object.

**Params**

* `name` **{String}**
* `returns` **{Object}**

**Example**

```js
verb.getTask('abc');

// get a task from app `foo`
verb.getTask('foo:abc');

// get a task from sub-app `foo.bar`
verb.getTask('foo.bar:abc');
```

### .addApp

Alias for `register`. Adds a `app` with the given `name` to the `verb.apps` object.

**Params**

* `name` **{String}**: The name of the config object to register
* `config` **{Object|Function}**: The config object or function

**Example**

```js
base.addApp('foo', function(app, base, env) {
  // `app` is a `Verb` instance created for the app
  // `base` is a "shared" instance that provides access to all loaded apps
  // `env` is a configuration/environment object with details about the app,
  // user cwd, etc
});
```

### .hasApp

Return true if app `name` is registered. Dot-notation may be used to check for [sub-apps](#sub-apps).

**Params**

* `name` **{String}**
* `returns` **{Boolean}**

**Example**

```js
base.hasApp('foo.bar.baz');
```

### .getApp

Return app `name` is registered. Dot-notation may be used to get [sub-apps](#sub-apps).

**Params**

* `name` **{String}**
* `returns` **{Boolean}**

**Example**

```js
base.getApp('foo');
// or
base.getApp('foo.bar.baz');
```

### .extendApp

Extend an app.

**Params**

* `app` **{Object}**
* `returns` **{Object}**: Returns the instance for chaining.

**Example**

```js
var foo = base.getApp('foo');
foo.extendApp(app);
```

### .invoke

Invoke app `fn` with the given `base` instance.

**Params**

* `fn` **{Function}**: The app function.
* `app` **{Object}**: The "base" instance to use with the app.
* `returns` **{Object}**

**Example**

```js
verb.invoke(app.fn, app);
```

## Authoring apps

_(TODO)_

### App naming conventions

Use `verb-` as the prefix, followed by any words of your choosing to describe the purpose of the app.


[assemble]: http://assemble.io
[assemble-core]: https://github.com/assemble/assemble-core
[base-methods]: https://github.com/jonschlinkert/base-methods
[gulp]: http://gulpjs.com
[scaffold]: https://github.com/jonschlinkert/scaffold
[verb]: https://github.com/verbose/verb
[vinyl]: http://github.com/gulpjs/vinyl

## Running tests
Install dev dependencies:

```sh
$ npm i -d && npm test
```

## Contributing
Pull requests and stars are always welcome. For bugs and feature requests, [please create an issue](https://github.com/jonschlinkert/verb/issues/new).

## Author
**Jon Schlinkert**

+ [github/jonschlinkert](https://github.com/jonschlinkert)
+ [twitter/jonschlinkert](http://twitter.com/jonschlinkert)

## License
Copyright © 2015 [Jon Schlinkert](https://github.com/jonschlinkert)
Released under the MIT license.

***

_This file was generated by [verb](https://github.com/verbose/verb) on Sun Dec 06 2015 21:35:43 GMT-0500 (EST)._

[ansi-colors]: https://github.com/doowb/ansi-colors
[assemble-core]: https://github.com/assemble/assemble-core
[assemble-loader]: https://github.com/jonschlinkert/assemble-loader
[base-argv]: https://github.com/jonschlinkert/base-argv
[base-cli]: https://github.com/jonschlinkert/base-cli
[base-config]: https://github.com/jonschlinkert/base-config
[base-pipeline]: https://github.com/jonschlinkert/base-pipeline
[base-questions]: https://github.com/jonschlinkert/base-questions
[base-runner]: https://github.com/jonschlinkert/base-runner
[base-store]: https://github.com/jonschlinkert/base-store
[common-middleware]: https://github.com/jonschlinkert/common-middleware
[engine-base]: https://github.com/jonschlinkert/engine-base
[extend-shallow]: https://github.com/jonschlinkert/extend-shallow
[get-value]: https://github.com/jonschlinkert/get-value
[global-modules]: https://github.com/jonschlinkert/global-modules
[has-glob]: https://github.com/jonschlinkert/has-glob
[helper-copyright]: https://github.com/helpers/helper-copyright
[helper-reflinks]: https://github.com/helpers/helper-reflinks
[helper-related]: https://github.com/helpers/helper-related
[is-valid-glob]: https://github.com/jonschlinkert/is-valid-glob
[lazy-cache]: https://github.com/jonschlinkert/lazy-cache
[matched]: https://github.com/jonschlinkert/matched
[minimist]: https://github.com/substack/minimist
[node-resolve]: https://github.com/substack/node-resolve
[resolve-dir]: https://github.com/jonschlinkert/resolve-dir
[stream-exhaust]: https://github.com/chrisdickinson/stream-exhaust
[success-symbol]: https://github.com/jonschlinkert/success-symbol
[time-stamp]: https://github.com/jonschlinkert/time-stamp
