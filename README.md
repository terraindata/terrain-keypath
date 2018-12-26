# terrain-keypath
[![version](https://img.shields.io/npm/v/terrain-keypath.svg)](https://www.npmjs.org/package/terrain-keypath)
[![dependencies](https://david-dm.org/terraindata/terrain-keypath.svg)](https://david-dm.org/terraindata/terrain-keypath)
[![devDependencies](https://david-dm.org/terraindata/terrain-keypath/dev-status.svg)](https://david-dm.org/terraindata/terrain-keypath#info=devDependencies)

_An opinionated keypath type_

A natural task in JS is to query or modify an element of a deeply-nested JSON object.
However, if you're doing operations like that frequently and involving dynamic, different
elements, it becomes a pain to describe where all those elements are located within the
deep object.

`terrain-keypath` provides a standard format for specifying elements of, among other
possible use cases, deep JSON objects.  A `KeyPath` is an array of `WayPoint`s, each
of which is a `string` or `number`.  For example, for the document
```js
doc = {
 a: {
  b: {
   c: [
     { d: 'e' },
     { f: 'g' },
   ]
  }
 }
}
```
you would use e.g. `const kp = new KeyPath(['a', 'b', 'c', '1', 'f'])` to obtain
a reference to the object whose value is `'g'`.

`KeyPath` makes the design decision that **every** `WayPoint` should be a `string`
**unless** you are indicating the unique numeric **wildcard** token `-1`.  The
semantic intention of the wildcard token is to denote "all children" of an element,
e.g. all entries of an array.  For example,
`const kp = new KeyPath(['a', 'b', 'c', -1])`
is meant to mean "all children of a.b.c".

It's worth emphasizing that **any** string is a valid JSON field name, including
field names with special characters like `.`, `*`, etc.  Thus, if you get a deep
JSON document "from the wild," there's no guarantee that other existing keypath
libraries (which typically use such special tokens as wildcards or waypoint
delimiters) will work.

Particularly in conjunction with [yadeep](https://github.com/terraindata/yadeep),
we have tested `terrain-keypath` against a broad variety of wild JSON documents
and have successfully deployed enterprise applications using this keypath type.

TypeScript definitions included!

## Installation

    npm install terrain-keypath


