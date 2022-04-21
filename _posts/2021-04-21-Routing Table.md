---
layout: post
author: "praconfi"
tags: Network
title: "Routing Table"
---

- 네트워크상의 최적의 경로를 따라 패킷이 어디로 가야하는지 설정되어 있는 테이블

- `netstat -r` 로 확인해 볼 수 있다

- 테이블에 적혀있지 않은 네트워크 대역은 찾아갈 수 없으며, `게이트웨이`로 향하게 된다

![](../assets/imgs/2021-04-21/routingTable.png)

