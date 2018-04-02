## Object Extension ##

### Object.setPrototypeOf, Object.assign ###
當我們想要一個物件 a 同時也擁有物件 b 的屬性的時候, 可以選擇兩種方式去實現這個夢想: Object.setPrototypeOf 或 Object.assign

兩者在實現的方式上有一點點不一樣, Object.setPrototypeOf 是將被拷貝物件的屬性加到目標物件的 prototype (原型) 中; Object.assign 則是真的將屬性拷貝至物件的屬性去, 並非 prototype 中。有點讓人 confused 了, 看一下程式碼和 console.log 的結果應該就比較有感覺惹~

```js
let a = {
    x: 1
}

let b = {
    y: 4
}

Object.setPrototypeOf(a, b) //這時候會將 b 的屬性透過 prototype chain 一起傳到 a 去, 但是並非 a 的屬性中有 y , 而是 a 的 prototype 中有 y
console.log(a)
/*
    得到 { x: 1 } , 但是你可以看到 a 的 prototype 裡面有一個 y : 4
*/

console.log(a.__proto__)
/*
    得到 { y: 4 }
*/

console.log(a.y)
/*
    得到 4, 但不是因為 a 物件有 y 這個屬性, 而是因為 a 物件的 prototype 中有 y 這個屬性, 所以當物件屬性找不到的時候, 就會去找 prototype 看有沒有這個屬性, 如果 prototype 也沒有才結束; 如果有, 就秀出, 就像這個範例一樣秀出 4 這個值
*/

let c = {
    m: 10
}
let d = {
    n: 11
}

Object.assign(c, d)
console.log(c)
/*
    得到 { m: 10, n: 11 }, 所以 c 真的有 n 屬性了唷 
*/
```

### Object.defineProperty ###

```js
let a = { x: 1}, b = { y: 2, z: 3}

Object.defineProperty(b, 'w', {
    value: 4,
    enumerable : false
})

console.log(b.w)
/*
    得到: 4 , 表示 Object.defineProperty 幫我們在 b 物件中定義了 w 這個屬性
*/

let target = {}
Object.assign(target, a, b)
console.log(target)
/*
    得到 { X: 1, y: 2, Z: 3 }, 因為 w 屬性設定為 enumerable = false , 所以他不會被 Object.assign 加到 target 中唷!!
*/

console.log(target.w)
/*
    得到: undefined
*/

```