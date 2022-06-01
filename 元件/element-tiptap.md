# element-tiptap

extensions

  共用參數

```js
{ 
  buuble:氣泡菜單(反白時出現),
  menubar菜單欄 
}
```

  必要

```js
Doc() 參數{ title: 啟用標題模式(默認false), 為true需引入Title }
Paragraph()
Text()
ListItem() 工具列
```

工具列

```js
Heading({level: 6})  標題, 參數{ level: 1~6, 最高到六 }
Bold()  粗體
Underline()  底線
Italic()  斜體
Strike()  劃線
BulletList()  點點list
OrderedList()  數字list
Link()  網頁超連結
Image()  上傳圖片, 可由網址抓取or本地上傳, 參數{ urlPattern: 檢查url是否有效, uploadRequest: 自定義圖片上傳方法，方法應該返回Promise<url>, 默認返回圖像的base64數據 }
CodeBlock()  程式碼區塊
Blockquote()  程式碼備註
TodoList()  TodoList, 類似完成後畫線的checkBox
TodoItem()  Todo選項, 與TodoList一起使用
TextAlign()  對齊方式, 參數{ alignments: 對齊方式, 順序會影響菜單按鈕的渲染順序(默認['left', 'center', 'right', 'justify']) }
Indent()  類似tab的空格, 參數{ minIndent: 最小縮進, maxIndent: 最大縮進(每一縮進=30px) }
LineHeight()  參數{ lineHeights: 行高, 順序會影響菜單按鈕的渲染順序(默認['100%', '115%', '150%', '200%', '250%', '300%']) }
HorizontalRule()  水平分隔線
History()  上/下一步
Table({resizable: true})  插入表格 ,參數{ resizable: 表格單元格是否可以調整大小(默認false) }
TableHeader()  使用Table時必須同時啟用
TableCell()  使用Table時必須同時啟用
TableRow()  使用Table時必須同時啟用

FormatClear()  清除反白部分的樣式
TextColor()  字體顏色, 參數{ colors: 字體顏色(默認看https://github.com/Leecason/element-tiptap/blob/master/src/utils/color.ts#L6) }
TextHighlight()  字的背景顏色
Preview()  預覽
Print()  列印
Fullscreen()  全螢幕
SelectAll()  全選, 跟Ctrl+A功能一致
FontType()  字型, 參數{ fontTypes: 字體類型(默認{Arial,Arial Black,Georgia,Impact,Tahoma,Times New Roman,Verdana, Courier New,Lucida Console,Monaco,monospace})}
FontSize()  字體大小, 參數{ fontSizes: 字體大小(默認['8', '10', '12', '14', '16', '18', '20', '24', '30', '36', '48', '60', '72']) }
```

  不懂功能

```js
HardBreak()  看不懂是啥(
TrailingNode()  看不懂是啥(
```

  應該無法/不會使用

```js
Iframe()  上傳影片, 暫不可用=>報錯: 缺少template compiler
CodeView()  查看和編輯 HTML 源代碼的擴展, 需要下載codemirror, 參數{ codemirror:  codemirror library, codemirrorOptions: codemirror的選項 }
```



editorProperties (Object) 

> 可以直接控制編輯器行為, 供自定義編輯器使用

placeholder (String)

> 當編輯器為空時顯示placeholder

content (String)

> 可以使用:content="content"或v-model="content"綁定資料

output (String)

> 可選'html'或'json'(預設html)

readonly (Boolean)

> 預設false

spellcheck (Boolean)

> 是否開啟拼寫檢查, spellcheck插件的值

height/width (String | Number)

> 數字的預設單位為px

showMenubar (Boolean)

> 是否顯示工具列(預設為true)

charCounterCount (Boolean)

> 是否顯示計數器(預設為true)

tooltip (Boolean)

> hover時是否顯示按鈕名稱(預設為true)

lang (String)

> 預設為插件lang的值