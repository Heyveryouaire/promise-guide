# Promise 

Promise is a object, use to do async things !

### Basic syntax :
```js
new Promise((resolve, reject) => {    
    // code here ..
    if(something){
        resolve("Done")
    }else{
        reject("Error")
    }
})
```

### Handling promise : 

```js
// Resolve will be run in then: 
.then(rep => console.log(rep))

// Reject will be run in catch
.catch(err => console.log(err))
```

## How to ? 
Wrap a functionnality in promise to make it asynchronous !

```js
// The function return message in specific time
function out(time, message) {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            resolve(message)
        }, time)
    })
}

out(1000, "1er")
.then(e => console.log(e))

out(3000, "2eme")
.then(e => console.log(e))

out(2000, "3eme")
.then(e => console.log(e))

```

```bash
1er
3eme
2eme
```

If you need to wait for 1 before 2 start, then 3, you can chain them !

```js
out(1000, "1er")
.then(e => {
    console.log(e)
})
.then(_ => {
    out(3000, "2eme")
    .then(e => {
        console.log(e)
    })
    .then(_ => {
        out(2000, "3eme")
        .then(e => {
            console.log(e)
        })
    })
})
// Pretty ugly ..
```

## Aync / Await 

We can make asynchronous code easier !

```js
// Frist, we need to wrap all code we need to be async in async function
async function main(){
    function out(time, message) {
        return new Promise((resolve, reject) => {
        setTimeout(() => {
            resolve(message)
        }, time)
    })
}

// and need the await keyword 
let first = await out(1000, "1er")
console.log(first)
let second = await out(3000, "2eme")
console.log(second)
let three = await out(2000, "3eme")
console.log(three)

}main()
```

```bash
1er
2eme
3eme
```

## What without promise ? 

```js
setTimeout(() => {
    console.log("1er")
}, 1000)
setTimeout(() => {
    console.log("2eme")
}, 3000)
setTimeout(() => {
    console.log("3eme")
}, 2000)
```

```bash
1er
3eme
2eme
```

*Very usefull if you need to wait to specific data before continue like, fetching data.*
