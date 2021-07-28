---
title: JavaScript - Scope 簡介
date: 2021-07-29 01:29:40
tags: JavaScript
---

在電腦編程中，(作用域)Scope是指對應某種entity的name所能夠被合法辨識以及使用的範圍，其中entity是指的是某種記憶體區塊，而name就是variable，換言之，只要我們透過variable就能操控代表記憶體區塊的entity。



## Global vs. Local

根據Scope的範疇，我們主要分為Global和Local，前者指的是合法辨識和使用的範圍是整個程式碼(系統)或者整個檔案，而Local則是範圍被限制在一個小區塊，並不會是整個系統當中。

通常只要某個對應entity的名字脫離它本身的scope，系統會自動釋放記憶體。



