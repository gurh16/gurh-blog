---
title: 为hexo添加live2d
date: 2021-01-18 9:57
tags: [hexo,live2d]
categories: hexo
number: 1
---

## 为hexo添加live2d

1. 安装live2d模块

   `npm install --save hexo-helper-live2d`

2. 安装live2d模型

   `npm install {packagename}`

   - `live2d-widget-model-chitose`
   - `live2d-widget-model-epsilon2_1`
   - `live2d-widget-model-gf`
   - `live2d-widget-model-haru/01`
   - `live2d-widget-model-haru/02`
   - `live2d-widget-model-haruto`
   - `live2d-widget-model-hibiki`
   - `live2d-widget-model-hijiki`
   - `live2d-widget-model-izumi`
   - `live2d-widget-model-koharu`
   - `live2d-widget-model-miku`
   - `live2d-widget-model-ni-j`
   - `live2d-widget-model-nico`
   - `live2d-widget-model-nietzsche`
   - `live2d-widget-model-nipsilon`
   - `live2d-widget-model-nito`
   - `live2d-widget-model-shizuku`
   - `live2d-widget-model-tororo`
   - `live2d-widget-model-tsumiki`
   - `live2d-widget-model-unitychan`
   - `live2d-widget-model-wanko`
   - `live2d-widget-model-z16`

3. 相关配置

   在hexo的blog根目录下，编辑_config.yml文件，在最下方加入：

   

```yml
# Live2D
## https://github.com/EYHN/hexo-helper-live2d
live2d:
  enable: true
  # enable: false
  scriptFrom: local # 默认
  pluginRootPath: live2dw/ # 插件在站点上的根目录(相对路径)
  pluginJsPath: lib/ # 脚本文件相对与插件根目录路径
  pluginModelPath: assets/ # 模型文件相对与插件根目录路径
  # scriptFrom: jsdelivr # jsdelivr CDN
  # scriptFrom: unpkg # unpkg CDN
  # scriptFrom: https://cdn.jsdelivr.net/npm/live2d-widget@3.x/lib/L2Dwidget.min.js # 你的自定义 url
  tagMode: false # 标签模式, 是否仅替换 live2d tag标签而非插入到所有页面中
  debug: false # 调试, 是否在控制台输出日志
  model:
    use: live2d-widget-model-haru
    scale: 1
    hHeadPos: 0.5
    vHeadPos: 0.618
    # use: live2d-widget-model-wanko # npm-module package name
    # use: wanko # 博客根目录/live2d_models/ 下的目录名
    # use: ./wives/wanko # 相对于博客根目录的路径
    # use: https://cdn.jsdelivr.net/npm/live2d-widget-model-wanko@1.0.5/assets/wanko.model.json # 你的自定义 url
  display:
    superSample: 2
    width: 150
    height: 300
    position: right
    hOffset: 0
    vOffset: -20
  mobile:
    show: true # 是否在移动设备上显示
    scale: 0.5 # 移动设备上的缩放       
  react:
    opacityDefault: 0.7
    opacityOnHover: 0.8
```

**注意：yml文件强制缩进，不要多打空格。**

最后使用`hexo g`重新构建网站