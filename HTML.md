## HTML相关

#### 1.如何选择图片格式，例如 png, webp

| 图片格式 | 压缩方式 | 透明度 | 动画   | 浏览器兼容                               | 适应场景                                         |
| -------- | -------- | ------ | ------ | ---------------------------------------- | :----------------------------------------------- |
| JPEG     | 有损压缩 | 不支持 | 不支持 | 所有                                     | 复杂颜色及形状、尤其是照片                       |
| GIF      | 无损压缩 | 支持   | 支持   | 所有                                     | 简单颜色，动画                                   |
| PNG      | 无损压缩 | 支持   | 不支持 | 所有                                     | 需要透明时                                       |
| APNG     | 无损压缩 | 支持   | 支持   | FirefoxSafariiOS Safari                  | 需要半透明效果的动画                             |
| WebP     | 有损压缩 | 支持   | 支持   | ChromeOperaAndroid ChromeAndroid Browser | 复杂颜色及形状浏览器平台可预知                   |
| SVG      | 无损压缩 | 支持   | 支持   | 所有（IE8以上）                          | 简单图形，需要良好的放缩体验需要动态控制图片特效 |

#### 2.对 HTML 语义化标签的理解

HTML5 语义化标签是指正确的标签包含了正确的内容，结构良好，便于阅读，比如 nav 表示导航条，类似的还有 article、header、footer 等等标签。

#### 3.HTML5 新增的元素

首先 html5 为了更好的实践 web 语义化，增加了 header，footer，nav,aside,section 等语义 化标签，在表单方面，为了增强表单，为 input 增加了 color，emial,data ,range 等类型， 在存储方面，提供了 sessionStorage，localStorage,和离线存储，通过这些存储方式方便数 据在客户端的存储和获取，在多媒体方面规定了音频和视频元素 audio 和 vedio，另外还 有地理定位，canvas 画布，拖放，多线程编程的 web worker 和 websocket 协议。