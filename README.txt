pickle.js is a JavaScript implementation of the Python pickle format. It
supports pickles containing a cross-language subset of the primitive types.

pickle.js was written using a combination of the pickle.py docs and
"observational learning." (Banging on ipython ;-)

==== Key differences between pickle.js and pickle.py: ====
 * text pickles only
 * some types are lossily converted (e.g. int)
 * some types are not supported (e.g. class)

==== Key differences between pickles and JSON: ====
 * pickles are not human readable
 * pickles can express complex objects (multiple references and recursion)

== API ==
The API for pickle.js was chosen to match the Python pickle module.

pickle.dumps(object) -> string
pickle.loads(string) -> object

== Features and Limitations ==
pickle.js can pickle and unpickle objects with complex graphs. This can
include shared references and cycles.

pickle.js currently supports a cross-language subset of the pickle protocol 0
(text mode). Text mode pickles are less compact than binary pickles (protocols
1 and 2), but are more appropriate for JavaScript. Version 0 pickles are the
format used by dumps() and loads() in Python.

Support for binary pickles may be added in the future with the convention that
they be delivered as integer arrays, base64 strings, or ByteArrays (used by
ActionScript and possibly future JavaScript versions).

pickle.js does not support pickles containing functions, classes, or
instances.

== Convsersions ==
Differences between Python and JavaScript types prevent pickling with
pickle.js from being cleanly invertible. For instance, in Python, there is a
distinction between integer and floating point numerical types, but in
JavaScript there is only one type. Integers contained within a pickle are
unpickled to Numbers and so on.

=== unpickle (loads) ===
* Python str            -> JavaScript String
* Python int            -> JavaScript Number
* Python float          -> JavaScript Number
* Python list           -> JavaScript Array
* Python dict           -> JavaScript Object (all keys get stringed)
* Python bool           -> JavaScript boolean
* Python None           -> JavaScript null

=== pickle (dumps) ===
JavaScript String       -> Python str
JavaScript Number       -> Python float
JavaScript Array        -> Python list
JavaScript Object       -> Python dict
JavaScript Boolean      -> Python bool
JavaScript null         -> Python None

== History ==

v 0.5
    Cross browser compatibility (removing console.logs :-)

v 0.4
    Performance optimizations

v 0.3
    * null
    * bool

v 0.2
    * serialization of JavaScript object (dumps)

v. 0.1
    The first cut of pickle.js includes support for the primitive types plus
    references. Pickling and unpickling are included.

    * loads
    * integers
    * floats
    * dicts
    * lists
    * strings

    * references
    * recursive objects
    * works in at least 1 browser (firefox 2)
