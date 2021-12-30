# SCSS Note

## 變數

使用變數時，單位不要寫在變數裡

> dev時編譯會過，build就會出問題。

**錯誤示範**：

```scss
$small: 12px;
$large: 14px;

@mixin MixinFontSize($fontSize){
  font-size $fontSize;
}
```

**正確做法**：

```scss
$small: 12;
$large: 14;

@mixin MixinFontSize($fontSize){
  font-size $fontSize + px;
}
```

