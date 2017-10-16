# laravel-vue-file-upload
laravel+vue file upload(使用laravel和vue实现文件上传功能)
The "form" tags can be used in vue file because input tags are invalid.
在vue框架里面无法使用<input type="file">类似的文件上传html代码，因此使用了form标签

html代码如下：
<form enctype="multipart/form-data" method="post" class="service-file-form">
    <input type="file" class="form-control" name="file">
</form>
<input class="btn btn-warning btn-sm" value="Upload" v-on:click="uploadService('service-'+item.id)">

js部分：
uploadAdvertise(tag) {
    if (!this.order.id) {
        swal({
            title: "Warning!",
            text: "Please save the order first!",
            type: "warning",
            confirmButtonText: "OK"
         });
         
      } else {
          let uri = 'api/order/upload/' + this.orderId + '/?tag=' + tag;
          let form = new FormData($(".ad-file-form")[0]);
          //upload api
          this.upload(uri, form);
       }
},

接下来就是后端如何接收文件数据

Storage::put($path, file_get_contents($request->file('file')));

Above codes can receive the file and save it.
这样就把前端传过来的文件保存下来了
