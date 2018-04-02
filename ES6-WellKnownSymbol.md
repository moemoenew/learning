## Wellknown Symbol ##

除了自行將 symbol 作為 object 的屬性名稱之外, 還有一些 javacript ES6 內建的 symbol 就稱之為 well-know symbol, 大家可以去 MDN site 查詢一下相關的一些應用 (https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Symbol)

看幾個範例囉~

### Symbol.toStringTag ###
```js
let Pig = function() {

}

Pig.prototype[System.toStringTag] = 'oink'
let Peppa = new Pig()
console.log(Peppa.toString())

/*
    得到 [object oink] , 通常若我們不執行 Pig.prototype[Symbol.toStringTag] 則會得到 [object Object]
    所以我們可以透過 Symbol.toStringTag 將 toString 方法回傳給我們的訊息的後半部做修改唷~
*/
```

### Symbol.isConcatSpreadable ###
```js
let values = [8, 10, 12]
console.log([].concat(values))
/*
    得到 [8, 10, 12]
*/

values[Symbol.isConcatSpreadable] = false
console.log([].concat(values))

/*
    得到 [[8, 10, 12]] , Symbol.isConcatSpreadable 被我們設定為 false 了, 造成 array.concat 無法有效的將 values 這個 array 裡面的元素一個一個建立到空的 array 裡面, 反而是將整個 values 當成他的第一個元素, 造成了巢狀 array 囉
*/
```

### Symbol.toPrimitive
```js
let values = [8, 10, 12]
let sum = values + 100
console.log(sum)

/*
    得到 8,10,12100 這個字串
*/

values[Symbol.toPrimitive] = function(hint) {
    return 55
}
let sum2 = values + 100
console.log (sum2)

/*
    得到 155, 我們可以視為 Symbol.toPrimitive 給了 values 這個 array 一個值讓其可以跟 100 進行相加
*/

```