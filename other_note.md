## 可能可行

#### JS

**基礎**

1. 型別

> [你不可不知的 JavaScript 二三事#Day3：資料型態的夢魘——動態型別加弱型別](https://ithelp.ithome.com.tw/articles/10202260)

```javascript
// JavaScript是一個弱型別的程式語言

// 強型別EX：C#(靜態)、Java(靜態)、Python(動態)
// 弱型別EX：JavaScript(動態)、PHP(動態)、C(靜態)、C++(靜態)

// 原本學的開始寫js可能會覺得很麻煩，因為太自由了允許程式碼隨便亂寫，所以很難debug
// 強型別的宣告變數，會指定這個變數要裝什麼，像是只能裝數值或只能裝字串，一旦宣告了他就永遠只能裝你規定的這種資料
// 弱型別雖然不一定都像js一樣自由到可以隨時改變變數裡面要裝的東西，剛剛宣告這個箱子裡裝的是黃金下一行馬上就變成裝毛巾，
// 但是弱型別程式語言都至少會有某種方式可以改變變數型態
```

2. 記憶體

> [透過複製陣列理解 JS 的淺拷貝與深拷貝 - JavaScript](https://askie.today/javascript-deep-copy-swallow-copy/)

```js
// 宣告一個變數就是去記憶體那邊開闢一塊空間給這個變數存資料，可以想像成去公家單位登記一塊土地的感覺
// 結合型別來看，強型別就像你登記了一塊農地，這塊地永遠都只能拿來種東西
// 弱型別就像你雖然登記了這塊是農地，但ㄓ你還是可以用這塊地蓋百貨公司

// 淺拷貝：共用同一塊記憶體
// 身拷貝：分出不同塊記憶體
```



**return**

```js
let personA = doWhat('nothing'); // personA = 'do nothing'

function doWhat(something){
  if(something === "nothing"){
    return 'do nothing'
  }
  console.log(`do ${something}`); 
}

// return之後就不會繼續執行下面的程式碼了
// 所以如果傳進來的參數 something 的值為 "nothing"，符合 if 條件，那麼下面的console就不會被執行
// 只有當傳進來的 something 不是 'nothing' 的時候，才會繼續執行下面的console

// return就像你得出了結論並告訴問你問題的人(呼叫function的人)，你把結論告訴他的他就把結論拿去用了，沒有人會繼續看結論下面還有什麼
// 範例中符合if條件的話會return一個字串
// 因為return這種丟結論出去之後、下面的程式碼就不會繼續被執行的特性，我們很常用來中斷function
// 如果不符合什麼條件的話就return，符合的話才繼續執行接下來的動作

let personB = doWhat2('shopping');

function doWhat2(something){
  if(something === 'nothing'){
    return 'do nothing'
  }
  return `do ${something}`
}
```

**ES6**

```js
// `${}`用法
// 可以做一個練習
let whoList = ['我', '隔壁阿姨', '王老先生', '工讀生'];
let whereList = ['家裡', '路上', '天堂', '地獄', '太空船'];
let actionList = ['吃麥當勞', '寫程式', '學習JS', '追直播'];

function getRandomItem(list){
  // Math.floor: 小於等於所給數字的最大整數
  // EX: Math.floor(5.99) => 5
  // EX: Math.floor(-5.01) => -6
  let index = Math.floor(Math.random()*list.length);
  return list[index];
}

function makeSentence(){
  let who = getRandomItem(whoList);
  let where = getRandomItem(whereList);
	let action = getRandomItem(actionList);
	alert(`${who}在${where}${action}`)
}
```

