# JavaScript Note

## 基本用法

### 複製Object - 深拷貝

> 應用場景：使用物件儲存資料時，為了判斷資料是否被更動過，有不能更動的A(異動前資料)、和可以被更動的B
>
> 程式區塊範例是用在vue專案中的情況

需要將 A 物件的值複製給 B 物件時不能直接 `this.B = this.A` 或 `this.B = {...this.A}`

上述兩種方式都是**淺拷貝**，因為指向同一塊記憶體，在vue中會導致只用v-model綁定了 B、並只對 B 進行操作，但 A 的值會跟著被更動

<b style="color:orange">解決方式</b>：`this.B = JSON.parse(JSON.stringify(this.A))` (深拷貝)

> **深拷貝**在複製物件時，會獨立出來不共用同一個記憶體位置，改動 `newObject` 時不會動到 `oldObject`。



### 判斷大小寫

```js
let text = 'A';

IsUpper(code) {
  return code === code.toUpperCase()
},
  
console.log(this.IsUpper(text)); // ture
```



### 判斷含有特定字串 indexOf

```js
let text = "there's something wrong";

console.log(text.indexOf("something") >= 0); // true
```



### 取代特定字串 replace

取代第一個找到的字串

```js
let text = "there's something wrong";

text.replace("something", "hahaha");

console.log(text); //there's hahaha wrong
```

取代全部

```js
// 取代字串
val = val.replace(/被取代的文字/g, '新的文字')

// 取代換行符號=換行標籤
val = val.replace(/\n/g, '<br>')
```



### 分割字串 split

String to Array

```js
let text = "A,B,C,D";

let list1 = text.split(",");
// list1 = ["A","B","C","D"]

let list2 = text.split("");
// list2 = ["A", ",", "B", ",", "C", ",", "D"]
```



### 合併字串 join

Array to String

```js
let arr = ["A","B","C","D"];

let str1 = arr.join("、");
// str1 = "A、B、C、D"

let str2 = arr.join("");
// str2 = "ABCD"
```



### 擷取字串/陣列 slice

```js
let fruits = ['Banana', 'Orange', 'Lemon', 'Apple', 'Mango'];

let citrus1 = fruits.slice(1, 3);
// citrus1 = ['Orange','Lemon']
```



### 比較2個陣列

> C 是一個陣列

1. **交集**

   A和B的交集，取出A資料中包含與B資料內相同的資料

   ```js
   // 1.
   let C = A.filter(x => B.includes(x))
   
   // 2.
   let C = new Set([...A].filter(x ))
   ```

2. **差集**

   A和B的差集，取出A資料中不包含與B資料內相同的資料

   ```js
   let C = A.filter(x => !B.includes(x))
   ```

3. **聯集**

   ```js
   let C = new Set([...A, ...B])
   ```

   

### 刪除/取代陣列元素 splice

`arr.splice(index, 刪除的數量, 取代成)`

```js
let arr = ["A", "B", "C"]

arr.splice(1, 1, "❤")
// arr = ["A", "❤", "C"]
// 第1個索引位置刪除1個元素，並插入❤

arr.splice(1, 0, "ㄅ", "ㄆ")
// arr = ["A", "ㄅ", "ㄆ", "❤", "C"]
// 第1個索引位置刪除0個元素，並插入ㄅ、ㄆ

arr.aplice(2, 2, "♠♣♦♥")
// arr = ["A", "ㄅ", "♠♣♦♥", "C"]
// 第2個索引位置刪除2個元素，並插入♠♣♦♥
```



### 排序

一般

```js
list.sort(function(a, b) {
  return a[columnName] - b[columnName]
})
```

依照別的陣列順序排序

```js
referenceList.forEach((i, index) => {
  arr.forEach((a, aIndex) => {
    if (i === a) {
      arr.splice(aIndex, 1)
      arr.splice(index, 0, a)
    }
  })
})
```

中文排序

```js
list.sort(function(a, b) {
	return a[columnName].localeCompare(b[columnName], 'zh-TW')
})
```



### 陣列元素交換順序

```js
let arr = ["A", "B", "C"];

[arr[1], arr[0]] = [arr[0], arr[1]];
// arr = ["B", "A", "C"]
```



### 鍵盤事件

> keyCode，例： `keyCode === 46` 這種用法已經被棄用了，要避免使用。

```js
textarea.addEventListener('keydown', (e) => {
  if(e.key === 'Delete'){
    //do something when 'Delete'
  }
  if(e.key === 'z' && e.ctrlKey){
    //do something when 'ctrl+Z'
  }
});
```

```js
document.onkeydown = (e) => {
  // e.key
}
```



<<<<<<< HEAD
### 迴圈等非同步結束

```js
function 方法名 () {
  return new Promise(resolve => {
    調用非同步方法.then(參數=>{
      // do something
      resolve();
    })
  })
}

fot(let i = 0; i < list.length; i++) {
  await 方法名().then(()=>{
    if(i === list.length - 1){
      //do something
    }
  })
}
```

