## Symbol ##

Symbol 是 javascript ES6 的一個新的型別, 咱們可以用下面的 code 來看一下~

```js

var s = Symbol()
console.log(typeof s)
/*
    會得到 symbol, 表示symbol真的是一個型別,  不是 object , 也不是 function
*/
```
注意喔, 直至目前(2018/04/02)為止, <span style="color: red; font-weight: bold">IE 系列的瀏覽器都還沒有支援 Symbol</span> , 看來是不會支援了啦, 所以要用 Symbol 基本上就要透過 babel 等 Polyfill 的 compiler 幫忙轉譯一下變成 ES5 的語法嚕~

從上面的 code 可以看到, 當我們在宣告變數是一個 Symbol 型別的時候, 我們並不會用到 new 這個關鍵字, 但是我們卻會用到成對的小括弧 () 喔~

symbol 本身是一個用來建立 unique identifier 的類型, 但是我們卻無法得知他的 unique identifier 值是什麼。來看一下 symbol 的一些特性吧~

```js
var s = Symbol('Peppa')
console.log(s.toString())
/*
    得到  Symbol(Peppa)
*/

var s2 = Symbol('Peppa')
console.log(s === s2)
/*
    得到 false , 此舉證明 symbol 都是 unique 的唷
*/

var s3 = Symbol.for('DaddyPig')
var s4 = Symbol.for('DaddyPig')
console.log(s3 === s4)
/*
    得到 true , 因為 symbol.for 會在 symbol 不存在時幫忙產生一個新的, 不然就是回傳該 symbol
*/

let s = Symbol.for('MommyPig')
let description = Symbol.keyFor(s)
console.log(description)
/*
    得到 MommyPig , Symbol.keyFor 會回傳我們在建立 Symbol 時的傳入值, 姑且就叫他 key ?
*/
```
從上面的例子簡單看出, symbol 就是一個 unique 的東西存在於系統之中, 雖然利用同樣的字串傳入建立 symbol , 但是其指向不同的 symbol ; 我們可以透過 Symbol.for 去找到有同樣 key 的 symbol , 也可以透過 Symbol.keyFor 來得知該 symbol 的 key , 但是最重要的一點,  我們一就是無法得到該 symbol 的識別值, 也就是他獨一無二的 ID 到底是啥~(神秘唷唷唷唷唷~~)

symbol 還可以用在神奇的地方唷~只要是有地方想要應用到"獨一無二", "唯一的", 也許在我們內心都可以稍稍考慮一下使用 symbol 這個型別~

接下來看一下 symbol的一些應用~

```js
let Pig = {
    title: 'Piggy',
    [Symbol.for('BigNose')]: 'oink'
}

let bigNose = Pig[Symbol.for('BigNose')]
console.log(bigNose)
/*
    得到 oink , 可以將 symbol 應用在 object 的屬性建立唷~
*/

console.log(Object.getOwnPropertyNames(Pig))
/*
    得到 ['title'] , 挖哩, 用 symbol 所建立的屬性是無法被列舉的喔~
*/

console.log(Object.getOwnPropertySymbols(Pig))
/*
    得到 [Symbol(BigNose)] ,  Object.getOwnPropertySymbols 是在ES6中心的 method , 我想用意就是在可以觀察一下有哪些屬性是用 symbol 建立的囉
*/
```