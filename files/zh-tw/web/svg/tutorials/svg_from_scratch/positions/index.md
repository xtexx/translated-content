---
title: 座標定位
slug: Web/SVG/Tutorials/SVG_from_scratch/Positions
---

{{ PreviousNext("Web/SVG/Tutorials/SVG_from_scratch/Getting_started", "Web/SVG/Tutorials/SVG_from_scratch/Basic_shapes") }}

## 網格

![](canvas_default_grid.png) 對於所有元素，SVG 使用的座標系统或者說網格系統，和 [Canvas](/zh-TW/docs/Web/API/Canvas_API) 用的差不多（所有電腦繪圖绘图都差不多）。這種座標系统是：以頁面的左上角為 (0,0) 坐標點，坐標以像素為單位，x 軸正方向是向右，y 軸正方向是向下。注意，這和你小時候所教的繪圖方式是相反的。但是在 HTML 文檔中，元素都是用這種方式定位的。

#### 範例：

元素

```html
<rect x="0" y="0" width="100" height="100" />
```

定義一个矩形，即從左上角開始，向右延展 100px，向下延展 100px，形成一个 100\*100 大的矩形。

### 什麼是 "像素"?

基本上，在 SVG 文檔中的 1 个像素對應輸出設備（比如螢幕）上的 1 個像素。但是這種情况是可以改變的，否則 SVG 的名字裡也不至於會有「Scalable」（可縮放）這個詞。如同 CSS 可以定義字體的絕對大小和相對大小，SVG 也可以義絕對大小（比如使用「pt」或「cm」標示單位）同時 SVG 也能使用相對大小，只需给出數字，不標明單位，輸出時就會採用用戶的單位。

在没有进一步规范说明的情况下，1 个用户单位等同于 1 个屏幕单位。要明确改变这种设定，SVG 里有多种方法。我们从`svg`根元素开始：

```html
<svg width="100" height="100"></svg>
```

上面的元素定義了一個 100\*100px 的 SVG 畫布，這裡 1 用戶單位等同於 1 螢幕單位。

```html
<svg width="200" height="200" viewBox="0 0 100 100"></svg>
```

這裡定義的畫布尺寸是 200\*200px。但是，viewBox 屬性定義了畫布上可以顯示的區域：從(0,0)點開始，100 寬\*100 高的區域。這個 100\*100 的區域，會放到 200\*200 的畫布上顯示。於是就形成了放大兩倍的效果。

用戶單位和螢幕單位的映射關係被稱為**用戶座標系統**。除了縮放之外，座標系統還可以旋轉、傾斜、翻轉。預設的用戶座標系統 1 用戶像素等於設備上的 1 像素（但是設備上可能會自己定義 1 像素到底是多大）。在定義了具體尺寸單位的 SVG 中，比如單位是「cm」或「in」，最終圖形會以實際大小的 1 比 1 比例呈現。

下面是引自 SVG1.1 規範的一段說明：

> \[…] 假設在用戶的設備環境裡，1px 等於 0.2822222 毫米（即分辨率是 90dpi），那麼所有的 SVG 內容都會按照這種比例處理： \[…] "1cm" 等於 "35.43307px" （即 35.43307 用戶單位）；

{{ PreviousNext("Web/SVG/Tutorials/SVG_from_scratch/Getting_started", "Web/SVG/Tutorials/SVG_from_scratch/Basic_shapes") }}
