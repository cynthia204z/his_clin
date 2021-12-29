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



# 紀錄

```vue
<template>
  <div :class="prefixCls">
    <quill-editor
      ref="myQuillEditor"
      v-model="content"
      :content="value"
      :options="editorOption"
      @blur="onEditorBlur($event)"
      @focus="onEditorFocus($event)"
      @ready="onEditorReady($event)"
      @change="onEditorChange($event)"
    />
  </div>
</template>

<script>
import { quillEditor } from 'vue-quill-editor'
import 'quill/dist/quill.core.css'
import 'quill/dist/quill.snow.css'

export default {
  name: 'JNPFQuill',
  components: { quillEditor },
  props: {

    prefixCls: {
      type: String,
      default: 'jnpf-editor-quill'
    },
    // 表單校驗用字段
    // eslint-disable-next-line
    value: {
      type: String
    },
    placeholder: {
      type: String,
      default: '請輸入內容...'
    }
  },
  data() {
    return {
      content: this.value,
      editorOption: {
        modules: {
          toolbar: [
            [{ size: ['small', false, 'large', 'huge'] }],
            // [{size:  ['10px', '12px', '14px','16px','18px','20px','24px','26px','32px','48px'] }],
            ['bold', 'italic', 'underline'],
            [{ color: [] }]
            // 加個font
          ],
          // keyboard: {
          //   bindings: {
          //
          //   }
          // }
        },
        theme: 'snow',
        placeholder: this.placeholder
      }
    }
  },
  computed: {
    editor() {
      return this.$refs.myQuillEditor.quill
    }
  },
  watch: {
    value(val) {
      this.content = val
    },
    placeholder(val) {
      this.$set(this.editorOption, 'placeholder', val)
    }
  },
  methods: {
    onEditorBlur(quill) {
      // console.log('editor blur!', quill)
    },
    onEditorFocus(quill) {
      // console.log('editor focus!', quill)
      this.$emit('editorFocus', quill)
    },
    onEditorReady(quill) {
      // console.log('editor ready!', quill)
      const THIS = this

      quill.keyboard.addBinding({key: '1', ctrlKey: true}, function(){
        THIS.$emit('handleKeyup', '1')
      })
      quill.keyboard.addBinding({key: '2', ctrlKey: true}, function(){
        THIS.$emit('handleKeyup', '2')
      })
      quill.keyboard.addBinding({key: '3', ctrlKey: true}, function(){
        THIS.$emit('handleKeyup', '3')
      })
      quill.keyboard.addBinding({key: '4', ctrlKey: true}, function(){
        THIS.$emit('handleKeyup', '4')
      })
      quill.keyboard.addBinding({key: '5', ctrlKey: true}, function(){
        THIS.$emit('handleKeyup', '5')
      })
      quill.keyboard.addBinding({key: '6', ctrlKey: true}, function(){
        THIS.$emit('handleKeyup', '6')
      })
      quill.keyboard.addBinding({key: '7', ctrlKey: true}, function(){
        THIS.$emit('handleKeyup', '7')
      })
      quill.keyboard.addBinding({key: '8', ctrlKey: true}, function(){
        THIS.$emit('handleKeyup', '8')
      })
      quill.keyboard.addBinding({key: '9', ctrlKey: true}, function(){
        THIS.$emit('handleKeyup', '9')
      })
      quill.keyboard.addBinding({key: '0', ctrlKey: true}, function(){
        THIS.$emit('handleKeyup', '0')
      })
    },
    onEditorChange({ quill, html, text }) {
      // console.log('editor change!', quill, html, text)
      // this.$emit('change', html)
      this.$emit('input', this.content)
      // let text = this.$refs.myQuillEditor.quill.getText();
      this.$emit('pureText', text)
    },
  }
}
</script>
<style lang="scss" scoped>
.jnpf-editor-quill {
  >>> .ql-editor {
    min-height: 400px;
  }
  >>> .ql-toolbar.ql-snow {
    border: 1px solid #dcdfe6;
    border-bottom: 0;
    border-radius: 4px 4px 0 0;
    padding: 0;
  }
  >>> .ql-container.ql-snow {
    border: 1px solid #dcdfe6;
    border-radius: 0 0 4px 4px;
  }
}
</style>

```

