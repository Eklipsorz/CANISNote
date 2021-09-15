

## reduce 方法
1. 陣列方法，將陣列的所有元素歸納（reduce) 成一個值或著物件
2. 形式為，回傳值會是函式物件中的total參數 

Array = [var1, var2, …. , varn]

Array.reduce(function, default)

function 是指夾雜2-3個參數的函式物件，常見都為兩個，第一個參數為total，第二個參數為currentValue


3. 執行方式：

若沒default參數的話，一開始會是total = function(var1, var2)，第二次會是 total = function(total, var3)，
第三次會是total = function(total, var4)，後面依此類推，最後會是由total來歸納所有function的結果

若有default參數的話，一開始會是total = function(default, var1)，第二次會是total = function (total, var2)
，第三次會是total = function(total, var3)，後面依此類推


使用上有個小細節，若函式物件是箭頭函式，那麼若函式中沒有括號的話，可省略return，有加上括號的話，要添加return。
使用括號的話：
```
let arr = []

arr.reduce((var1, ...., varN) => {
      // do something
      return value/object
})
```


沒使用括號的例子：
```
let arr = []

arr.reduce((var1, ...., varN) => do something)

```
## dataset
1. 屬於html5語法
2. 用來自訂標籤的屬性
3. 可添加至html標籤內部當作其標籤的屬性來給js存取，其形式為data-*，而*只能填寫小寫字母、不能填入特殊符號和數字，而屬性值可依照一般屬性值來定義
4.  標籤自訂屬性的方式以使用方式為：


Html標籤自訂屬性：
```
<element data-variable=“value”> context </element>

```

在JavaScript，由於該屬性會在DOM Tree出現，所以在JS可以直接得到其值，使用方式為對HTML元素節點使用其擁有的dataset屬性，
該屬性會存放所有data-*的屬性，使用方式如下：

```
let element = document.querySelector(‘element’) 

console.log(element.dataset.variable)

```

若*夾雜更多-連字號會在js當作句號的.

```
<element data-variable1-variable2=“value”> context </element>
let element = document.querySelector(‘element’) 

console.log(element.dataset.variable1.variable2)
```

參考資料：
https://blog.csdn.net/lishimin1012/article/details/54425886



## Accessible Rich Internet Application (ARIA)

Accessible Rich Internet Application (ARIA) 是一組特定的標籤屬性，可藉由其標籤屬性幫助更多人去存取該網頁，比如説藉由標籤屬性值來為盲人提供語音的服務，或者視力不好的人

1. 形式上會是aria-開屬性。
2. 例子：在 aria-label 這個設定中，我們把這個功能的名稱定義為 Toggle navigation，當螢幕閱讀器使用語音閱讀你的網站時，就能告訴使用者「這個 button 的目的是 toggle navigation」。


## inline forms
1. Inline forms 是單行表單
2. bootstrap提供的樣式之一，其樣式名為form-inline


## card
1. card 是以卡片的形式來呈現
2. bootstrap提供的樣式之一，其樣式名為card，該樣式下會有card-body和card-footer這兩個子樣式來分別定義卡片的body內容、footer的內容，前者為卡片的主要內容，後者會是卡片的底部內容




## sr-only
1. 它是class的選擇器之一，由bootstrap所提供。
2. 用來定義包含的內容只能給screen reader來看，而screen reader是將文字轉化語音的應用程式



## Pagination

1. 定義：一種將整份內容分散至好幾頁的處理方式
2. 在html中會被當作分頁器，並提供數字來當作目前顯示的頁數和可以瀏覽的頁數
3. bootstrap把pagination當作class的樣式之一，class=“pagination”
4. 它本身就是flexbox，所以可以使用flex的屬性值，比如justify-content-center



## Modal
1. 定義為互動視窗，是當觸發某件事件後而跑出來的視窗
2. 若是使用bootstrap上的modal，則需要定義兩個元件，第一個元件是觸發視窗的元件，第二個元件為視窗
3. 這兩者使用上，觸發視窗的元件a上必須在標籤內定義data-target屬性值，其值會是視窗的id屬性值，只要觸發元件a便能按照data-target來跑出視窗

 4. 通常會在元件a上存有data-toggle屬性值，這是bootstrap定義點擊後元件a的外觀是什麼樣

例子：

這邊 data-toggle 我們指定接下來要使用 modal 的形式，而 data-target 則定義了互動的目標元件是 #movie-modal：Modal 指的是互動視窗，當點擊之後便會跑出另一個視窗，視窗內容為#movie-modal對應的元件
```

<button
class="btn btn-primary btn-show-movie"
data-toggle="modal"
data-target="#movie-modal"
>
More
</button>


    <!-- Movie Modal -->
    <div
      class="modal fade"
      id="movie-modal"
      tabindex="-1"
      role="dialog"
      aria-labelledby="exampleModalLabel"
      aria-hidden="true"
    >
      <div class="modal-dialog">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title" id="movie-modal-title">Modal title</h5>
            <button
              type="button"
              class="close"
              data-dismiss="modal"
              aria-label="Close"
            >
              <span aria-hidden="true">×</span>
            </button>
          </div>
          <div class="modal-body" id="movie-modal-body">
            ...
          </div>
          <div class="modal-footer">
            <button
              type="button"
              class="btn btn-secondary"
              data-dismiss="modal"
            >
              Close
            </button>
            <button type="button" class="btn btn-primary">Save changes</button>
          </div>
        </div>
      </div>
    </div>



```