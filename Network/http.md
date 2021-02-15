# HTTP

[//]: # (__author__ = "Wenger Binning")

## HTTP响应报文

### 响应状态码

* `1xx`：指示信息。表示请求已接收，继续处理。

* `2xx`：请求成功。表示请求已接收、理解、处理。

  * `200`：请求成功。

* `3xx`：请求重定向。表示请求需要进行更进一步的操作。

* `4xx`：客户端错误。表示请求有语法错误或请求无法实现。

  * `403`：服务端收到请求，但是拒绝提供服务。
  
* `5xx`：服务端错误。表示服务器未能实现请求。