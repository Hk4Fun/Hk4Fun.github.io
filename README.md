主页：https://hk4fun.github.io

部署平台：[GitHub Pages][1]

框架：[Hexo][2]

主题：[Yelee][3] [使用说明][4]（fork 于 [Yilia][5]）

分享：[AddThis][6]

图床：[微博图床][7]

网站统计：[百度统计][8]

页面统计：[不蒜子][9]

评论系统：[来必力（Livere）][10]

写作工具：[Typora][11]

由于yelee没有加入livere评论系统，需要自己添加:

首先在主题的 `_config.yml `文件中添加如下配置：

``` yaml
livere:
  on: true
```
然后在`\themes\yelee\layout\_partial\comments`下添加`livere.ejs`，把livere安装代码复制进去，文件内容如下，**其中data-uid就是你自己的data-uid**：

``` gcode?linenums
<!-- 来必力City版安装代码 -->
<div id="lv-container" data-id="city" data-uid="your data-uid" style="margin-left:30px;margin-right:30px">
<script type="text/javascript">
   (function(d, s) {
       var j, e = d.getElementsByTagName(s)[0];

       if (typeof LivereTower === 'function') { return; }

       j = d.createElement(s);
       j.src = 'https://cdn-city.livere.com/js/embed.dist.js';
       j.async = true;

       e.parentNode.insertBefore(j, e);
   })(document, 'script');
</script>
<noscript>为正常使用来必力评论功能请激活JavaScript</noscript>
</div>
<!-- City版安装代码已完成 -->
```
**注意官网livere给的安装代码没有`margin-left:30px;margin-right:30px`，这个样式是为了不与左边栏叠加**

最后在`\themes\yelee\layout\_partial\article.ejs`中的`<% if (!index && post.comments){ %>`后面插入：

``` gcode?linenums
<% if (theme.livere.on){ %>
    <%- partial('comments/livere', {
        key: post.path,
        title: post.title,
        url: config.url+url_for(post.path)
      }) %>
```
至此，为yelee主题添加livere评论插件完成

最后向Hexo作者tommy致敬！（附上[Hexo起源之地][12]）

更新：不蒜子的域名更新了，需要在 MyBlog\themes\yelee\layout\_partial\after-footer.ejs 
中将不蒜子的域名由

`<script async src="https://dn-lbstatics.qbox.me/busuanzi/2.3/busuanzi.pure.mini.js">
</script>`

改为

`<script async src="https://busuanzi.ibruce.info/busuanzi/2.3/busuanzi.pure.mini.js">
</script>`

[1]: https://pages.github.com/
[2]: https://hexo.io/
[3]: https://github.com/MOxFIVE/hexo-theme-yelee
[4]: http://moxfive.coding.me/yelee/
[5]: https://github.com/litten/hexo-theme-yilia
[6]: https://www.addthis.com/
[7]: https://chrome.google.com/webstore/detail/%E6%96%B0%E6%B5%AA%E5%BE%AE%E5%8D%9A%E5%9B%BE%E5%BA%8A/fdfdnfpdplfbbnemmmoklbfjbhecpnhf
[8]: https://tongji.baidu.com/web/welcome/login
[9]: http://ibruce.info/2015/04/04/busuanzi/
[10]: https://livere.com/
[11]: https://typora.io/
[12]: https://zespia.tw/blog/2012/10/11/hexo-debut/