---
layout:     post
title:      "在ipad pro上写博客"
subtitle:   " \"Hello World, Hello Blog\""
date:       2017-12-13 19:41:00
author:     "Mountain"
header-img: "img/writeBlogonipad/601.jpg"
mathjax: true
tags:
    - 生活
---

## 前言

一直想找个地方记点什么，但由于我的要求太苛刻，很久以来都没有找到合适的平台。

## 我想要的方式

首先，自从入手ipad pro 10.5后就一直想尽办法将笔记本上的工作全部转移到平板上来。这个过程可以说耗费了大量的时间和金钱。时间主要用在看各种教程，经验，以及思考自己的工作流上了。金钱则是用在大量的或者令人感动或者令人无语的App上。基于此，我希望我的博客也**可以在ipad pro上完成**。

其次，**必须支持markdown语言**。

再次，因为经常需要写带有数学的内容，所以必须要**对公式有很好的支持**。

最后，非常关键的一点是必须要**美观**，毕竟博客是要挂出来的嘛。

## 选择

下面是一些我了解过、尝试过的方式，以及其为什么没有选择这种方式的理由。

|         方式          |                 拒绝理由                 |
| :-----------------: | :----------------------------------: |
|        CSDN         |            不够美观，对移动端支持不好             |
|         简书          | 除了不支持公式外非常符合我的要求，如果以后增加了对公式的支持后会考虑使用 |
|       Medium        |                  有墙                  |
|      WordPress      |              总之用起来就是不顺               |
| Hexo + Github Pages |  各方面都很好，但是必须在本地编译，所以ipad pro上似乎不能用   |

## 如何打造我的工具

在折腾了几圈后，最终选择了[jekyll](https://www.jekyll.com.cn)加[Github Pages](https://pages.github.com)的方式。其实个人感觉用jekyll和[Hexo](https://hexo.io)差不多，只是由于jekyll项目可以在Github平台上自动编译，因此无需本地具有编译能力，所以ipad pro就可以用了，毕竟ipad pro上有不少Github工具。

主要分为三步完成我的工作。

### 搭建博客框架

网上有很多详细的如何用已有的模版，搭建博客框架的教程，这里就不再赘述了，我主要参考的文章有两个：

[利用 GitHub Pages 快速搭建个人博客](http://www.jianshu.com/p/e68fba58f75c)以及[Hux blog 模板](https://github.com/Huxpro/huxpro.github.io/blob/master/README.zh.md)，事实上，前者是基于后者的模版构建的，而后者又是对其它模版修改后的到的。分享的好处就是我们可以让事物越来越复合自己的需要。

### 让公式显形

通过Hux模版搭建的博客还不能很好的支持数学公式，因此还需要进一步调整。找了不少文章才解决这个问题[^sgeos] [^jekyll]。具体做法是，先在**_includes**文件夹内创建文件**mathjax.html**，将下列代码粘贴至**mathjax.html**中：

```html
{% if page.mathjax %}
<script type="text/x-mathjax-config">
  MathJax.Hub.Config({
    TeX: {
      equationNumbers: {
        autoNumber: "AMS"
      },
      TagSide: "right"
    },
    tex2jax: {
      inlineMath: [ ['$','$'], ["\\(","\\)"] ],
      processEscapes: true
    }
  });
</script>
<script
  type="text/javascript"
  charset="utf-8"
  src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"
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

其中还设置了公式的自动编号，这使我们可以用非常类似于**Latex**的方式写公式。

接着在**_layouts/default.html**文件中加一句:

```html
{% include mathjax.html %}
```

到此，配置工作基本完成。在写文章时如果想在某篇文章中加入公式支持，只需要在其**YAML**部分加一句

```markdown
mathjax: true
```

即可，例如本文中：

```yaml
layout:     post
title:      "在ipad pro上写博客"
subtitle:   " \"Hello World, Hello Blog\""
date:       2017-12-13 19:41:00
author:     "Mountain"
header-img: "img/writeBlogonipad/601.jpg"
mathjax: true
```

现在可以尝试下写写公式的了: $E = m c^2$

\begin{equation}\label{ai}
E = mc^2
\end{equation}

质能公式\ref{ai}.

### 到ipad上去

最后我还想能够在ipad pro上写博客。iOS平台上有许多git工具，经过试用、比较后我选择了[Working Copy](https://workingcopyapp.com)。该软件是免费的，但是如果要用它来写博客就必须使用Push功能，这就需要解锁内购了，而且还挺贵的。不过考虑到这个软件确实强大、美观，内购也是值得的。

首先在Working Copy中登陆Github账号，接着将博客对应的Github仓库Clone到ipad上，然后就可以开始在ipad pro上写博客了。不过记住每次修改之前先pull一下，获取最新版本的仓库，写完后commit当前修改，再push到远程，这样可以有效减少笔记本和ipad pro写作内容的冲突。


[^sgeos]: [Adding MathJax to a GitHub Pages Jekyll Blog](https://sgeos.github.io/github/jekyll/2016/08/21/adding_mathjax_to_a_jekyll_github_pages_blog.html)
[^jekyll]: [Math Support](https://jekyllrb.com/docs/extras/)