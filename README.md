# Introduction

## 依赖安装
gitbook install

## 启动项目
gitbook serve

## 构建项目
gitbook build

## gitbook项目插件
1. gitbook项目添加、安装插件方式：直接在book.json plugins中追加插件项
   1. book.json plugins中追加插件项后 启动项目后会报错，命令行中执行"gitbook install"方可正常运行
      1. 错误信息：`Error: Couldn't locate plugins ${插件名称}, Run 'gitbook install' to install plugins from registry.`
2. book.json中使用的插件
   1. search-pro：高级搜索
   2. anchor-navigation-ex-toc：为文章增加锚点目录栏及回到顶部功能