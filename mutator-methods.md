# Avoiding Array Mutations

Mutating arrays directly in different parts of your codebase may make it more difficult to reason about their value at any given point, as well as make it more difficult to test the functions that affect them.

## Mutator Methods

These are available array methods that directly manipulate the value of an array. We look at alternatives available that will instead return a new array, maintaining the value of the original array. Note some of these alternatives use features added in ES2015.

### fill

Fill the elements in an array with a given value, with the option of specifying a start and end index.  
Use `map` instead. It may be useful to create a reusable helper function to support the same optional parameters as `fill`.

```javascript
const arr1 = [1, 2, 3]

// a basic implementation of a helper function
const immutFill = (arr, value, start, end) => {
  return arr.map((ele, index) => {
    if (!start && start !== 0) return value
    if (index >= start) {
      if (end) {
        return index < end ? value : ele
      }
      return value
    }
    return ele
  })
}

const arr2 = immutFill(arr1, 4)
const arr3 = immutFill(arr1, 4, 1)
const arr4 = immutFill(arr1, 4, 1, 2)

// without using a helper
// requires knowing exactly what we want to fill with and where we want to fill
// here we want to fill all values after the first with 7
const arr5 = arr1.map((ele, index) => index === 0 ? ele : 7)

console.log(arr1) // [1, 2, 3]
console.log(arr2) // [4, 4, 4]
console.log(arr3) // [1, 4, 4]
console.log(arr4) // [1, 4, 3]
console.log(arr5) // [1, 7, 7]
```

### pop

Remove the last element in an array and return that element.  
Use `slice` instead.

```javascript
const arr1 = [1, 2, 3]

const arr2 = arr1.slice(0, arr1.length - 1)

const lastElementOfArr1 = arr1[arr1.length - 1]

console.log(arr1) // [1, 2, 3]
console.log(arr2) // [1, 2]
console.log(lastElementOfArr1) // 3
```

Note that because we never mutate our array, we can access the value `pop` would return (`lastElementOfArr1`) whenever we need it.

### push

Add a new element to the end of an array and return the new array's length.  
Use the spread operator (`...`) instead.

```javascript
const arr1 = [1, 2, 3]
const arr2 = [...arr1, 4, 5]
const arr2Length = arr2.length
console.log(arr1) // [1, 2, 3]
console.log(arr2) // [1, 2, 3, 4, 5]
console.log(arr2Length) // 5
```

Alternatively, you can use `concat`.

```javascript
const arr1 = [1, 2, 3]
const arr2 = arr1.concat([4, 5])
const arr2Length = arr2.length
console.log(arr1) // [1, 2, 3]
console.log(arr2) // [1, 2, 3, 4, 5]
console.log(arr2Length) // 5
```

Note that once we have created our new array, we can access the value `push` would return (`arr2Length`) whenever we need it.

### reverse

Reverse the order of an array.  
Use `reduceRight` instead.

```javascript
const arr1 = [1, 2, 3]

const immutReverse = (arr) => {
  return arr.reduceRight((a, b) => {
    a.push(b)
    return a
  }, [])
}

const arr2 = immutReverse(arr1)

console.log(arr1) // [1, 2, 3]
console.log(arr2) // [3, 2, 1]
```

Note we are using `push` inside our callback. This is pushing to the empty array (`[]`) we have set as the initial value of `reduceRight`, and is what the method will ultimately return. So even though we are using a mutative method, there are no mutations taking place _outside_ our method call, which is the expectation.

### shift

Remove the first element in an array and return that element.  
Use `slice` instead.

```javascript
const arr1 = [1, 2, 3]
const arr2 = arr1.slice(1)
const firstElementOfArr1 = arr1[0]

console.log(arr1) // [1, 2, 3]
console.log(arr2) // [2, 3]
console.log(firstElementOfArr1) // 1
```

Note that because we never mutate our array, we can access the value `shift` would return (`firstElementOfArr1`) whenever we need it.

### sort

Sort the elements of an array.  
Create a unique copy the array using the spread operator (`...`) before performing the sort.

```javascript
const arr1 = [2, 5, 1, 3, 4]
const arr2 = [...arr1].sort((a, b) => b > a)
console.log(arr1) // [2, 5, 1, 3, 4]
console.log(arr2) // [5, 4, 3, 2, 1]
```

Alternatively, you can use `concat`.

```javascript
const arr1 = [2, 5, 1, 3, 4]
const arr2 = [].concat(arr1).sort((a, b) => b > a)
console.log(arr1) // [2, 5, 1, 3, 4]
console.log(arr2) // [5, 4, 3, 2, 1]
```

Note that when using `sort`, the comparison function is executed multiple times per element within the array. If this function is relatively complex and/or your source array is relatively large, this may increase the overhead of the sort. In this case consider [using the map method to sort](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort#Sorting_with_map).

### splice

Add and/or remove elements at a specific range in an array.  
Use `slice` with the spread operator (`...`) instead.

```javascript
const arr1 = [1, 2, 3]

const indexToRemove = 1
const arr2 = [
  ...arr1.slice(0, indexToRemove),
  ...arr1.slice(indexToRemove + 1)
]

const indexToReplace = 1
const eleToAdd = 5
const arr3 = [
  ...arr1.slice(0, indexToReplace),
  eleToAdd,
  ...arr1.slice(indexToReplace + 1)
]

console.log(arr1) // [1, 2, 3]
console.log(arr2) // [1, 3]
console.log(arr3) // [1, 5, 3]
```

Note the above example shows removing one element (`arr2`) and replacing one element (`arr3`). For a range of elements, consider creating a helper function using this example as a starting point.

### unshift

Add a new element to the start of an array and return the new array's length.  
Use the spread operator (`...`) instead.

```javascript
const arr1 = [1, 2, 3]
const arr2 = [4, 5, ...arr1]
const arr2Length = arr2.length
console.log(arr1) // [1, 2, 3]
console.log(arr2) // [4, 5, 1, 2, 3]
console.log(arr2Length) // 5
```

Alternatively, you can use `concat`.

```javascript
const arr1 = [1, 2, 3]
const arr2 = [4, 5].concat(arr1)
const arr2Length = arr2.length
console.log(arr1) // [1, 2, 3]
console.log(arr2) // [4, 5, 1, 2, 3]
console.log(arr2Length) // 5
```

Note that once we have created our new array, we can access the value `unshift` would return (`arr2Length`) whenever we need it.

## forEach

The `forEach` method iterates over an array and executes a callback function once per array element. While this in and of itself is not mutative, the callback is often used to perform a mutation on the array element.

```javascript
let arr1 = [1, 2, 3]

arr1.forEach((ele, index, srcArray) => {
  srcArray[index] = ele++
})

console.log(arr1) // [2, 3, 4]
```

Here the callback is mutating the value of each element in `arr1` by incrementing its value by 1.  
Use `map` instead.

```javascript
const arr1 = [1, 2, 3]
const arr2 = arr1.map(ele => ele + 1)

console.log(arr1) // [1, 2, 3]
console.log(arr2) // [2, 3, 4]
```
