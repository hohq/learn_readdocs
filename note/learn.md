# readdocs 学习笔记

## 初步认知

readdocs 用 sphinx 主要构成，Sphinx 是 Python 社区编写和使用的文档构建工具，除了天然支持 Python 项目以外，Sphinx 对 C/C++ 项目也有很好的支持，并在不断增加对其它开发语言的支持。

- Sphinx 网站：http://sphinx-doc.org/
- Sphinx 使用手册：https://zh-sphinx-doc.readthedocs.io/en/latest/index.html

Sphinx 使用 reST 作为标记语言，其与 markdown 非常相似。

- reStructuredText 网站：http://docutils.sf.net/rst.html

## 初步实战

使用总比弄懂简单，我一般先用一遍然后再去看它的构建
https://blog.csdn.net/lu_embedded/article/details/109006380

根据这个指引写一点 rest 试试
试试用 sphinx 构建

### 构建一个 diary 日记文档

#### 启动！

使用 sphinx-quickstart 进行初始化

- y
- 项目名
- 作者
- release 号
- 语言：（这次的要求是英文所以我们使用 en）

ok 这样就帮我们初始化了一个项目（怎么有点像 vue 这种构建）
可以看出，这个项目还是很依赖于 make 的。

#### 展示

##### 启动

make html 启动！这样就有对应的 indexhtml
ok 那如果我们用 nginx 按理来说我们也能部署
但 sphinx 给我们提供了很方便的 sphinx-autobuild
sphinx-autobuild source build/html 自动将项目映射到 8000 端口

怎么越来越熟悉了，这玩意怎么有种 pnpm 的感觉

###### 样式选择

在 conf.py 中修改
html_theme 字段可以改出（我怎么觉得我可以在这安装某个插件以来丰富展示，可以去研究一下）

- html_theme = 'sphinx_rtd_theme'
  这个好看 ↑

#### 一些reST分析

- 第1-4行由 .. + 空格开头，属于多行评论（类似于注释），不会显示到网页上。
- 第6-7行是标题，reST 的标题需要被双下划线（或单下划线）包裹，并且符号的长度不能小于文本的长度。
- 第9-11行是文档目录树结构的描述，.. toctree:: 声明了一个树状结构（toc 即 Table of Content），-maxdepth: 2 表示目录的级数（页面最多显示两级），:caption: Contents: 用于指定标题文本（可以暂时去掉）。
- 第15-20行是索引标题以及该标题下的三个索引和搜索链接。

也就是说，indexhtml这个界面/路由是由这个rest文件组织的，我们可以通过创建新的rest文件让它自动组织创建出新的页面。但需要注意进行路由管理（？需要吧）

在toctree中可以进行路由管理，直接写上对应的相对路径即可进行。
空格非常重要！！！！！！！！不要少打不要多打！！！！！！！

哦吼是即时响应的。