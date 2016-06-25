# Array Iterator Methods

These methods take a callback as a parameter, which is then executed once for every element in the array.

### Table of Contents

* [every](#every)
* [some](#some)
* [filter](#filter)
* [find](#find)
* [findIndex](#findindex)
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

Return an array of all elements in an array that evaluate a given callback to `true`.

```javascript
const numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

const oddNumbers = numbers.filter((num) => num % 2 === 1)

console.log(oddNumbers) // [1, 3, 5, 7, 9]
```

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

console.log(userEntry1) // { name: 'jose', age: 35 }
console.log(userEntry2) // undefined
```

## findIndex

Return the index of the first element in an array that evaluates a given callback to `true`. If no matching element is found, return `-1`.

```javascript
const userEntries = [
  { name: 'maria', age: 29 },
  { name: 'jose', age: 35 },
  { name: 'emilio', age: 27 }
]

const getUserEntry = (username) => {
  return userEntries.findIndex(ele => ele.name === username)
}

const userEntry1 = getUserEntry('jose')
const userEntry2 = getUserEntry('samantha')

console.log(userEntry1) // 1
console.log(userEntry2) // -1
```

## map

Return a new array containing the results of calling a given callback on each element in an array.

```javascript
const values = [1, 2, 3, 4]

const valuesDoubled = values.map((ele) => {
  return ele * 2
})

console.log(valuesDoubled) // [2, 4, 6, 8]
```

## reduce

Return a single value by calling a given callback for each element in an array and passing on the value returned by the callback to the next iteration. An optional initial value can be passed to be used as the first value the first the callback runs.


If no initial value is passed the first two values from the array are used, so in the example below the first time the callback runs, `a = 1`, `b = 2`, and the callback returns `3`. The second time the callback runs, `a = 3`, the value returned by the previous iteration, and `b = 3`, the current element in the array.

```javascript
const values = [1, 2, 3, 4]

const sumofValues = values.reduce((a, b) => {
  return a + b
})

console.log(sumofValues) // 10
```

Here we pass an initial value of `5`, so the first time the callback runs, `a = 5`, `b = 1`, and the callback returns `6`. The second time the callback runs, `a = 6`, the value returned by the previous iteration, and `b = 2`.

```javascript
const values = [1, 2, 3, 4]

const sumofValues = values.reduce((a, b) => {
  return a + b
}, 5)

console.log(sumofValues) // 15
```

## reduceRight

`reduceRight` works the same way as `reduce`, but loops backward through the given array starting at the last element in the array.
