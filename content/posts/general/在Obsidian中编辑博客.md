---
title: "在Obsidian中编辑博客"
date: "2026-02-26T10:50:32+08:00"
draft: false
---
> 一个方便的博客编辑方案

在完成[[一个免费博客方案]] 后，我们已经有了一个基于 hugo 的博客。
现在我们要通过 obsidian 获得更好的编辑体验。

1. 创建一个新仓库，目录为 博客项目中的 `content` 目录
2. 配置一个模板 "hugo-new-file-template", 内容如下：
```
---
title: "{{title}}"
date: "{{date:YYYY-MM-DDThh:mm:ss+08:00}}"
draft: false
---
```

3. 新建文件， 使用模板



注意：
首次提交可能需要先创建分支, 避免使用 `main` 分支， 频繁触发构建。

```
git checkout -b obsidian-branch
git push --set-upstream origin obsidian-branch
```