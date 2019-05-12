# HashRouter vs BrowserRouter



**HashRouter vs BrowserRouter**

* HashRouter
  * 它使用URL的哈希部分（即window.location.hash）来保持页面的UI与URL同步
* BrowserRouter
  * 使用HTML5历史API（ pushState，replaceState和popstate事件），让页面的UI同步与URL 

官方建议： BrowserRouter 原因如下

* 因为hashRouter没有使用html5中history的api，无法从历史记录中获取到key和state值，所以当刷新路由后state值会丢失导致页面显示异常
* 在以前的版本中，我们试图填充行为，但是有一些我们无法解决的边缘情况。任何需要此行为的代码或插件都不起作用。由于此技术仅用于支持旧版浏览器，因此我们建议您将服务器配置为使用

HashRouter最简单，不需要服务器端渲染，服务器端无论对任何URL请求都返回一模一样的HTML就好，真正有效信息是 HASH 前的部分 BrowseRouter稍微复杂一点，因为要求服务器端对不同URL返回不同的HTML 如果服务端没有配置 当我们从首页进入其他路由，如果刷新浏览器，就会报404错误，要想重新进入，必须返回路由默认首页

**原因**

上面的问题其实是因为，刷新浏览器，相当于浏览器向服务端求/xxxx/manage/ 但是服务端（或者nginx）并没有配置这样一个路由，找不到当然返回404。

那是不是就需要我们配置这样一个路由，当然不是，因为还有许多其他路由，这样配置当然不可能；其次，spa应用路由是在前端由react-router配置控制的

解决办法就是，把找不到的路由，都返回index.html,这样刷新后，利用浏览器缓存，js会根据路由，控制应该那个页面显示。刷新前后还是同一个页面

**BrowseRouter 服务端配置**

真正的配置，只需要在nginx的配置，比如我使用的默认配置（/etc/nginx/conf.d/default.conf\),加上如下

```text
 server {  
   server_name xxx.xxxxxx.com;  
   location / {  
     root /xxx/xxx/xxx/www/build;  
     try_files $uri /index.html;  
   }  
   location ^~ /api/ {  
     proxy_pass http://11.11.11.11:1111/;(服务端接口做代理)  
   }
```

**try\_files**

* 其作用是按顺序检查文件是否存在，返回第一个找到的文件或文件夹\(结尾加斜线表示为文件夹\)，如果所有的文件或文件夹都找不到，会进行一个内部重定向到最后一个参数。
* 需要注意的是，只有最后一个参数可以引起一个内部重定向，之前的参数只设置内部URI的指向。最后一个参数是回退URI且必须存在，否则会出现内部500错误。

