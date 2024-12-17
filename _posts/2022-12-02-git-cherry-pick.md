---
layout: post
author: "praconfi"
tags: git
title: "필요한 커밋만 빼오기(cherry pick)"
---

> git cherry-pick 기능을 이용해 다른 브랜치에서 원하는 커밋만 가져올 수 있다  

## 커밋을 가져오고 싶은 브랜치에 가서 commit id 확인
```bash
$ git checkout other-branch
$ git log --oneline

# 원하는 commit id를 적어둔다
```

## 커밋을 가져올 브랜치로 이동후, 체리픽
```bash
$ git checkout new-branch
$ git cherry-pick COMMIT-ID
```