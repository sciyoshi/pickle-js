pickle.js is a JavaScript implementation of the Python pickle format. It supports pickles containing a cross-language subset of the primitive types.

#### Key differences between pickle.js and pickle.py: ####
  * text pickles only
  * some types are lossily converted (e.g. int)
  * some types are not supported (e.g. class)

#### Key differences between pickles and JSON: ####
  * pickles are not human readable
  * pickles can express complex objects (multiple references and recursion)

## API ##
The API for pickle.js was chosen to match the Python pickle module.
```
 pickle.dumps(object) -> string

 pickle.loads(string) -> object
```

## Conversions ##
Differences between Python and JavaScript types prevent pickling with
pickle.js from being cleanly invertible. For instance, in Python, there is a
distinction between integer and floating point numerical types, but in
JavaScript there is only one type. Integers contained within a pickle are
unpickeled to Numbers and so on.

#### unpickle (loads) ####
| **from Python** | **to JavaScript** |
|:----------------|:------------------|
| str             | String            |
| int             | Number            |
| float           | Number            |
| list            | Array             |
| dict            | Object (all keys get stringed) |
| bool            | Boolean           |
| None            | null              |

#### pickle (dumps) ####
| **from JavaScript** | **to Python** |
|:--------------------|:--------------|
| String              | str           |
| Number              | float         |
| Array               | list          |
| Object              | dict          |
| Boolean             | bool          |
| null                | None          |