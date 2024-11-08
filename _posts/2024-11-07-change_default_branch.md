---
layout: post
author: "betternormal"
tags: 'git'
title: "Default branch 변경하기"
---


## GitHub에서 master 브랜치를 main 브랜치로 옮기고 기본 브랜치를 main으로 변경하는 방법:

### 1. main 브랜치 생성

```bash
git checkout master
git checkout -b main
```
### 2. main 브랜치를 원격 저장소에 푸시
```bash
git push origin main
```
### 3. GitHub에서 기본 브랜치를 main으로 설정
GitHub 저장소로 이동합니다.  
Settings 탭을 클릭합니다.  
General 섹션에서 Default branch 설정을 찾아 main으로 변경합니다.  
### 4. master 브랜치 삭제 (선택 사항)
기존 master 브랜치를 더 이상 필요하지 않다면 삭제할 수 있습니다:

```bash
git push origin --delete master
```
또는 로컬에서도 삭제할 수 있습니다:  

```bash
git branch -d master
```
main 브랜치가 기본 브랜치로 설정완료!  