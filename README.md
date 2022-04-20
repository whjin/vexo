# 博客配置

## 全局配置 ##

由于初始的博客页面菜单栏是不完整的，需要新建页面才会显示出来，这个很多初次使用 **Hexo** 的朋友并不了解，所以这里给出方法：

- 安装依赖：`cnpm i`
- 新建菜单页面：`hexo new page "tags"`，以此类推， `archives`、`project`、`about`页面也是这样操作，如果需要把标题改为中文，可以到 `source` 文件下修改相应的文件。我已经帮大家改好了。
- 对于 `scaffolds` 文件夹里的文章模板，我推荐大家直接复制并覆盖自己的对应文件，方便以后写文章，减少重复性工作。
- 微博、脸书、Github等 `Links` 只需要填写用户名，知乎那一项我填了作为参考。
- 不明白的可以提 `Issuss`

## 可能遇到的问题 ##

- 在线测试命令为： `hexo server` 简写为`hexo s`；
- 编译文件命令为： `hexo g`;
- 上传文件到 **Github** 命令为： `hexo d`

遇到 **hexo deploy命令显示ERROR Deployer not found : github**

解决方法：`deploy`的`type`改成`git`，然后运行下 `npm install hexo-deployer-git --save`      
再运行 `hexo g`、`hexo d`

**安装插件**，根据自身需要进行选择：

    npm install hexo-generator-feed --save
    npm install hexo-generator-sitemap --save
    npm install ember-cli-materialize --save-dev
