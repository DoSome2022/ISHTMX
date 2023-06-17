# HTMX的簡介  
- htmx 使您可以使用屬性 直接在 HTML 中訪問AJAX、CSS Transitions、WebSockets和服務器發送事件，因此您可以使用 超文本的簡單性和 強大功能構建現代用戶界面

- htmx 很小（~14k min.gz'd）， 無依賴性， 可擴展，兼容 IE11 並且與 react 相比，代碼庫大小減少了 67%
---
## 安裝HTMX  
```
  <script src="https://unpkg.com/htmx.org@1.9.2"></script>
```
- 在寫這篇文章時，它是1.9.2版本。一旦完成，你就可以在你的網頁上實現htmx功能。

---

## htmx 核心思想
- 任何元素，不僅僅是錨點和表單，都可以發出 HTTP 請求
- 任何事件，不僅僅是點擊或表單提交，都可以觸發請求
- 可以使用任何HTTP 動詞，而不僅僅是GET和POST
- 任何元素，不僅僅是整個窗口，都可以成為請求更新的目標

---

##  用htmx發送AJAX請求  
Htmx提供了一組屬性，允許你直接從一個HTML元素發送AJAX請求。可用的屬性包括。

- hx-get- 向提供的URL發送GET 請求
- hx-post- 向提供的URL發送POST 請求
- hx-put- 向提供的URL發送PUT 請求
- hx-patch- 發送PATCH 請求到所提供的URL。
- hx-delete- 發送DELETE 請求到所提供的URL。

---

## 例子 
來源  [官網](https://htmx.org/docs/#introduction)


```
  <button hx-post="/clicked" hx-swap="outerHTML">
    Click Me
  </button>
```
這個按鈕上的和hx-post屬性hx-swap告訴 htmx：

- 當用戶點擊這個按鈕時，向 /clicked 發出 AJAX 請求，並用 HTML 響應替換整個按鈕

知道運作原理後再看看實戰中的htmx的樣貌

```
<input type="text" name="q"
    hx-get="/trigger_delay"
    hx-trigger="keyup changed delay:500ms"
    hx-target="#search-results"
    hx-swap="outerHTML"
    placeholder="Search..."
>
<div id="search-results"></div>

```
hx-get上面提及是AJAX  

而hx-trigger , hx-target 和 hx-swap 是甚麼?

--- 
### hx-trigger(觸發請求)
默認情況下，AJAX 請求由元素的“自然”事件觸發：

- input, textarea&在事件select上觸發change
- formsubmit在事件上觸發
- click其他一切都由事件觸發

簡單來說就是在前端的js裹,可以設定鼠標滑過某地方後會有甚麼效果出現,按了鍵盤一刻有效果,還是按下後放手才有效果,再看看以下在官網的例子
這是當鼠標進入時div發佈到的：/mouse_entered
```
<div hx-post="/mouse_entered" hx-trigger="mouseenter">
    [Here Mouse, Mouse!]
</div>
```
---

### hx-target(目標)  
如果您希望將響應加載到與發出請求的元素不同的元素中，您可以使用hx-target屬性，它採用 CSS 選擇器。回顧我們的實時搜索示例：
```
<input type="text" name="q"
    hx-get="/trigger_delay"
    hx-trigger="keyup changed delay:500ms"
    hx-target="#search-results"
    hx-swap="outerHTML"
    placeholder="Search..."
>
<div id="search-results"></div>

```
以上例子hx-target="#search-results" 是指 id名叫search-results

---

### hx-swap(交換)  
htmx 提供了幾種不同的方法來將返回的 HTML 交換到 DOM 中。默認情況下，內容替換 innerHTML目標元素的。您可以使用具有以下任何值的hx-swap屬性來修改它：
- innerHTML
默認情況下，將內容放在目標元素內
- outerHTML
用返回的內容替換整個目標元素
- afterbegin
在目標內的第一個孩子之前添加內容
- beforebegin
在 targets 父元素中的 target 之前添加內容
- beforeend
在目標內的最後一個孩子之後追加內容
- afterend
在 targets 父元素中的 target 之後追加內容
- delete
無論響應如何，都刪除目標元素
- none
不附加響應中的內容（帶外交換和響應標頭仍將被處理）

---
### CSS 過渡  
htmx 使得在沒有 javascript 的情況下使用CSS Transitions變得容易。考慮這個 HTML 內容：
```
<div id="div1">Original Content</div>
```
想像一下，這個內容通過一個帶有這個新內容的 ajax 請求被 htmx 替換：
```
<div id="div1" class="red">New Content</div>
```
我們可以編寫一個從舊狀態到新狀態的 CSS 轉換：
```
.red {
    color: red;
    transition: all ease-in 1s ;
}
```
注意兩點：

- div在原始內容和新內容中具有相同的id
- 該類red已添加到新內容中

簡單點就是
```
<style>
.red {
    color: red;
    transition: all ease-in 1s ;
}
</style>

<div id="div1" class="red">New Content</div>

//要用css的時候可以開一個名叫style,裹面寫下名叫red的class
之後可以直接用css

```

最後HTMX可以理解成在django裹可以執行簡單的js  
詳情可去[官網](https://htmx.org/docs/#introduction)