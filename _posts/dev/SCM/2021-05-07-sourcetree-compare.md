---
layout: post
title:  "[Sourcetree] 외부 비교 - Visual Code"
subtitle:   "git 형상관리"
categories: dev
tags: scm sourcetree git VisualCode
image:
  path: /assets/img/dev/scm/2021-05-07-header.png
description : >
    SourceTree, 그리고 Compare 도구로써 Visual Code
---

<!--more-->
0. this ordered seed list will be replaced by the toc
{:toc .large-only}

## Git Diff
- `git diff <branch명> <비교할 branch명>`
- 두 파일을 비교하여 코드 상의 차이점을 보여주는 명령어
- 로컬 branch 간, 로컬과 원격, commit 간의 파일을 비교할 수 있음
- sourcetree에서는 History의 우측하단에 수정된 코드를 표시해주며, 외부 비교도구를 연동하여 `git diff`의 기능 수행이 가능
  - 가장 널리 쓰이는 도구는 **Beyond Compare**로, 유료이지만 빠르고 쉽게 파일과 폴더를 비교(Compare) 및 병합(Merge)할 수 있다.
  - Windows 전용 무료 오픈 소스인 **WinMerge** 또한 자주 쓰이는 파일 비교 유틸이다.
  - **Visual Code**는 Microsoft사의 무료 오픈소스 코드 에디터로, 기존에 사용하고 있는 IDE이고 사용하기 편리하며 익숙하기 때문에 선택하였다.

## 외부 비교 도구로 Visual Code를 연동하는 SourceTree 튜토리얼
### 설정
1. SourceTree에서 [도구(Tools)] > [옵션(Options)] 클릭
![도구-옵션 클릭](/assets/img/dev/scm/2021-05-07-compare-setting-1.png)   

1. [비교(Diff)] 탭에서 [외부/비교 병합] 란에 "외부 비교도구"와 "병합도구"를 모두 **커스텀**으로 선택한다.
![비교 탭 설정](/assets/img/dev/scm/2021-05-07-compare-setting-2.png)   

1. 경로를 Visual Code의 설치경로로 설정하고, 각 변수를 그림과 같이 기입한다.
- Visual Code 경로 : C:\Users\사용자\AppData\Local\Programs\Microsoft VS Code\Code.exe
- 명령어 : 외부 비교 도구에서 실행하는 명령어 / 커스텀이 아닌 경우 생략 가능
  - diff 명령어 :  -n -w -d $LOCAL $REMOTE
  - 병합 명령어 : -n -w $MERGED   
  - Visual Code 명령어   
      1. -n
      - 기존에 열려 있는 탭이 있을 경우 새 창을 열지 않음
      1. -w, --wait
      - Git은 실행 중인 VS Code가 닫힐 때까지 대기
      - Git의 편집기로 사용할 때 유용
      1. -d, --diff path1 path2
      - path1과 path2 파일을 비교
      1. $LOCAL : 로컬 경로
      1. $REMOTE : 원격 경로
      1. $MERGED : mergetool 설정
![도구 선택 및 변수 작성](/assets/img/dev/scm/2021-05-07-compare-setting-3.png)    

### 비교 실행
1. Sourcetree 내부 비교 창의 톱니바퀴 모양의 버튼을 눌러 [외부 비교도구]를 클릭한다.
![외부 비교도구 클릭](/assets/img/dev/scm/2021-05-07-compare-execute-1.png)   
   
2. VS Code가 자동으로 실행되어 좌측에 기존 파일, 우측에 수정된 파일 및 변경 사항에 대한 GUI 표시가 나타난다.
![VS 자동실행 화면](/assets/img/dev/scm/2021-05-07-compare-execute-2.png)
