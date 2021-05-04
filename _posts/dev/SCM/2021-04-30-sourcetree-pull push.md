---
layout: post
title:  "[Sourcetree] Git 작업 순서"
subtitle:   "git 형상관리"
categories: dev
tags: scm sourcetree git components status push pull
image:
  path: /assets/img/dev/scm/2021-04-30-header.png
description : >
    git의 3가지 컴포넌트, git 상태, git 작업 순서
---

<!--more-->
0. this ordered seed list will be replaced by the toc
{:toc .large-only}

## Git의 구성요소
![GIT의 3가지 컴포넌트](/assets/img/dev/scm/2021-04-30-git-status.png)

### 1. 작업트리 (Work-Tree / Working Directory)
- 프로젝트의 특정 버전을 Checkout한 것
- 현재 작업 중인 디렉토리 폴더   
- 수정가능하며 읽을 수 있는 모든 파일이 들어 있는 컴포넌트
- 파일 상태 : **Modified**

### 2. 인덱스 (Index / Staging Area)
- git 명령어 : `git add <filename>`, `git add --all`
- commit 되기 전 준비 단계가 보존되는 컴포넌트 (Git Directory에 존재)  
- 작업트리에 있는 파일 중 (1)변경 사항이 있으며 (2)commit할 파일들   
  - 모든 변경된 파일 중 commit할 파일을 선택하는 작업 : **인덱스에 등록**, **스테이징**
  - 인덱스라는 가상 공간이 중간에 존재함으로써 작업 트리 내에 commit이 필요없는 파일을 제외하고 원하는 일부 변경 사항만 등록해 commit할 수 있음
- 파일 상태 : **Staged**

### 3. 저장소 (Repository / Container / Git Directory)
#### 3-1. 로컬 저장소 (Local Repository)
- git 명령어 : `git commit`
- 모든 commit된 파일들의 History를 snapshot의 형태로 보유
- 파일 상태 : **Commited**

#### 3-2. 원격 저장소 (Remote Repository)
- git 명령어 : `git push origin master`
- 로컬 저장소에 commit된 파일들을 push 명령어를 통해 원격 저장소로 전달   

## Git 프로젝트 작업 순서
### 1. Pull
- 원격 저장소(github)의 변경된 데이터를 가져오는 git 명령어
- 원격 저장소의 버전을 가져와, 로컬 저장소와 **병합(merge)**되어 새로운 버전이 만들어지기 때문에 충돌이 일어날 수 있음   
- <u>**새로운 작업을 시작하기 전**</u>에, 반드시 Pull 명령어를 실행하여 원격 저장소에 새로운 내용이 있는지 확인
  - pull 없이 새로운 작업을 수행하여 원격 저장소에 push를 할 경우, git은 push를 거절   

#### 1-1. pull 작업 SourceTree 튜토리얼
1. SourceTree에서 Pull 버튼을 클릭 
![pull 버튼 클릭](/assets/img/dev/scm/2021-04-30-pull-1.png)   

1. SourceTree에서 Pull 관련 설정을 확인 
![pull 버튼 클릭](/assets/img/dev/scm/2021-04-30-pull-2.png)    

1. SourceTree에서 Pull이 완료된 History 확인
- 원격 저장소(origin/master)와 로컬 저장소(master)가 버전이 같아진 것을 확인할 수 있다.   
![pull 버튼 클릭](/assets/img/dev/scm/2021-04-30-pull-3.png)    

### 2. 작업 (로컬)
- 데이터의 생성/수정/삭제 등 필요한 작업을 로컬에서 수행한다.

### 3. Commit
- 원격저장소로 변경사항을 push하기 전, 인덱스의 파일들을 local repository로 변경 이력을 저장하는 git 명령어
#### 3-1. commit 작업 SourceTree 튜토리얼
1. "스테이지에 올라가지 않은 파일"에서 변경 사항이 있는 모든 파일들을 확인한다. 리스트를 클릭하면 우측하단에서 변경된 log를 볼 수 있다. **모두 스테이지에 올리기**"를 클릭하거나 commit할 파일들을 복수 선택하여 "**선택 내용 스테이지에 올리기**"를 클릭한 후, 좌측 상단의 ""**Commit**" 버튼을 클릭한다.
![Staging & Commit](/assets/img/dev/scm/2021-04-30-commit-1.png)   

1. "스테이지에 올라가지 않은 파일"에서 변경 사항이 있는 모든 파일들을 확인한다. 리스트를 클릭하면 우측하단에서 변경된 log를 볼 수 있다. **모두 스테이지에 올리기**"를 클릭하거나 commit할 파일들을 복수 선택하여 "**선택 내용 스테이지에 올리기**"를 클릭한 후, 좌측 상단의 ""**Commit**" 버튼을 클릭한다.
![Staging & Commit](/assets/img/dev/scm/2021-04-30-commit-2.png)  
### 4. pull
- 원격 저장소에 push 하기전에 pull을 한 번 더 실행하여 로컬 작업 중 원격 저장소가 업데이트된 경우를 대비한다.
- 
### 5. push


## Reference
[Git Documentation 1.3 시작하기 - Git 기초](https://git-scm.com/book/ko/v2/%EC%8B%9C%EC%9E%91%ED%95%98%EA%B8%B0-Git-%EA%B8%B0%EC%B4%88)