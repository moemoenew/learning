## 今天學到的新東西-Vue Router

最近在做一個Single Page Application, 順道學習了一下Vue-Router, 覺得需要筆記一下。

**Install**

因為我本身在NodeJS專案中使用，所以理當是用npm來執行安裝vue-router囉!

```
npm install vue-router@版本號 --save
```

這時候就把vue-router安裝上來嚕~

**Start**

在開始使用vue-router,必須先建立一個js檔案來作為vue-router的設定檔，通常我會把這個檔案叫做router.js，然後開始在裡面進行vue-router的設定。

在這個設定檔之中，我們必須先引入vue和vue-router

```javascript
Import Vue from 'vue'
Import VueRouter from 'vue-router'
```

**Plugin**

vue-router本身應該是屬於Vue的一個plugin功能，所以當你在開始使用vue-router的時候，都要先掛載到Vue底下才行囉。

```javascript
Vue.use(VueRouter)
```

使用Vue.use方法去掛載VueRouter, 這樣就OK囉，可以開始進行vue-router的設定啦~

**Config**

當要開始使用vue-router時，當然就要建構這個instance囉~ 然後vue-router的建構涵式之中就要開始進行設定啦~

```javascript
const router = new VueRouter({
  //開始進行設定
})
```

在vue-router之中，最重要的當然是告訴Vue，我應該怎麼去根據url的設定來做頁面的導向，所以vue-router中有一個很重要的屬性就是routes。routes本身是一個array型態，也就是說你可以根據傳入的url去分別做判斷該導去哪一頁，當然在我的Single Page Application中就是要載入哪一塊的內容囉。

你可以像以下設定方式分別針對Home, About, Login三個頁面進行設定，從我寫的這三種連結也可以名稱也可以大概知道，vue-router設定會蠻常出現在我們網頁的Header區塊的呀~

```javascript
const router = new VueRouter({
  routes: [
    {
      path: '/Home',
      component: './theme/Home.vue'
    },
    {
      path: '/About',
      component: './theme/About.vue'
    },
    {
      path: '/Login',
      component: './theme/Login.vue'
    }
  ]
})
```

從上面的程式碼我想大概就可以略知一二，我在routes屬性中加入了三個object，分別都有兩個屬性:path和component，path理所當然是在url中所選定要導向的子頁面；component就是我希望在這一個頁面中所呈現載入的內容(都是來自於theme資料夾底下的vue檔案)。

然而，要透過這樣的方式去使用vue-router依據不同的url來變動內容，相對的在整個頁面layout的那個vue檔案裡面也要有相對應的改動，基本上就是運用router-view這個tag來完成。程式碼範例就像是這樣：

`Layout.vue`
```HTML
<template>
  <div>
    <router-view></router-view> Home/About/Login.vue內容會隨url嵌入在這裡
  </div>
</template>
```
