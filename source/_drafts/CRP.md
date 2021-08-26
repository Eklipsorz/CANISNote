---
title: Critical Rendering Path 簡介
tags:
---


Critical Rendering Path 是瀏覽器如何將網頁檔案轉化成網頁的處理路徑，其路徑包含了Networking、HTML/CSS/JavaScript三者合力形成的DOM(Document Object Model)樹狀結構和CSSOM(CSS Object Model)樹狀結構、DOM樹狀結構和CSSOM樹狀結構結合而成的Render Tree、Layout、Paint，每個路徑之間關係會像是
