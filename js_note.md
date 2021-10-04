# 複製Object - 深拷貝

> 應用場景：使用物件儲存資料時，為了判斷資料是否被更動過，有不能更動的A(異動前資料)、和可以被更動的B
>
> 程式區塊範例是用在vue專案中的情況

需要將 A 物件的值複製給 B 物件時不能直接 `this.B = this.A` 或 `this.B = {...this.A}`

上述兩種方式都是**淺拷貝**，因為指向同一塊記憶體，在vue中會導致只用v-model綁定了 B、並只對 B 進行操作，但 A 的值會跟著被更動

==解決方式==：`this.B = JSON.parse(JSON.stringify(this.A))` (深拷貝)

> **深拷貝**在複製物件時，會獨立出來不共用同一個記憶體位置，改動 `newObject` 時不會動到 `oldObject`。



# 判斷大小寫

```js
let text = 'A';

IsUpper(code) {
  return code === code.toUpperCase()
},
  
console.log(this.IsUpper(text)); // ture
```



# 判斷含有特定字串 indexOf

```js
let text = "there's something wrong";

console.log(text.indexOf("something") >= 0); // true
```



# 取代特定字串 replace

取代第一個找到的字串

```js
let text = "there's something wrong";

text.replace("something", "hahaha");

console.log(text); //there's hahaha wrong
```

取代全部



# 分割字串 split

```js
let text = "A,B,C,D";

let list = text.split(",");

// list = ["A","B","C","D"]
```



