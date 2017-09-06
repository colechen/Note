- const
- let, {}
- Arrow function
- default parameters
- rest parameters
- spread operators
- template literals
- property shorthand obj = { x, y } equiv. obj = { x: x, y: y }
- computed property name 
let obj = {
	foo: “bar”,
	[“baz” + quux() ]: 42
}

Restructuring:
- array matching var [a, b] = [1,2,3] //a = 1, b = 2, according position
- object matching with default value //according to name
- parameter context matching
function f ([ name, val ]) {
    console.log(name, val)
}
function g ({ name: n, val: v }) {
    console.log(n, v)
}
function h ({ name, val }) {
    console.log(name, val)
}
f([ "bar", 42 ])
g({ name: "foo", val:  7 })
h({ name: "bar", val: 42 })

Classes
- More like java class 
- in constructor defined class variable
- extends
- parent class access
- static member
- getter/setter

Symbol
- Object.getOwnPropertySymbols(obj) // [ foo, bar ]
- Symbol.for(‘byname’), Symbol()

Map/Set & WeakMap/WeakSet
- Set - add(), delete(), has(), entries()
- Map - get(), set(), delete(), has(), entries(), keys(), values()
- new Set(), add(), size, has(), iterate 
let s = new Set()
s.add("hello").add("goodbye").add("hello")
s.size === 2
s.has("hello") === true
for (let key of s.values()) // insertion order
    console.log(key)

- new Map(), get(key), set(key, value), size, iterate
let m = new Map()
let s = Symbol()
m.set("hello", 42)
m.set(s, 34)
m.get(s) === 34
m.size === 2
for (let [ key, val ] of m.entries())
    console.log(key + " = " + val)

- The WeakSet is weak: References to objects in the collection are held weakly. If there is no other reference to an object stored in the WeakSet, they can be garbage collected. That also means that there is no list of current objects stored in the collection. WeakSets are not enumerable.

Build-In methods
- Object.assign, combine objects
- Array Element Finding, 
[ 1, 3, 4, 2 ].find(x => x > 3) // 4
[ 1, 3, 4, 2 ].findIndex(x => x > 3) // 2
- String repeat
" ".repeat(4 * depth)
"foo".repeat(3)
- String searching, (ES5, indexOf())
"hello".startsWith("ello", 1) // true
"hello".endsWith("hell", 4)   // true
"hello".includes("ell")       // true
"hello".includes("ell", 1)    // true
"hello".includes("ell", 2)    // false
- Number checking
Number.isNaN(42) === false
Number.isNaN(NaN) === true

Number.isFinite(Infinity) === false
Number.isFinite(-Infinity) === false
Number.isFinite(NaN) === false
Number.isFinite(123) === true

- Number Safety checking
Number.isSafeInteger(42) === true
Number.isSafeInteger(9007199254740992) === false

- Number comparison
console.log(0.1 + 0.2 === 0.3) // false
console.log(Math.abs((0.1 + 0.2) - 0.3) < Number.EPSILON) // true

- Number Truncation
console.log(Math.trunc(42.7)) // 42
console.log(Math.trunc( 0.1)) // 0
console.log(Math.trunc(-0.1)) // -0

- Number sign determination
console.log(Math.sign(7))   // 1
console.log(Math.sign(0))   // 0
console.log(Math.sign(-0))  // -0
console.log(Math.sign(-7))  // -1
console.log(Math.sign(NaN)) // NaN


Array
- Array.from(), Array.isArray(), concat(), entries(), filter(), find(), findIndex(), forEach(), includes(), indexOf(), join(), keys(), lastIndexOf(), map(), pop(), push(), reduce(), reduceRight(), reverse(), shift(), slice(), some(), sort(), splice(), toString(), unshift(), values()

sort() - default sort by unicode value, for number sort, provide function
function compareNumbers(a, b) {
  return a - b;
}

String
- .length, charAt(), concat(), endsWith(), indexOf(), lastIndexOf(), match(), replace(), search(), slice(), split(), startsWith(), substr(), substring(), toLowerCase(), toUpperCase(), trim()
