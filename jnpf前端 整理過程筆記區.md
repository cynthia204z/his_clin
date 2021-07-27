# 過濾器

> value 未知
> options = `[{"fullName":"失效","id":"Y"}]` 
> 最後回傳 ==["Y"]==
>
> options是陣列且有fullname
>
> ------
>
> ==設有id和value相同==
>
> 
>
> **value是陣列的狀況：**
> value可能長這樣 ["Y"]
> item = id等於value的options項目
> item可能是 0:{"fullName":"失效","id":"Y"}
> 最後應該回傳"失效"，單元格內顯示「失效」
>
> 
>
> **value不是陣列的狀況：**
> value可能長這樣 "Y"
> item = id等於value的options項目
> item可能是 0:{"fullName":"失效","id":"Y"}
> 最後應該回傳"失效"，單元格內顯示「失效」
>
> 
>
> **假設不成立**
>
> ------
>
> ==設沒有id和value相同==
>
> 
>
> **value不是陣列的狀況：**
> value可能長這樣 '["Y"]'
> 找不到item，直接回傳value
> 最後應該回傳'["Y"]'，單元格內顯示「["Y"]」
>
> ------
>
> ==實測==
>
> ![image-20210624233432103](https://raw.githubusercontent.com/cynthia204z/mybed1/master/img/image-20210624233432103.png)
>
> 所以應該是傳入的value有問題





# 整理md過程看到的問題

一對多的頁高RWD有點問題

欠款管控稽核中，下方標籤頁包表格的div高度用300px定義(class="table-height")，在我的筆電規格就會超出JNPF-common-layout-center範圍被遮掉（而外層overflow:hidden導致連滾輪都沒有直接看不到）