非同步**照順序**等回傳資料

```js
var resultData = [];
(function fetchData(i){
  // 處理 i跟非同步方法的關係
  非同步方法.then(res=>{
    resultData.push(res);
    if(i < list.length){
      fetchData(i+1);
    } else {
      // do something after get all 非同步方法's res
    }
  });
})(1);
// ------
var resultData = [];
function fetchData(i){
  // 處理i跟非同步方法的關係
  非同步方法.then(res=>{
    resultData.push(res);
    if(i < list.length){
      fetchData(i+1);
    } else {
      // do something after get all 非同步方法's res
    }
  });
}
fetchData(1);
```





=======
>>>>>>> cc0ab948af083fd1ef2fd5f6c9e2608a820fdf69
## 程式碼優化

### if else替代方法

> 參考文章：
>
> [徹底消除if else， 讓你的代碼看起來更優雅](https://juejin.cn/post/6882390231715151879)

1. **map**: function

   > 在Map集合中，get一個不存在的值，不會拋出異常，獲得的返回值為null。

   原本使用if else時

   ```js
   if(type === '1'){
     arr.push(item)
   }else if(type === '2'){
      FuncA(item)
   }else if(type === '3'){
     if(item === 'A'){ 
       FuncB()
     }
   }else if(type === '4'){
     FuncC()
   }else{
     /*do something*/
   }
   ```

   改成

   ```js
   let actions = new Map([
     ['type1', (item)=>{ arr.push(item) }],
     ['type2', (item)=>{ FuncA(item) }],
     ['type3', (item)=>{ if(item === 'A'){ FuncB() } }],
     ['type4', ()=>{ FuncC() }]
     ['default', ()=>{/*do something*/}],
   ])
   let action = actions.get(`type${type}`) || actions.get('default')
   action(item)
   ```

   **map**: string

   原本使用if else時

   ```js
   if(pathType === 'C'){
     return 'yellow'
   }else if(pathType === 'K'){
     return 'pink'
   }else if(pathType === 'W'){
     return 'blue'
   }
   ```

   改成

   ```js
   let colorMap = new Map([
     ['C', 'yellow'],
     ['K', 'pink'],
     ['W', 'blue'],
   ])
   return colorMap.get(pathType)
   ```

   

2. **Object**

   原本使用if else時

   ```js
   if(actionType === 'goto'){
     if(status === '1'){
       FuncA()
     }else if(status === '2'){
       FuncB()
     }
   }else if(actionType === 'backto'){
     if(status === '2'){
       FuncC()
     }else if(status === '3'){
       FuncD()
     }
   }else{
     /*do something*/
   }
   ```

   改成

   ```js
   let actions = {
     'goto1': ()=>{ FuncA() },
     'goto2': ()=>{ FuncB() },
     'backto2': ()=> { FuncC() },
     'backto3': ()=> { FuncD() },
     'default':()=>{/*do something*/}
   }
   let action = actions[`${actionType}${status}`] || actions['default']
   action()
   ```

   


### for迴圈: i of arr替代arr.length

原

```js
for (let i = 0; i < arr.length; i++){
  console.log(arr[i])
}
```

改

```js
for (let i of arr){
  console.log(i)
}
```



<<<<<<< HEAD
## 其他

### 隨機HEX色碼

```js
function getRandomColor() {
  var letters = '0123456789ABCDEF'.split('');
  var color = '#';
  for (var i = 0; i < 6; i++ ) {
    color += letters[Math.floor(Math.random() * 16)];
  }
  return color;
}
```



=======
>>>>>>> cc0ab948af083fd1ef2fd5f6c9e2608a820fdf69
# Moment.js Note

## 半年前

```js
let halfAYear = moment(new Date()).subtract(6, 'months').format('YYYY-MM-DD')
```



## 上/下個月

```js
let currentDate = moment().format('YYYY-MM-DD') //當天

let aMonthLater = moment(currentDate).month(1).format('YYYY-MM-DD') //下個月同日
let aMonthAgo = moment(currentDate).month(-1).format('YYYY-MM-DD') //上個月同日
```



## 月初、月底

```js
let currentMonth = moment().format('YYYY-MM') //當月

let startDate = moment(currentMonth).startOf('month').format('YYYY-MM-DD') //當月月初
let endDate = moment(currentMonth).endOf('month').format('YYYY-MM-DD') //當月月底
```



## 一天的頭尾

```js
let startTime = moment().startOf('day').format('YYYY-MM-DD HH:mm') // xxxx-xx-xx 00:00
let endTime = moment().endOf('day').format('YYYY-MM-DD HH:mm') //xxxx-xx-xx 2
```



## 相減計算單位

```js
//單位：'years', 'months', 'weeks', 'days', 'hours', 'minutes', 'seconds'

let monthCount = moment(後面的時間).diff(moment(前面的時間), 單位)
```
