## 新玩意兒-Axios ##

Axios這個玩意兒,主要是用來跟WebAPI要資料的嚕。
一般來說要透過連接資料來源端的WebAPI,古老的方法就是用XMLHttpRequest來做。但是時代在變,技術也一直再進步,現在大家都用其他的Library來做這個工作啦,相對下的語法也就簡單多惹。

要透過Axios這玩意兒來接資料,首先當然也是先安裝一下嚕。

```
npm install axios@版本號 --save
```

安裝完成之後,就可以開始引入使用嚕。
通常來說,我們會建立一個app.service.js來做axios的相關設定,其他地方要引用的時候,再把它給import進來就好。

首先,你可以先設定一下要連接對口端的主網域是啥,像是這樣：
```javascript
Import axios from 'axios'

axios.defaults.baseURL('https://api.abcde.com.tw')
```

再來就是可以開始去要資料啦！通常來說,因為我們要將這個module提供給別人去import,所以我們會將相關去要資料的method通通包在一個object裡面再export出去,這樣import的人就可以直接引用方法來獲取資料,像是這樣：

```javascript
//這是app.service.js

const appService = {
  //裡面一堆方法透過axios去跟對方要資料
  methodA () { .... },
  methodB () { .... }
}

export default appService
===========================================
//這是要接資料應用的
import appService from 'app.service.js'

let data = appService.methodA()
//這樣就把資料接到data變數裡面啦
//但是當然沒這麼簡單啦,這只是使用示意
```

然而要透過axios去獲取資料,就要用它的get方法嚕。在使用get方法的同時,由於它本身是一個promise,所以就要設定promise的instance給它唷！

整個在取資料的app.service和呼叫取資料的前端大概會長成下面這樣子:

```javascript
import axios from 'axios'

asiox.defaults.baseURL('https://api.abcde.com.tw')

const appService = {
  methodA () {
    //回傳一個promise給呼叫端, 讓他可以繼續針對回傳的data做處理
    return new Promise((resolve, reject) => {
      axios.get('取資料的WebAPI路徑')
        .then(response => {
          //取得資料成功的話,用resolve處理回傳的資料
          resolve(response.data)
        })
        .catch(response => {
          //取資料失敗的話,用reject處理回傳的status
          reject(response.status)
        })
    })
  }
}

export default appService
===============================================================
import appService from 'app.service.js'

callAppServiceMethodA () {
  appService.methodA()
    .then((data) => {
      //針對回傳的data做處理
    })
    .catch(() => {
      //針對取資料失敗做處理
    })
}

```
