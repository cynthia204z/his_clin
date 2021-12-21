# Clin-Quill 簡易富文本組件

> ※ 若需要更多功能請使用 **JNPFQuill**

![image-20210810152459538](https://raw.githubusercontent.com/cynthia204z/mybed1/master/img/clinquill.png)



```vue
<Clin-Quill
	v-model="data.plan"
	placeholder="請輸入內容..."
	@pureText="getPlanText"
	@editorFocus="editorFocus"
></Clin-Quill>
```

> v-model綁定的內容是包含標籤的文字

`pureText`： 取得純文字

`editorFocus`：focus富文本框時，傳出event(quill)



## 在游標位置插入文字片段

```js
export default {
  data() {
    return{
      quill: undefined,
      quillIndex: undefined,
    }
  },
  methods: {
    editorFocus(quill) {
      // 取得當前富文本編輯器
      this.quill = quill
      // 取得游標位置
      this.quillIndex = this.quill.selection.savedRange.index;
    },
    addText() {
      // 在游標位置插入文字
      this.quill.insertText(this.quillIndex, 'text content', true);
    }
  },
}
```

![image-20210810152459538](https://raw.githubusercontent.com/cynthia204z/mybed1/master/img/1635130180916.gif)