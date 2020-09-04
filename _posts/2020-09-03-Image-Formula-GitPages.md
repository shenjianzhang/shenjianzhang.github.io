---
layout: post
mathjax: true
title:  "在Markdown文件中添加公式和调整图片格式"
date:   2020-09-03 22:17:00 +0800
categories: git
---

这篇文章记录自己在用`.markdown`格式的文件写 **GitHub Page** 时学习到的两个技巧，分别是如何在GitHub Page的网页中添加公式，和如何调整Git Page网页中插入的图片的格式（如大小，对齐方式等）。需要说明的是，这两个问题在网上都能搜到很多不同的解决方法，所以这里只是记录自己所采用的方法，并不一定是唯一的或者最好的。

## 添加公式
在[用GitHub Pages和Jekyll写博客](https://shenjianzhang.github.io/git/2020/05/03/Git-Pages.html)中我们可以看到，GitHub Page是借助 **Jekyll** 来搭建个人博客的，Jekyll可以支持Markdown格式，但是却不能在其中直接插入公式，需要借助[MathJax](https://www.mathjax.org/)来帮助渲染。

由于这里采用的方法需要修改`_includes/`和`_layouts/`中的文件，而自己之前在设置Jekyll主题时采用的是官方默认的方式，所以博客目录中并没有相应的文件夹或者文件，这样其实个性化修改起来会相对不方便。因此我们首先到 **minima** 主题的网站<https://github.com/jekyll/minima>下载相应的文件，包括`_includes`，`_layouts`，`_sass`，`assets`中的所有文件，并根据其`_config.yml`修改本地GitHub Pages根目录下的`_config.yml`。修改完成后，可以参考[用GitHub Pages和Jekyll写博客](https://shenjianzhang.github.io/git/2020/05/03/Git-Pages.html)中的方法，先在本地查看构建的站点。如果没有问题的话，就可以将新的修改暂存并提交到本地的Git仓库中，并推送到GitHub中。
```bash
$ git add .
$ git commit -m "Add files for theme minima."
$ git push -u origin master
```

完成这些修改后，就可以设置插入公式了。首先在`_includes/`中新建文件`_includes/mathjax.html`，并写入以下代码：
```html
{% if page.mathjax %}
<script type="text/x-mathjax-config">
  MathJax.Hub.Config({
    extensions: ["tex2jax.js"],
    jax: ["input/TeX", "output/HTML-CSS"],
    <!--这部分是 tex2jax.js 预处理程序需要的配置-->
    tex2jax: {
      inlineMath: [ ['$','$'], ["\\(","\\)"] ],
      displayMath: [ ['$$','$$'], ['\\[','\\]'] ],
      processEscapes: true,
      processEnvironments: true
    },
    <!--处理 TeX 及相关插件的输入的-->
    TeX: {  
      equationNumbers: { autoNumber: "AMS" },
      noUndefined: { attributes: { mathcolor: "red", mathbackground: "#FFEEEE", mathsize: "90%" } },
      Macros: { href: "{}" }
    },
    <!-- MathJax **处理 HTML/CSS 输出的配置**-->
    "HTML-CSS": {
    <!--设置字体（preferredFont、availableFonts）-->
      availableFonts: ["TeX"]
    }
  });
</script>
<script
  type="text/javascript"
  charset="utf-8"
  src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML"
>
</script>
<script
  type="text/javascript"
  charset="utf-8"
  src="https://vincenttam.github.io/javascripts/MathJaxLocal.js"
>
</script>
{% endif %}
```
之后在`_layouts/post.html`的`header`中添加代码
```
{% raw %}{% include mathjax.html %}{% endraw %}
```
即
```
...
<header class="post-header">
  {% raw %}{% include mathjax.html %}{% endraw %}
  <h1 class="post-title p-name" itemprop="name headline">{{ page.title | escape }}</h1>
...
```
这样修改之后，我们只需要在任何想要插入公式的博客(post)的[YAML front matter](https://jekyllrb.com/docs/front-matter/)部分通过`mathjax: true`来开启MathJax功能即可，例如
```ruby
---
layout: post
mathjax: true
title:  "SPECFEM3D_GLOBE中网格(mesh)的可视化"
date:   2020-08-28 19:18:00 +0800
categories: specfem3d
---
```
如果设置没有问题的话，在这个博客中就可以通过Tex的语法来插入公式了。
`.markdown`中的
```
对于一个单元 $\Omega_e$ 中笛卡尔坐标下的点$\mathbf{x}=(x,y,z)$，我们有其与参考单元的映射：
\\[
\begin{equation}
 \mathbf{x}(\boldsymbol{\xi})=\sum_{a=1}^{n_a} N_a(\boldsymbol{\xi}) \mathbf{x_a}
\end{equation}
\\]
其中$\boldsymbol{\xi}=(\xi,\eta,\zeta), -1\leq\xi,\eta,\zeta \leq 1$。$\mathbf{x_a}$为控制点(control points, or anchors)。
```
在网页中效果

对于一个单元 $\Omega_e$ 中笛卡尔坐标下的点$\mathbf{x}=(x,y,z)$，我们有其与参考单元的映射：
\\[
\begin{equation}
 \mathbf{x}(\boldsymbol{\xi})=\sum_{a=1}^{n_a} N_a(\boldsymbol{\xi}) \mathbf{x_a}
\end{equation}
\\]
其中$\boldsymbol{\xi}=(\xi,\eta,\zeta), -1\leq\xi,\eta,\zeta \leq 1$。$\mathbf{x_a}$为控制点(control points, or anchors)。

简单来看的话，根据`_includes/mathjax.html`中的设置，`$`和`$`之间的内容会被解释为行内公式，而`\\[`和`\\]`之间的内容则会解释为行间公式。这里其实有个问题，在`_includes/mathjax.html`中设置`$$`和`$$`之间的内容也可以解释为行间公式，但是在应用中却并不成功，我自己也没找到具体原因。

关于MathJax的语法问题，用过Latex的话应该就很熟悉了，一些具体的语法也可以参考网上很多相关网站，例如[MathJax basic tutoral and quick reference](https://math.meta.stackexchange.com/questions/5020/mathjax-basic-tutorial-and-quick-reference)。

#### 主要参考资料
- [MathJax Documentation](http://docs.mathjax.org/en/latest/index.html)
- [Adding MathJax to a GitHub Pages Jekyll Blog](http://sgeos.github.io/github/jekyll/2016/08/21/adding_mathjax_to_a_jekyll_github_pages_blog.html)
- [为hexo添加mathjax支持](https://www.zhongxiaoping.cn/2019/01/09/%E4%B8%BAhexo%E6%B7%BB%E5%8A%A0mathjax%E6%94%AF%E6%8C%81/)

---

## 调整图片格式
当我们采用`![name of image](source of image)`的方法在`.markdown`文件中插入图片时，图片的格式在文件`_sass/minima/_base.scss`中通过以下内容设定
```css
/**
 * Images
 */
img {
  max-width: 100%;
  vertical-align: center;
}
```
这样的问题是，只能设定全局中图片的大小，而不能根据每张图片单独设置，而且虽然这里写着`vertical-align: center`，但是在网页中图片依旧是靠左排列。

这里，根据网上的方法，将插入图片的方法改为直接采用 **html标签**，例如将
```markdown
![slice_edge_num](/img/slice_edge_num.png)
```
替换为
```html
<div style="text-align:center">
  <img src="/img/slice_edge_num.png" width="500"/>
</div>
```
其中`style="text-align:center`控制图片的位置，即居中排列，而`width=500`为图片的大小，这里的默认单位是 *px*，即CSS像素单位，注意 **minima** 主题中文章的宽度默认设为800px，当然，这里图片的宽度也可以设为相应的百分比，如`width=80%`。

调整前后的图片效果如下

原始设置

![img_before_reset](/img/img_before_reset.png)

修改后

![img_after_reset](/img/img_after_reset.png)


可以看到图片居中显示，而且尺寸相应变小。

#### 主要参考资料
- [Markdown-图片设置（大小，居中）](https://blog.csdn.net/qq_35451572/article/details/79443467)
- [Markdown 中控制图片的大小 对齐方式](https://blog.csdn.net/sunsteam/article/details/73112787?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-2.channel_param&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-2.channel_param)
