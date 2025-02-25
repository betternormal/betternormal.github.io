---
layout: post
author: "betternormal"
tags: 
title: "Mac에서 Window 원격접속하기(feat. Microsoft Remote Desktop)"
---


Mac에서 Windows PC로 원격 접속하는 방법은 여러 가지가 있지만, 가장 간단하고 일반적인 방법은 **Microsoft Remote Desktop (MSRD)**(Windows App으로 이름바뀜)을 사용하는 것이다.

## 1. Windows PC에서 원격 데스크톱 활성화
### Windows에서 원격 데스크톱을 활성화
설정 → 시스템 → 원격 데스크톱으로 이동  
"원격 데스크톱 활성화"를 ON으로 설정  

### Windows PC의 IP 주소 확인
Windows + R 키를 누른 후 cmd 입력  
ipconfig 입력 후 IPv4 주소 확인  
사용자 계정 권한 설정  
원격으로 접속할 사용자가 관리자 그룹에 속해 있는지 확인(Microsoft 계정을 사용한다면 이메일(example@outlook.com)을 사용자 이름으로 입력, 해당계정의 pw, 로컬계정일경우 계정이름, pin)  

관리자 권한이 필요하면 제어판 → 사용자 계정에서 설정 가능  
### Windows PC의 정확한 사용자 이름을 확인하는 방법:
Windows + R 키를 누르고 cmd 입력 후 실행  
다음 명령어 입력:  
```  
whoami  
```  
출력된 결과가 PC이름\사용자이름 형식이면, 사용자이름 부분을 사용하거나 전체를 사용할 수 있습니다.  

## 2. Mac에서 Microsoft Remote Desktop 앱 설치 및 설정
### Mac App Store에서 "Microsoft Remote Desktop" 설치

앱스토어에서 "Microsoft Remote Desktop" 검색 후 다운로드 및 설치(현재는 Windows App)
### 새로운 연결 추가
Microsoft Remote Desktop 실행 후 + 버튼 클릭 → Add PC 선택
PC name에 Windows PC의 IP 주소 입력
User account를 설정(매번 입력하거나 저장 가능)
Display 및 Sound 등 원하는 설정 조정
연결 및 원격 접속

## 3. 추가 설정 (필요한 경우)
### 같은 네트워크에서만 접속 가능:
기본적으로 같은 Wi-Fi 또는 유선 네트워크에서만 원격 접속 가능
외부에서 접속하려면 포트 포워딩 또는 VPN 설정 필요

### 방화벽 설정 확인:
Windows 방화벽에서 원격 데스크톱 서비스 (TCP 3389 포트)가 차단되지 않았는지 확인
Windows + R 키를 눌러 실행 창을 엽니다.  
control firewall.cpl 입력 후 Enter 키를 누릅니다.  
"Windows Defender 방화벽" 창이 열립니다.  
### 원격 데스크톱 허용하기  
왼쪽 메뉴에서 **"Windows Defender 방화벽을 통해 앱 또는 기능 허용"**을 클릭합니다.  
목록에서 **"원격 데스크톱"**을 찾습니다.  
"개인" 및 "공용" 네트워크 둘 다 체크되어 있는지 확인합니다.  
체크되어 있지 않다면 "설정 변경" 버튼을 클릭한 후 체크한 뒤 확인을 누릅니다.  
### 원격 데스크톱 사용자 그룹에 계정 추가하기
Windows에서는 원격 접속을 허용할 사용자 계정이 "Remote Desktop Users" 그룹에 속해야 합니다.  
🔹 사용자 추가 방법:  
Windows + R → sysdm.cpl 입력 후 실행  
"원격" 탭 클릭  
"원격 사용자 선택" 버튼 클릭  
"추가" 버튼 클릭  
"선택할 개체 이름 입력" 창에 사용자 계정 이름(로컬 계정) 입력 후 확인  
다시 확인을 눌러 설정 저장  