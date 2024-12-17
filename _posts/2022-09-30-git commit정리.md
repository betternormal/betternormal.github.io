---
layout: post
author: "praconfi"
tags: git
title: "커밋 개수, 내용 깔끔하게 정리(fixup, squash)"
---

> git rebase기능을 이용해 커밋들의 순서를 변경할수 있고, 작은 커밋들을 병합, 수정할 수 있다  
> 이를 이용해 commit들을 정리하면 깔끔한 커밋 기록을 남길 수 있다

# 1. 현재 브랜치에서 아래 명령어 입력
```
$ git rebase -i master (또는 main)
$ git rebase -i HEAD~3 (최근 3개의 커밋)
```

# 2. 커밋 수정, 병합
## 1. 위치조정
VIM에서 `dd(cut)`, `p(paste)`(uppercase)를 이용해 커밋의 순서를 변경

## 2. 커밋 병합, 수정
### fixup
```
pick 1aab3a 원본 커밋 메세지
fixup 70c0cc 합칠 커밋 메시지
=> 원본 커밋메세지만 남음
```
### squash
```
pick 1aab3a 원본 커밋 메세지
squash 70c0cc 합칠 커밋 메시지
=> 두개의 커밋메세지가 줄바꿈되어 합쳐진다
```
### reword
```
pick을 reword로 변경한 후 :wq  
이후 나오는 화면에서 커밋메세지 변경
한번에 여러개도 가능하다
```
## 3. 저장및 종료
```
:wq
```

# 3. 원격브랜치 업데이트
```
$ git push origin 브랜치명 -f
```

## Ref
- [ref](https://shinsunyoung.tistory.com/93)