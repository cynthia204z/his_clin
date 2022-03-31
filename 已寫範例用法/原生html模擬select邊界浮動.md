ueditor select解決辦法

```js
// 取到ueditor iframe中的document
this.editor.window.document.addEventListener("click", (e)=>{
  if(e.target.className.indexOf('oak-field') !== -1){
    selectElOnClick(e, this.editor.window.document)
  }
})

// 一般狀況就用document就好，function也不用傳editorDocument參數
document.addEventListener("click", (e)=>{
  if(e.target.className.indexOf('oak-field') !== -1){
    selectElOnClick(e)
  }
})
```

```js
export function selectElOnClick(e, editorDom) {
    // find select component by class
    let selectInputEl = e.target


    // reset position, height of select component
    let type = selectInputEl.parentElement.getAttribute('oakplugin')
    if(type === 'select'){
        let docBCR = editorDom.body.getBoundingClientRect();
        resetSltMenuPosition(docBCR, selectInputEl);
    }
}

function resetSltMenuPosition(docBCR, selectInputEl) {
    let sltInputBCR = selectInputEl.getBoundingClientRect();

    // 觸發事件時，下拉框的子元素選單還沒渲染，直接使用觸發事件當下取得的target會選不到
    // 先往上選一層(parentElement)確保可以往下選到打開的下拉選單
    // .oak-field > .oak-select-root > .oak-select-content > .oak-select
    let newSelectInputEl = selectInputEl.parentElement.lastChild
    let sltMenuEl = newSelectInputEl.firstChild.firstChild;

    // 下拉框高
    let inputHeight = sltInputBCR.height;
    // 選單展開總高
    let menuHeight = sltMenuEl.children.length * 20;
    // 下拉框上緣到body底部空間 (body高 - 下拉框上緣到body頂部空間)
    let bottomSpace = docBCR.height - sltInputBCR.top;
    // 下拉框下緣到body頂部空間 (下拉框上緣到body頂部空間 + 下拉框高)
    let topSpace = sltInputBCR.top + inputHeight;

    let maxH, top;


    // 下拉框到body底部空間 > 選單高度
    if (bottomSpace > menuHeight) {
        maxH = bottomSpace;
        top = 0;
        // console.log(`1`)
    }
    // 下拉框到body頂部空間 > 選單高度
    else if (topSpace > menuHeight) {
        maxH = topSpace;
        top = -menuHeight + inputHeight;
        // console.log(`2`)
    }
    // 選單長度 > 上下空間：
    else {
        // topSpace bigger
        if (topSpace > bottomSpace) {
            maxH = topSpace;
            top = -topSpace + inputHeight;
            // console.log(`3`)
        }
        // bottomSpace bigger
        else {
            maxH = bottomSpace;
            top = 0;
            // console.log(`4`)
        }
    }


    sltMenuEl.style.overflowX = 'hidden'
    sltMenuEl.style.overflowY = 'auto'
    sltMenuEl.style.maxHeight = `${maxH - 8}px`
    sltMenuEl.style.top = `${top}px`
}

```

