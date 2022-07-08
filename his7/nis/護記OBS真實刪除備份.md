NisPatFocusSheetADGTable

```js
// 刪除
deleteRow() {
  let delList = [this.currentRow]
  if (this.currentRow.children && this.currentRow.children.length) {
    delList = [...delList, ...this.currentRow.children]
  }
  let obsTransIdDelList = delList.map(delRow => delRow.obsTransId)
  // 判斷是否所有紀錄皆為當前使用者建立
  let isRec = delList.every(delRow => delRow.focusRecorder === this.userInfo.userAccount)
  if (isRec) {
    // 刪除焦點紀錄主檔
    let delIdList = delList.map(delRow => delRow.id)
    console.warn(delIdList)
    postData(uiDeletePatFocusItem, delIdList).then(res => {
      this.showMsgAndRefresh(res.msg)
    })
    delRows(NisPatFocusSheet, delIdList).then(focusRes => {
      // 刪除OBS表單
      this.delMultipleObsData(obsTransIdDelList).then(obsRes => {
        console.warn('obsRes', obsRes)
        this.showMsgAndRefresh(focusRes.msg)
      })
    })
  } else {
    this.$alert('刪除的護理紀錄中，包含非您所寫的紀錄，不可刪除！')
  }
}
// 刪除OBS表單
delMultipleObsData(obsTransIdDelList) {
  return new Promise(async(resolve) => {
    let deleteDataForLoop = async() => {
      for (let transId of obsTransIdDelList) {
        await this.deleteObsByTransId(transId)
      }
    }
    await deleteDataForLoop().then((res) => {
      resolve(res)
    })
  })
}
deleteObsByTransId(transId) {
  return new Promise(resolve => {
    deleteTransdtl(transId).then(resDtl => {
      deleteTransmst(transId).then(resMst => {
        resolve([resMst, resDtl])
      })
    })
  })
}
```

