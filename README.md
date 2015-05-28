Pixelworker Runtime Environment
===============================

Mission: Have the same image manipulation algorithms run in Firefox for
show¹ and in io.js for automation.
(¹ Might double as an "average user" windows compatiblity mode.)


Meta definitions
----------------
Throughout this document,
  * `pxalgo` refers to a JS module object that holds the image algorithm.
    * think `var pxalgo = require('./invert_opacity');`
  * To "then-return" a value means to return either the value or a then-able
    (semi-promise) for the value. To "then-expect" is to expect such a value.


API declaration
===============

pxwrkDescribeAPI
----------------
In order to provide the proper input data for `pxalgo`,
`pxwrk` will call `pxalgo.pxwrkDescribeAPI` with a single argument,
which is a reference to the `pxwrk` module. As result it then-expects
a JS object which should hold these properties:

  * `inputs`: An array of input descriptions.
  * `actions`: An array of action descriptions.

Input descriptions
------------------
… are JS objects with these keys:

  * `name` (required): Identifier for a form field or CLI option name.
    You can use lowercase letters, digits and hyphens, but start with a letter.
  * `descr`: Short description of what's expected.
  * `type` (required): see "Input types" below.
  * `multi`: Reserved for future use.

Input types
-----------
… define how to inquire and convert user input.

  * `text`: Use for rather short strings.
  * `text-file`: Use for large amounts of text.
  * `number`: Range limited by JS, use `text` for huge or precise numbers.
  * `bool`: Checked/set = `true`, not checked/ unset = `false`.
  * `maybe`: Yes = `true`, no = `false`, dunno = `null`.
  * `select-one`: Like `text` but offer `items` to pick.
  * `select-many`: Zero or more `items`, given as an Array.
  * `json`: Surprise package. Parsed by `pxwrk`.
  * `json-file`: Accept larger surprise packages.
  * `sprite`: A JS object that can be drawn onto a canvas.
    It should have integer properties `width` and `height`.
    A source URL might be set in its `srcUrl` property.
    The CLI might be limited to relative URLs.
  * `canvas`: Like `sprite` but `pxwrk` will attempt to deliver a JS canvas,
    not just any object. `pxalgo` can expect a `getContext` method on it.

Action descriptions
-------------------
… can be just strings (used as the `func` setting),
or JS objects with these keys:

  * `name`: Optional human-readable name.
    If missing, a name may be guessed based on the `func` property.
  * `func`: The action starter function, given as either
    * a function
    * an empty string: The module object is the action starter.
    * a non-empty string: Property name by which to look up the action
      starter in the module object.
  * `descr`: Short preview of what should happen.

Output descriptions
-------------------
:TODO:

  * `name` (optional)
  * `filename` (optional): recommendation
  * `type`
    * (l8r?) `progress`
    * `msglog`
    * `errlog`
    * `image`
    * `json` (may include numbers and strings)
    * `html`
  * `descr`















License
=======
:TODO:




&nbsp;

-*- coding: utf-8, tab-width: 2 -*-
