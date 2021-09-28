---
layout: post
title:  Jekyll 개발 환경 구축 및 블로그 생성
date:   2021-03-19 10:00:35 +0300
image:  pexels-rachel-claire-4993161.jpg
tags:   Resources
---
### Command-Line Tools
터미널을 열고 아래와 같이 입력하여 [Command-Line Tools]를 설치합니다.
```
$ xcode-select --install
```
Command-Line Tools를 설치해야 되는 이유는 Xcode 없이 맥에 '명령어 라인 도구[Command Line Tools]를 설치하는 방법에 잘 설명된 문구가 있어 차용해봤습니다.

> 맥 운영체제에서 'gcc' 'make' 같은 컴파일 툴이나 'svn' 'git' 같은 분산 버전 관리툴, 또는 기본적인 Unix/Linux 툴킷을 사용하려면 기본적으로 홈브류(Homebrew)나 명령어 라인 도구'[Command Line Tools]'을 먼저 설치해야 합니다.

### Homebrew 설치
Homebrew를 설치합니다. Homebrew는 Ruby를 설치하기 위해 필요하며, 만약 Homebrew가 이미 설치되어 있다면 건너뛰어도 괜찮습니다.
```
$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```
### Ruby 설치


Homebrew를 사용하여 Ruby를 설치합니다.

```
$ brew install ruby
```
Shell 설정에 Ruby 경로를 추가합니다. Ruby 경로를 추가해야 터미널에서 Ruby 명령어를 사용할 수 있습니다.

```
$ echo 'export PATH="/usr/local/opt/ruby/bin:$PATH"' >> ~/.bash_profile

```
Ruby와 Gem이 잘 설치되어 있는지 확인합니다.

```
$ ruby -v
```
ruby 2.6.3p62 (2019-04-16 revision 67580) [universal.x86_64-darwin19]

```
$ gem -v
```

3.0.3
Jekyll 설치
Gem을 사용하여 Jekyll을 설치합니다.

```
$ sudo gem install -n /usr/local/bin/ jekyll
```

Jekyll이 잘 설치되어 있는지 확인합니다.

```
$ jekyll -v
```

jekyll 4.1.0
Jekyll 프로젝트 생성 및 구조 파악
Jekyll 명령어를 사용하여 프로젝트를 생성합니다. --blank 옵션을 주게되면 테마가 없는 빈 프로젝트가 생성됩니다.
```
$ jekyll new my-blog --blank
```
New jekyll site installed in /path/to/my-blog.


프로젝트가 생성된 디렉토리로 이동하여 Jekyll 프로젝트를 실행합니다. --port 옵션을 따로 주지 않으면 기본적으로 4000 포트에서 실행됩니다.
```
$ cd my-blog
$ jekyll serve
```

http://localhost:4000/로 접속하여 Jekyll 프로젝트가 정상적으로 동작하는지 확인합니다.

### 디렉토리 구조
프로젝트를 생성하면 아래와 같이 디렉토리가 구성됩니다. _site는 Jekyll 프로젝트를 실행하면 웹 사이트 구동에 필요한 모든 파일들이 동적으로 생성되는 디렉토리이므로 설명을 생략하겠습니다.
```
.
├── _config.yml
├── _data
├── _drafts
├── _includes
├── _layouts
├── _posts
├── _sass
├── assets
└── index.md
```


### File/Directory	Description
_config.yml	프로젝트에 사용될 환경 변수를 정의합니다.
_data	사용자 정의 데이터 파일을 관리합니다.
_drafts	아직 배포하고 싶지 않은 포스트들을 관리합니다.
_includes	레이아웃에 공통으로 사용하는 HTML 파일을 관리합니다.
_layouts	레이아웃을 정의한 HTML 파일을 관리합니다.
_posts	배포할 포스트들을 관리합니다.
_sass	SASS 파일을 관리합니다.
assets	웹 사이트 구동에 필요한 정적 파일들을 관리합니다.
index.md	Index 페이지를 정의합니다.


