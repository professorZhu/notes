

使用nodejs搭建一个网络代理系统，技术点：nodejs，express

前提介绍node stream pipe方法

假设有两个对象，Readable用于产生数据，Writable用于接收Readable产生的数据， 一般可以使用事件进行关联，但node提供了pipe管道方法可以方便的关联这些流对象。

```javascript
import stream from 'stream';

var w = new stream.Writable;
var r = new stream.Readable;

// 定义一个会持续生成数据的 Readable 数据源
r._read = () => {};
void function callee(i) {
  r.push(i + '');
  setTimeout(callee, 200, i + 1);
}(0);

// 当收到时更新数据
r.on('data', data => {
  w.write(data);
});

// 定义一个会将接收到的数据输出的输出源
w._write = (data, enc, next) => {
  console.log(data + '');
  next();
};
```

r._read 会产生数据

r.on 监控如果有数据进入写入到w中

w._write 监控如果有数据写入执行

这是一个最简单的需求了，但是代码上看还是有些笼余。

使用pipe

```javascript
import stream from 'stream';

var w = new stream.Writable;
var r = new stream.Readable;

// 定义一个会持续生成数据的 Readable 数据源
r._read = () => {};
void function callee(i) {
  r.push(i + '');
  setTimeout(callee, 200, i + 1);
}(0);

// 关联
r.pipe(w);

// 定义一个会将接收到的数据输出的输出源
w._write = (data, enc, next) => {
  console.log(data + '');
  next();
};
```

使用pipe设置了一个r与w的通道，会在r与w间产生一个链条。返回方法参数对象

前期介绍完毕

------

代理网关的实现

我们可以将网络请求，request，response看做是两个通道。

在用户向代理想法发起请求时，我们解析用户的请求，将host  url指定向我们希望的位置

使用http模块向我们重新指定的位置发起请求。

使用pipe 关联http模块的reqest response向expressreqest response

![img](https://raw.githubusercontent.com/professorZhu/images/master/node/geteway.png) 

 核心代码

```javascript

router.get('/*', function(req, res, next) {
	/**
     * 重定向host port path method headers 等
     */
    var options = {
        host: api.root,
        port: api.port,
        path: req.url,
        method: req.method,
        headers: req.headers
    };
	
 	/**
     * 发送请求
     */
    var request = http.request(options,function(response){
        console.log(response.statusCode);
        res.statusCode = response.statusCode;
        /**
         * 将response放入res通道中
         */
        response.pipe(res);
    }).on("error",function(){
        res.statusCode = 503;
        res.end();
    });
    /**
     *使用pipe通道转发request
     */
    req.pipe(request);

}

```



