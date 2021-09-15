

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
3. 可添加至html標籤內部當作其標籤的屬性來給js存取，其形式為data-*，而*只能填寫小寫字母、不能填入特殊符號和數字
4. 

比如data-id、data-product，

3. 但連字號會被當作.，所以如果是data-id-test，只能在js上使用
element.data.id.test

4. 沒有大小寫之分，全都以小寫來看待，存取時注意
https://blog.csdn.net/lishimin1012/article/details/54425886
