HTML編輯器

1. 只讀模式的checkbox
https://share.vidyard.com/watch/LJVCpFKKhyyA86PQD4CfiD?

2. 數據庫有資料的checkbox和日期欄位UI沒有顯示
  https://share.vidyard.com/watch/jCL79LGb6eGX9fmhmw1uYL?

  > 原因是 getContent() 方法沒有把checkbox、radio的值寫進html

Vue組件

1. 沒勾選的checkbox被填入其他值
  https://share.vidyard.com/watch/27QotYu1uS6ZdBWAMHGCLY?

  in `src/components/EmrEditor/common/filetab.vue/saveTransDtl()`

2. 編輯模式存檔有時候會存到模板
  https://share.vidyard.com/watch/4dAA1e3Y5ux6o76SdnEo8t?

  in `src/components/EmrEditor/common/filetab.vue/saveDocument()`

3. 有長度限制的時候trans_dtl的儲存會被擋下來只儲存預設值，但trans_mst和sheet_def還是會被存到
  https://share.vidyard.com/watch/uapPU6toKQCtjxVqV7tTDZ?

  in `src/components/EmrEditor/common/filetab.vue/saveDocument()`

4. trans_mst和sheet_def被存到了，但trans_drl什麼都沒存
  https://share.vidyard.com/watch/88P23A8Ri4FLwq5tmhzqMY?