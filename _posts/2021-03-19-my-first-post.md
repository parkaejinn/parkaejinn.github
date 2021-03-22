---
layout: post
title:  블로그 포스팅하는 방법
date:   2021-03-19 10:00:35 +0300
image:  pexels-rachel-claire-4993161.jpg
tags:   Resources
---

## 1. Visual Studio Code 실행 
***
Jekyll 테마 내용물들이 들어 있는 GithubID.github.io 이름의 로컬 폴더를 열어준다.
<br><br>
## 2. _posts 폴더 생성
***
1. 모든 포스트 파일은  _posts 위치해야 한다.

2. GithubID.github.io 이름의 로컬 폴더 위치에 _posts 폴더가  없다면 생성해 준다.
<br><br>
## 3. yyyy-mm-dd-title.md 형식의 파일 생성
***
1. md는 포스트 파일의 확장자
  
2. ex) 2020-05-23-my-first-post.md
<br><br>
## 4.  포스트의 정보를 머릿말에 작성 
***
__--- 를 써서 머릿말 쓰는 영역을 구분해준다__ 

*---*

title:  " [Jekyll] 블로그 포스팅하는 방법 " 

excerpt: " md 파일에 마크다운 문법으로 작성하여 Github 원격 저장소에 업로드하고 에디터는 Visual Studio code 사용! 로컬 서버에서 확인. "

categories:
  - Blog
tags:
  - [Blog, jekyll, Github, Git]

toc: true
toc_sticky: true
 
date: 2020-05-25
last_modified_at: 2020-05-25 

*---*

* title : 포스트의 제목을 큰 따옴표로 적어 준다. title을 작성하지 않을 시 .md 파일 이름으로 적어주었던 title 부분이 제목으로 업로드 된다.

* excerpt : 포스트 목록에서 보여지는 블로그 소개 글로 들어가는 것 같다.
  
  

* toc : Table of Contents. 포스트의 헤더들만 보여주는 목차 사용여부를 물어보는 것이며 ture 로 해주면 포스트의 목차가 보이게 된다.
<br>
<br>  
## 5.포스트 내용을 Markdown 문법으로 작성
***

머릿말이 ---로 끝난 이후부터는 포스트 본문 영역

<br>
<br>

## 6. 작성한 포스트 파일을 git push 하여 Github Pages 서버에 업로드 하기
***
  1. Commit 아이콘을 클릭.
 2. Commit시 남길 메모를 입력하고 엔터 
    + repository에 반영한 것이 어떤 작업인지 작성
3. 이제 깃허브에 업로드
   + Visual Studio Code 아래쪽에 보이는 TERMINAL 창을 선택
   + 보이지 않는 경우 메뉴에서 View > Terminal을 선택
  
4. repository 페이지에 방문하여 Clone or download 버튼을 클릭하여 URL을 복사
5. git remote add origin __본인 URL__
 ex)git remote add origin https://github.com/parkaejinn/parkaejinn.github.io.git
   + 원격 repository 주소를 지정해주는 것이다
6. git pull origin master --allow-unrelated-histories
   + 깃허브에 있는 내용을 로컬 repository에 반영 해주는 것이다. 
7.git push -u origin master
<br>

+ ### *GithubID.github.io 폴더 내의 변동 사항*

1. _post 폴더가 새로 생성
   
2. _post 폴더 안 에 .md 파일이 새로 생성
<br><br>



+ ### *로컬 서버에서 블로그에 적용될 모습 확인하기 Permalink*
<br>
1. 명령 프롬프트 cmd를 켜고 cd로 GithubID.github.io 폴더로 이동한다.
   <br>
2. bundle exec jekyll serve 명령어를 입력하면 로컬 환경에서 jekyll 서버가 가동된다.
   <br> 
3. 작성 중인 .md 파일을 저장하고 웹 브라우저를 열고 http://127.0.0.1:4000 로 접속하면 적용될 모습을 미리 확인해볼 수 있다.
   <br> 
4. .md 파일을 저장해야 로컬 서버에 반영이 된다. 
   <br>
5. 로컬 서버가 가동 중인 cmd를 켜놓고 http://127.0.0.1:4000/ 페이지를 새로 고침하여 현재 작성 중인 글이 블로그에서 어떻게 보여질지 확인하며 포스트를 작성한다.




---
layout: post
title: VSCode에서 Github 연동하기 
date:   2021-03-22 10:00:35 +0300
image:  pexels-antonius-ferret-5254320.jpg
tags:   Resources
---

## 1. Local Folder지정
***
VSCode에서 사용할 특정 폴더를 선택

![img](./.png)

## 2. Git 초기화 
***
(1) VSCode 메뉴 → 소스제어 메뉴를 선택 → Repository 초기화 선택

![img](./)

(2) 초기화 버튼 선택하면 Local/LocalFoder.png아래와 같은 화면이 표시되고 원하는 폴더를 선택 

![img](./Git초기화.png)

(3) 자신의 Window 폴더 경로로 이동하면 _.git_ 폴더가 생성된다

![img](./Local/LocalFoder.png)

(4) VSCode 소스 제어 메뉴에도 변경된다

![img](./Local/LocalFoder.png)

## 3. Git Stage 관리
***

(1) 파일을 생성할려면 test.txt 파일을 생성 →  좌측메뉴의 탁색기 버튼 클릭  →  파일을 추가 →  소스제어 아이콘에 _1_ 표시

![img](./Local/LocalFoder.png)

(2) 소스제어 메뉴를 선택 →  _+_ (변경 내용 스테이징) 선택하면 Stage 처리 

![img](./Local/LocalFoder.png)

(3) 변경 된 내용 확인

![img](./Local/LocalFoder.png)

(4) _..._  클릭하면 git과 관련된 여러가지 작업 수행가능 

![img](./Local/LocalFoder.png)

## 4. Git Commit 
***

Stage에올라간 내용은 Commit 명령어를 통해 GitHub에 반영된다.

VSCode 소스 제어 아래 메뉴를 선택하면 된다.

```
git commit -m "test commit" 터미널에 입력한 것과 동일 
```

![img](./Local/LocalFoder.png)

## 5. Remote원격 Repository
***
(1) Github에 원격 Repository를 미리 생성해둔 경우 rmote repository에 연결

![img](./Local/LocalFoder.png)

(2) 본인 ID와 PW를 입력하면 VSCode와 GitHub가 정상적으로 연결




