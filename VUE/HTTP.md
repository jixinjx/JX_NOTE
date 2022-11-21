## post和get的差别
-   GET 请求只能 URL 编码，而 POST 支持多种编码方式
-   GET 请求只接受 ASCII 字符的参数，而 POST 则没有限制
-   GET 请求的参数通过 URL 传送，而 POST 放在 Request Body 中
-   GET 相对于 POST 更不安全，因为参数直接暴露在 URL 中
-   GET 请求会被浏览器主动缓存，而 POST 不会（除非自己手动设置）
-   GET 请求在 URL 传参有长度限制，而 POST 则没有限制
-   GET 产生的 URL 地址可以被收藏，而 POST 不可以
-   GET 请求的参数会被完整的保留在浏览器的历史记录里，而 POST 的参数则不会
-   GET 在浏览器回退时是无害的，而 POST 会再次提交请求

### 为什么不能都用post
-   GET一般有它的语义化的意思，一般用来获取数据，而不修改数据。论对某个资源GET多少次，它的状态是不会改变的，也就是说是幂等的。而POST一般会修改数据。
-   GET 请求是可被缓存的。但是POST不可以
-   GET 速度一般比 POST快.

redis
部署日志