### Jekyll 블로그 시작
본격적으로 Jekyll 블로그를 시작하려고 합니다. 홈 화면에서는 포스트 리스트를 출력하고 포스트를 클릭하면 상세 화면으로 이동할 수 있도록 레이아웃을 구성합니다.

index.md 파일을 열고 아래와 같이 수정합니다. _layouts/home.html 파일에 정의된 레이아웃을 사용하겠다는 의미입니다.
```
---
layout: home
---
```


### 레이아웃
레이아웃은 블로그마다 다른 형태를 지니겠지만 기본적으로 아래와 같은 형태를 지닙니다.

{% raw %}
```
<!DOCTYPE html>
<html>
{% include head.html %}
<body>
    {% include header.html %}
    <!-- main -->
    {% include footer.html %}
</body>
</html>
```
{% endraw %}

공통으로 사용하는 파일들은 _includes 디렉토리 하위에서 관리할 수 있습니다. 이는 코드의 중복을 방지하고 유지보수에 유리하도록 합니다.

home.html
_layouts 디렉토리 하위에 home.html 파일을 생성합니다. 위에서 정의한 템플릿을 복사한 뒤 <-- main --> 부분을 아래처럼 수정합니다.

{% raw %}

<ul>
    {% for post in site.posts %}
    <li>
        <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
    </li>
    {% endfor %}
</ul>
{% endraw %}

### post.html
_layouts 디렉토리 하위에 post.html 파일을 생성합니다. 위에서 정의한 템플릿을 복사한 뒤 <-- main --> 부분을 아래처럼 수정합니다.

{% raw %}
```
<section class="post">
    <h1>{{ page.title }}</h1>
    {{ content }}
</section>
```
{% endraw %}

### 포스트 작성
포스트는 _posts 디렉토리 하위에 YYYY-MM-DD-POST-TITLE.md와 같은 형태의 파일로 관리할 수 있습니다. _layouts/post.html 파일에 정의된 레이아웃을 사용할 수 있도록 명시하고 간단한 내용을 아래처럼 작성합니다.
```
---
layout: post
title: Hello World!
---

Hello World!

```


터미널을 열고 프로젝트의 루트 디렉토리로 이동하여 프로젝트를 실행합니다.

$ jekyll serve
http://localhost:4000/로 접속하여 홈 화면에 작성한 포스트가 있는지 확인합니다. 해당 포스트를 클릭하여 상세 화면으로 넘어가는지도 확인합니다.



### draft 작성
아직 배포하고 싶지 않은 포스트는 _drafts 디렉토리 하위에 POST-TITLE.md와 같은 형태의 파일로 관리할 수 있습니다. 배포되지 않기 때문에 jekyll serve 명령을 사용하더라도 _site 디렉토리 하위에 파일로 생성되지 않습니다. 로컬 환경에서 해당 포스트를 확인하고 싶다면 아래와 같이 입력하면 됩니다.

$ jekyll serve --draft


### Github 배포
Github은 Jekyll로 웹 사이트를 구축할 수 있는 Github Page를 제공합니다. 위에서 실습한 Jekyll 프로젝트를 GitHub에 배포해보도록 하겠습니다.

GitHub에서 create a new repository 버튼을 클릭하여 [username].github.io라는 이름의 저장소를 생성합니다. 반드시 자신의 username을 사용하여 [username].github.io라는 이름으로 생성해야 합니다.

터미널을 통해 생성한 저장소를 가져온 뒤 해당 디렉토리로 이동합니다.


```
$ git clone https://github.com/[username]/[username].github.io
$ cd [username].github.io
```


위에서 생성한 Jekyll 프로젝트를 모두 복사한 다음 원격 저장소에 업로드합니다.


```
$ git add --all
$ git commit -m "publish jekyll blog"
$ git push -u origin master
```


정상적으로 업로드가 되었다면 https://[username].github.io에 접속하여 Jekyll 블로그가 정상적으로 호스팅 되는지 확인하면 됩니다! 사이트가 구동되는 데에 시간이 조금 걸릴 수 있습니다.
