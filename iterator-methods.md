# Array Iterator Methods

These methods take a callback as a parameter, which is then executed once for every element in the array.

### Table of Contents

* [every](#every)
* [some](#some)
* [filter](#filter)
* [find](#find)
* [findIndex](#findindex)
* [keys](#keys)
* [map](#map)
* [reduce](#reduce)
* [reduceRight](#reduceright)
* [values](#values)

## every

Check if all elements in an array cause the passed callback to return `true`. Returns `true` or `false`.

Before the `every` method existed, you might have done this the following way:

```javascript
var arr1 = [80, 95, 72, 100, 85]
var noneUnder80 = true
var i = 0, len = arr1.length

for (i; i < len; i++) {
  if (arr1[i] < 80) {
    noneUnder80 = false
    break
  }
}

console.log(noneUnder80) // false
```

Since `every` returns a boolean, we can assign the method call directly to `noneUnder80`. If any element in the array causes the callback function to return `false`, `every` will return `false`.

```javascript
const arr1 = [80, 95, 72, 100, 85]
const noneUnder80 = arr1.every(ele => {
  return ele >= 80
})

console.log(noneUnder80) // false
```

## some

Check if any of the elements in an array cause the passed callback to return `true`. As long as at least one element passes, `some` will return `true`, otherwise it will return `false`.

```javascript
const arr1 = [2, 4, 6, 8]
let isBiggerThan10 = arr1.some(ele => ele > 10)

console.log(isBiggerThan10) // false

const arr2 = [2, 4, 6, 8, 12]
isBiggerThan10 = arr2.some(ele => ele > 10)

console.log(isBiggerThan10) // true
```

## filter

TODO

## find

Return the first element in an array that evaluates a given callback to `true`. If no matching element is found, return `undefined`.

```javascript
const userEntries = [
  { name: 'maria', age: 29 },
  { name: 'jose', age: 35 },
  { name: 'emilio', age: 27 }
]

const getUserEntry = (username) => {
  return userEntries.find(ele => ele.name === username)
}

const userEntry1 = getUserEntry('jose')
const userEntry2 = getUserEntry('samantha')

console.log(userEntry1); // { name: 'jose', age: 35 }
console.log(userEntry2); // undefined
```

## findIndex

TODO

## keys

TODO

## map

TODO

## reduce

TODO

## reduceRight

TODO

## values

TODO
