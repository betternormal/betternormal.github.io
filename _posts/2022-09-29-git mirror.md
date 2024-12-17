---
layout: post
author: "praconfi"
tags: git
title: "레포지토리 복제하기(git mirror)"
---

> git mirror를 이용해 커밋기록을 포함해, 레포지토리를 옮긴다

## 1️. 복사할 리포지토리를 local에서 미러링 한다.
```
$ git clone --mirror <리포지토리_url>
```

## 2️. 미러링이 되면 <리포지토리> 폴더가 생기는데 해당 폴더로 이동한다.
```
$ cd 리포지토리.git
``` 

## 3. 복사를 진행할 새 레포지토리 URL을 입력하여 push 한다.
```
$ git remote set-url --push origin <new_리포지토리_URL>
``` 

## 4. 마지막으로 push
```
$ git push --mirror
```