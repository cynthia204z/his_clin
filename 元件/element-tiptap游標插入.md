# element-tiptap游標後插入文字

element-tiptap沒有提供此功能，以下為使用javascript達成目標功能的方法：

```vue
<Tiptap :content.sync="content"></Tiptap>
```

1. 設置currentRange、currentNode變數儲存游標選擇範圍、異動節點

   ```js
   data(){
     return {
       content: '', // 文本框綁定值
       currentRange: null, //游標選擇範圍
       currentNode: null //異動節點
     }
   }
   ```

2. 給富文本框加點擊事件、keyup事件

   ```js
   mounted() {
     const THIS = this
     setTimeout(()=>{
       // 取得tiptap富文本框底下實際可以編輯的子節點
       let textarea = document.getElementsByClassName('el-tiptap-editor__content')[0]
       let textareaInput = textarea.firstElementChild
   
       textareaInput.onclick = function() {
         // 獲取文件中選中區域
         THIS.currentRange = document.getSelection().getRangeAt(0)
         THIS.currentNode = document.createElement('p')
       }
       
       textareaInput.onkeyup = function() {
         // 獲取文件中選中區域
         THIS.currentRange = document.getSelection().getRangeAt(0)
       }
     }, 500)
   }
   ```

3. 觸發插入文字的事件時，將舊的選取範圍刪除，將新的內容插入節點

   如果沒有已記錄的游標位置就直接加在原文後面

   ```vue
   <el-button @click="insertText('someText')">插入文字</el-button>
   ```

   ```js
   insertText(newText){
     if (this.currentNode && this.currentRange) {
       // 選中區域替換文字
       this.currentNode.innerHTML = newText
       // 刪除選中區原內容
       this.currentRange.deleteContents()
       // 在游標處插入新節點
       this.currentRange.insertNode(this.currentNode)
       // 取消選取
       window.getSelection().empty()
       this.currentNode = null
       this.currentRange = null
     } else {
       if(this.content) {
         this.content += newText  
       } else {
         this.content = newText
       }
     }
   }
   ```
   
   

