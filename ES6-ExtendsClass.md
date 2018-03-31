## Extends Class ##

其實在 javascript 裡面的 extends 就是我們在c#中看到的 inherit 的概念啦~一個繼承的概念~
那甚麼是繼承, 簡單一點說就是...爸爸媽媽有什麼, 生下來的孩子就會有什麼...XD

總不會爸媽是小豬, 生下一隻小野狼吧? (很爛的解釋)
來看看 code 吧!!
```js
class DaddyPig {
    constructor () {
        console.log ('I\'m a pig')
    }
}

class PeppaPig extends DaddyPig {
    constructor () {
        super()
        console.log('I \'m Peppa')
    }
}

let peppa = new PeppaPig()

//將會得到 
//I'm a pig
//I'm Peppa
```

注意唷!! 在上面的範例中, 子物件 PeppaPig 建構式裡面的 super() 這一段, <span style='color:red; font-weight: bold;'>不可以省略!!!</span> 不然會出錯啊啊啊啊啊!!! (原因好像是因為當透過 extends 要去繼承 parent class 的時候, 在 javascript 實作的時候, 她必須知道要去哪裡 copy prototype , 也就是說在那個當下應該要有 parent class 的實體才行, 如果不設定這個就會讓 javascript 迷失了方向不知道去哪裡 copy 啊~)

讓我們再看看下一段code:
```js
class DaddyPig {
    constructor (name) {
        consolog.log(`My name is ${name}`)
    }
    play () {
        console.log('I can play basketball')
    }
}

class PeppaPig extends DaddyPig {
    
}

let peppa = new PeppaPig('peppa')
peppa.play()

//將會得到:
// My name is peppa
// I can play basketball
```

在上面這一段code裡面, 我們將 DaddyPig 的建構式加入的一個 parameter, 此外也在DaddyPig這個class中, 加入了一個 play() 的方法; 在 PeppaPig 的 class 中, 我們則將她的建構式給拿掉~

然後我們在建立 PeppaPig 物件的時候傳入 peppa 字串, 這樣自然而然的, 由於 PeppaPig 繼承自 DaddyPig , 而 PeppaPig 本身又沒有建構式, 所以她就跑去用了 DaddyPig 的建構式嚕~

此外在 DaddyPig 中所建立的 play 方法, 也可以因為 extends 的關係給繼承了下來, 所建立出來的 PeppaPig 物件實體也都有相同的方法可以用嚕~

那接下來看一下, 如果我在 PeppaPig 這個 class 中也有一個 play 的方法, 那會怎樣?
```js
class DaddyPig {
    constructor (name) {
        console.log(`My name is ${name}`)
    }
    play () {
        console.log('I can play basketball')
    }
}

class PeppaPig extends DaddyPig {
    play () {
        console.log('I like to play soccer!!')
    }
}

let peppa = new PeppaPig('peppa')
peppa.play()

//將會得到:
// My name is peppa
// I like to play soccer!!
```
嘿嘿, 答案就是, 會複寫 DaddyPig 的 play 方法, 在呼叫 peppa.play 時就用了 PeppaPig class 裡面的 play 方法囉~