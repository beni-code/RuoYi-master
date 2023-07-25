# element上传组件自定义方式


data里维护一个文件列表变量：fileList

设置el-upload组件的属性
* `auto-upload` 设置为`false`
* `on-change`和`on-remove`事件内将fileList的内容设置为文件raw的列表
    
  ``` js
  this.fileList = [];
  for (var i = 0; i < fileList.length; i++) {
    this.fileList.push(fileList[i].raw);
  }
  ```

* `limit`属性可以设置可上传的最大文件数
* `action`属性设为'#'

上传逻辑

```js
// 将文件数组组合进FormData的files属性中
var formData = new FormData()
for (var i = 0; i < this.fileList.length; i++) {
  formData.append('files', this.fileList[i]);
}

// 接着直接将FormData对象赋给post请求的data（请求体）即可
```

后端接口接收参数：

```
@RequestParam("files") MultipartFile[] files
使用这种形式接收文件类型的参数
```
