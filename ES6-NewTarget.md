## new.target ##

我們都知道 new 是一個 javascript 的關鍵字
他主要是讓我們用來建立一個 instance 的
就像是:

```js
function pig(name) {
    this.name = name
}

var Peppa = new pig()
```
這樣子 Peppa 本身就是 pig 的 instance 嚕~

那為啥關鍵字還會有屬性?
好難解釋啊~我們來看 code

首先先來看看 new.target 他本身時啥咪碗糕吧

```js
class Pig {
    constructor () {
        console.log(typeof new.target)
    }
}

var Peppa = new pig()
//這時候console.log會得到 "function"
```
從上面的例子看來, new.target 是一個 function 啊!!
那....他是代表哪一個 function ?

```js
class Pig {
    constructor () {
        console.log(new.target)
    }
}

var Peppa = new Pig()
/*這時候你會得到:
    construtor () {
        console.log(new.target)    
    }
*/
```
也就是說 new.target 指向的是 Pig 這個 class 的建構式
不過這樣看起來, 那 new.target 好像也不太有用處啊?
我們再來看看下面的例子:

```js
class Pig {
    constructor () {
        console.log(new.target)
    }
}

class PeppaPig extends Pig {

}

var Peppa = new PeppaPig()
/*這時候你會得到
    constructor (...args) {
        super(...args)
    }
*/
```
唷呼,這裡發生了幾件神奇的現象, 第一個是 new.target 指向的不再是 Pig 這個 class 的建構式, 反而是指向了另一個我們不知道的 constructor ...
再想想, 這個 constructor 裡面有呼叫 super() , 那可以想見的就是, 他應該是 Pig 這個 class 的繼承物件吧? 所以答案揭曉囉~這個 construtor 的主人就是透過 extends 去繼承 Pig 的 PeppaPig class 啦~

另一個奇妙的事情就是, 我們明明就沒有設定 PeppaPig 的建構式, 那哪來的 constructor 勒? 其實這就是 javascript 幫我們預設定的建構式啦, 你看不見, 不代表他不存在啊啊啊啊啊~ XD javascript 本身都還是會幫每個 class 建置一個預設的建構式的~

那那那...new.target還是只有這樣的功能嗎?
我們再來看下一個例子~

```js
class Pig {
    constructor () {
        new.target.play()
    }
}

class PeppaPig extends Pig {
    static play () {
        console.log('I like to play soccer!!')
    }
    sleep () {
        console.log('I also like to sleep~')
    }
}

var Peppa = new PeppaPig()
/*
這時候你就會得到　I like to play soccer!!
*/
```
喔喔~從這個例子就可以看出來, 我們是可以透過 new.target 去直接呼叫 PeppaPig 的 static (靜態)方法唷!! 但是要特別記得的是, 該方法一定要是 static 方法唷, 也就是說, 在上述的例子中, 如果你要用 new.target.sleep() 在 Pig 這個 class 的建構式中的話, 會錯滴~

sleep 方法只能用在 PeppaPig 的實體上, 也就是 Peppa.sleep() 才對唷~
