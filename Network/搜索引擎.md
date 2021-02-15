# 搜索引擎

搜索引擎是获取各类网络资源的技术手段。其中著名搜索引擎有Google、Baidu、Sougou、Bing等。

## 搜索语法

其中Google等搜索引擎支持特定的搜索语法。

### 格式字符

* `<key word>`：关键字搜索，默认开启同义词搜索。
* `"<key word>"`：精确匹配，不会查找同义词。
* `*`：通配符。
* `$`：搜索与价格有关的内容。

### 搜索运算

* `AND`：逻辑与运算符，对多个搜索条件进行交集运算。
* `OR`：逻辑或运算符，对多个搜索条件进行并集运算。
* `|`：同OR。
* `+`：条件的并集。
* `-`：集合的差集运算符，对两个搜索集合进行差集运算。
* `in`：用于两个单位间的转换。这个在Google搜索引擎中支持。
* `()`：分组运算符，对搜索结果进行分组运算或者控制运算的优先级。
* `~`：开启同义词搜索。

### 特殊语法
  
* `inurl`：在包含指定的关键字的url中搜索资源。

  ```search
  # 
  inurl:asp?id=
  # allinurl是类似与inurl的搜索语法，可以支持多组关键词。
  ```

* `intitle`：搜索页面标题包含指定关键字的资源。

  ```search
  intitle:admin
  # allintitle是类似与intitle的语法。
  allintitle
  ```

* `intext`：搜索页面内容中包含指定关键字的资源。

  ```search
  intext:keyword
  allintext:keyword_1 keyword_2
  ```

* `inanchor`：搜索页面文本的链接中包含指定关键字的资源。

  ```search
  inanchor: domain.com
  allinanchor
  ```

* `filetype`：指定一个格式类型的文件作为搜索对象：pdf、txt、doc、xls、ppt。

  ```search
  googlehacking filetype pdf
  ```

* `site`：查询搜索引擎对某一网站的收录结果。

  ```search
  site:freebuf.com intitle googlehacking
  ```

* `domain`：查询网站被搜索引擎外链的结果。

* `link`：网站的外链数量。

* `cache`：搜索搜索引擎中关于某些内容的缓存。

* `related`：

* `daterange`:

* `link`：

* 


