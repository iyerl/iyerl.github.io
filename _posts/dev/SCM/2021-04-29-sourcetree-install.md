---
layout: post
title:  "[Sourcetree] 설치 및 Github 연동"
subtitle:   "git 형상관리"
categories: dev
tags: scm sourcetree install git
image:
  path: /assets/img/dev/scm/210429-header.PNG
description : >
    소스트리 v3.4.4 설치, github 연동
---

<!--more-->

## SourceTree
- Atlassian에서 개발한 GUI버전 GIT 형상관리 툴

* this unordered seed list will be replaced by the toc
{:toc .large-only}

## 설치
1. 소스트리 사이트에서 프로그램 다운로드   
SourceTree 홈페이지에서 Windows용 설치 프로그램을 **다운로드**한다.    
![소스트리 다운로드](/assets/img/dev/scm/210429-sourcetree-download.PNG)   
[SourceTree](https://www.sourcetreeapp.com/)   
{:.figure}   

1. Altassian 계정 로그인 (skip)
BitBucket Server나 BitBucket 계정이 있을 경우 로그인한다. 그러나 필수는 아니므로 여기서는 **생략**.
![계정 로그인](/assets/img/dev/scm/210429-sourcetree-1.PNG)   

1. Mercurial 설정 해제
Mercurial 체크를 **해제**하고 다음 버튼을 클릭한다.
![Mercurial 해제](/assets/img/dev/scm/210429-sourcetree-2.PNG)   

1. Preference
사용자명과 이메일을 입력한다.
![Mercurial 해제](/assets/img/dev/scm/210429-sourcetree-3.PNG)   

1. SSH Key 설정
다른 사람들과의 공유 Git 저장소에 접근할 경우 SSH Key가 필요하다(git 설치 후 git bash에서 ssh-keygen을 입력하면 .ssh 폴더에 자동 생성). 그러나 여기서는 필요없기 때문에 **"아니오"**를 클릭한다.
![Mercurial 해제](/assets/img/dev/scm/210429-sourcetree-4.PNG)   

## GitHub 연동
1. 원격 저장소 계정 추가
**Remote > 계정 추가**를 클릭한다.
![Mercurial 해제](/assets/img/dev/scm/210429-sourcetree-5.PNG)   

1. Github 호스팅 계정 편집
호스팅 주소를 **"GitHub"**로 설정 후 **"OAuth 토큰 새로고침"**을 클릭하여 나타나는 지시에 따라 github에 로그인한다.
![Mercurial 해제](/assets/img/dev/scm/210429-sourcetree-6.PNG)   

1. Github 호스팅 계정 설정 마무리
모든 작업을 완료한 후 "확인" 버튼을 클릭한다.
![Mercurial 해제](/assets/img/dev/scm/210429-sourcetree-7.PNG)   

1. Github 레퍼지토리 호출
**새로고침**을 클릭하여 자신의 GitHub Repository 전체를 불러온 후, 로컬에 불러올 Repository에 **Clone**을 클릭한다.
![Mercurial 해제](/assets/img/dev/scm/210429-sourcetree-8.PNG)   

1. Github 호스팅 계정 설정 마무리
저장소의 종류가 "Git 저장소입니다"로 표시되는 것을 확인 후, 로컬에 저장할 폴더를 지정하고 **클론**을 클릭한다.
![Mercurial 해제](/assets/img/dev/scm/210429-sourcetree-9.PNG)  

1. Github 연동 확인
선택한 Repo가 무사히 Clone되어 로컬 영역에 복사되었다!
![Mercurial 해제](/assets/img/dev/scm/210429-sourcetree-10.PNG)  