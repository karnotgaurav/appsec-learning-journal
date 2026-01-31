a closure is a function in which we remembers the variables cround it even after the parent function has finished running.


function createCounter() {
    let count = 0; // This variable is "closed over" (put in the backpack)

    return function() {
        count++; // The inner function remembers 'count'
        return count;
    };
}

const myCounter = createCounter(); // createCounter runs and finishes.

console.log(myCounter()); // Output: 1
console.log(myCounter()); // Output: 2
console.log(myCounter()); // Output: 3

createCounter finished running lines ago.

Normally, the count variable should have been deleted.

But because myCounter is a closure, it keeps count alive in its backpack.