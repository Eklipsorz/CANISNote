---
title: U39note - 應用 Bootstrap Components & Utilities
tags:
---

1. Content： HTML的預設樣式，比如字體大小、圖片、表格的處理。

2. Components： Website 常見的元件，比如導覽列、下拉選單、警告訊息、按鈕、大看板(Jumbotron)

3. Layout: 排版

4. Utilities: 共用的排版屬性





note: 
1. modal是彈跳視窗元件
2. 元件和元件之間的互動會藉由javascript尋找html上對應的id來互動，比如：當按下顯示"Launch demo modal"按鈕後會依照data-target對應的目標來顯示其目標的內容，
也就是modal的內容。

```
<!-- Button trigger modal -->
<button type="button" class="btn btn-primary" data-toggle="modal" data-target="#exampleModal">
  Launch demo modal
</button>

<!-- Modal -->
<div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
  <div class="modal-dialog">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title" id="exampleModalLabel">Modal title</h5>
        <button type="button" class="close" data-dismiss="modal" aria-label="Close">
          <span aria-hidden="true">&times;</span>
        </button>
      </div>
      <div class="modal-body">
        ...
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-secondary" data-dismiss="modal">Close</button>
        <button type="button" class="btn btn-primary">Save changes</button>
      </div>
    </div>
  </div>
</div>


``` 
