## ES6 Modules and Classes ##

Modules 就是所謂的模組化啦~
當你將一整套的方法流程包裝成一個module, 這時候就可以被引用來執行各項任務, 不用到處都去寫一樣的code, 達到重複利用且一次性修改的好處, 當然也就利於我們管理自己的專案囉~


### Class ###

class關鍵字本質上就是一個syntax sugar，可以將其視為就是一個object的建構式, 透過new 關鍵字來將 object 生成

```javascript
class Task {}

console.log(typeof Task)
//得到 "function"

let task = new Task()
console.log(typeof taks)
//得到 "object"

console.log(taks instanceof Task)
//得到 "true"
```

當然我們不會想要建立一個完全空空的 object, 我們讓這個class具有一些方法可以呼叫執行吧!

```javascript
class Task {
    showContent () {
        // Do something....
    }
}

let task = new Task()
console.log(task.showContent === Task.prototype.showContent)
//得到 "true"
```
從上面的程式碼中可以看到, 原來我們的class關鍵字是一個建構object的function, 然後若是我們在class中加入function, 那就等於我們將其加入該class的prototype裡面去唷!!

接下來我們看一下使用class關鍵字時所要注意的一些事項:

1. 在class之中, 可以利用Constructor function來執行物件建置時所要處理的一些方法:
```javascript
class Task {
    constructor () {
        //建構式
        console.log('Task instance is created')
    }
}
```

2. 在建構式以及一般的物件方法之間, 不用放逗點~
```javascript
class Task{
    constructor () {
        ///建構式
    } //<- 注意這邊不需要有逗點
    methodA () {}
    methodB () {}
}
```

3. 在class中不可以直接設置變數, 若是像下面這樣在class裡面設置一個變數taskID, 則會導致syntax error....
```javascript
class Task {
    let taskID = 5000 // <= 不可以這樣用
    constructor () {
        console.log(taskID)
    }
}

let task = new Task()
```

4. class 在使用上是沒有 hoisting 機制的
```javascript
let task = new Task() // <= 錯誤!!

class Task {
    constructor () {
        //Do something...
    }
}
```