# JavaScript Note

## 複製Object - 深拷貝

> 應用場景：使用物件儲存資料時，為了判斷資料是否被更動過，有不能更動的A(異動前資料)、和可以被更動的B
>
> 程式區塊範例是用在vue專案中的情況

需要將 A 物件的值複製給 B 物件時不能直接 `this.B = this.A` 或 `this.B = {...this.A}`

上述兩種方式都是**淺拷貝**，因為指向同一塊記憶體，在vue中會導致只用v-model綁定了 B、並只對 B 進行操作，但 A 的值會跟著被更動

<b style="color:orange">解決方式</b>：`this.B = JSON.parse(JSON.stringify(this.A))` (深拷貝)

> **深拷貝**在複製物件時，會獨立出來不共用同一個記憶體位置，改動 `newObject` 時不會動到 `oldObject`。



## 判斷大小寫

```js
let text = 'A';

IsUpper(code) {
  return code === code.toUpperCase()
},
  
console.log(this.IsUpper(text)); // ture
```



## 判斷含有特定字串 indexOf

```js
let text = "there's something wrong";

console.log(text.indexOf("something") >= 0); // true
```



## 取代特定字串 replace

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



## 分割字串 split

String to Array

```js
let text = "A,B,C,D";

let list1 = text.split(",");
// list1 = ["A","B","C","D"]

let list2 = text.split("");
// list2 = ["A", ",", "B", ",", "C", ",", "D"]
```



## 合併字串 join

Array to String

```js
let arr = ["A","B","C","D"];

let str1 = arr.join("、");
// str1 = "A、B、C、D"

let str2 = arr.join("");
// str2 = "ABCD"
```



## 擷取字串/陣列 slice

```js
let fruits = ['Banana', 'Orange', 'Lemon', 'Apple', 'Mango'];

let citrus1 = fruits.slice(1, 3);
// citrus1 = ['Orange','Lemon']
```



## 比較2個陣列

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

   ```
   let C = A.filter(x => !B.includes(x))
   ```

3. **聯集**

   ```js
   let C = new Set([...A, ...B])
   ```

   

## 刪除/取代陣列元素 splice

`arr.splice(index, 刪除的數量, 取代成)`

```js
let arr = ["A", "B", "C"]

arr.splice(1, 1, "❤")
// arr = ["A", "❤", "C"]

arr.splice(1, 0, "◼", "✔")
// arr = ["A", "◼", "✔", "❤", "C"]

arr.aplice(2, 2, "♠♣♦♥")
// arr = ["A", "◼", "♠♣♦♥", "C"]
```



## 排序

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



## 陣列元素交換順序

```js
let arr = ["A", "B", "C"];

[arr[1], arr[0]] = [arr[0], arr[1]];
// arr = ["B", "A", "C"]
```



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



## 相減計算單位

```js
//單位：'years', 'months', 'weeks', 'days', 'hours', 'minutes', 'seconds'

let monthCount = moment(後面的時間).diff(moment(前面的時間), 單位)
```
