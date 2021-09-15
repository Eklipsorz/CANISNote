

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
