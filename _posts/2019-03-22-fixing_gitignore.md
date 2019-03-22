---
title: "How to fix when gitignore file is not working."
date: 2019-03-22 18:13:50 +0900
categories: git
tags:
- gitignore
---

gitignore에 무시할 파일을 등록했는데, 작동하지 않을 때,\
git의 캐시된 파일들을 다 지우고 commit하면 된다.

```bash
git rm -r --cached .
git add .
git commit -m "fixed untracked files"
```
