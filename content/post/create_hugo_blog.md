---
title: "Hugo와 Github page로 블로그 만들기"
date: 2020-01-16T13:48:40+09:00
description: "Hugo를 사용해서 Github page에 개인 블로그 만들기"
categories:
  - "Development"
tags:
  - "Hugo"
  - "Blog"
sidebar: true
comments: true
authorbox: true
toc: true
---


블로그를 만들 계획은 1년 전 딱 이맘때 Github의 Github page를 사용해서 블로그를 만드는 방법을 배우고 나서부터다. 그때 만드는 방법이 간단해서 '언제든지 만들면 되겠지'하고 지난 시간이 1년이었다. 그리고 지금 새로운 해의 첫 달이 절반이나 지나서야 블로그를 만들었다.
<!--more-->

---
## Static Site Generator 선택

1년 전에 배운 블로그를 만드는 방법은 지금 와서는 상세하게 기억하지 못한다. 그래서 문서화의 중요성을 더욱더 뼈저리게 느끼며 다른 사람들이 정리한 Github page 블로그를 만드는 방법을 찾아 보았다.

블로그를 만들기 위해 많은 사람이 Static site generator를 사용하고 있었고 대표적인 Static site generator로는 Jekyll, Hexo, Hugo 등이 있었다. 그리고 내가 만들 블로그는 Hugo를 사용하기로 했다.

Static site generator 선택에서 Jekyll과 Hugo 중 무엇을 사용할지 고민을 많이 했다. Jekyll은 내가 이용하고자 하는 Github page에서  대표적으로 지원하고 있어서 Jekyll 프로젝트를 Github에 올리기만 해도 자동으로 빌드해서 웹페이지를 띄어준다. 그러다 보니 많은 사람이 Github page를 이용하면 Jekyll을 사용하고 있었고, Jekyll 사용자들이 정리한 문서, 만들어둔 테마가 많았다. 하지만 나는 Hugo를 선택했고, 그 이유는

- [StaticGen](https://www.staticgen.com/)에서 Hugo가 Jekyll보다 Github 별이 많고 증가 폭도 컸다.

  GitHub의 별의 수로 사용하는 개발자의 수를 어림짐작할 수 있다. 그리고 2020년 1월 기준으로  Jekyll보다 Hugo의 별의 수가 앞서고 있었다. 그러다 보니 Hugo 또한 사용자들이 정리한 문서를 쉽게 찾을 수 있었고 테마 또한 다양하게 있었다.

- Windows를 지원한다.

  나는 많은 개발자가 사용하는 Mac을 가지고 있지 않다. 사용하는 운영체제는 Windows다 보니 Windows 지원 여부는 주요한 선택 기준 중 하나이다. Jekyll은 Windows를 공식적으로는 지원하지 않아 Windows 환경에서 사용하기 위해서는 조금 번거로운 과정이 필요로 했다. 하지만 Hugo는 Windows를 공식적으로 지원하고 있어 간단하게 설치하고 사용할 수 있다.

- 빌드 속도가 빠르다.

  Hugo의 공식 페이지에서 이야기하는 장점 중 하나이며 많은 Hugo 사용자들이 Hugo를 선택한 이유이기도 하다. Jekyll은 Github에서 자동으로 빌드해 주지만 작성한 글이 많아질수록 빌드의 속도가 느려진다고 한다. 하지만 Hugo는 따로 빌드하고 GitHub에 올려야 하지만 빌드의 속도는 빠르다고 한다.

이렇게 3가지 이유로 나는 Hugo를 선택했다. 그리고 Hugo를 선택한 후에 React를 사용하는 Gatsby가 눈에 띄었지만, 블로그를 만드는 것을 Gatsby를 사용하기 위해 다시 미루는 것보다 빨리 시작하는 것이 중요하기에 Gatsby는 다음 기회로 미루었다.

---
## Hugo 설치

Hugo는 Windows를 공식적으로 지원하기에 Hugo 사이트에서 상세하게 설명하고 있다.

[Windows에서 Hugo 설치하기](https://gohugo.io/getting-started/installing/#windows)

또한 Youtu 영상을 보고 따라하면 쉽게 설치가 가능하다.

{{< youtube G7umPCU-8xc >}}
#

---
## Hugo 프로젝트 시작하기

설치를 완료하고 터미널창에서

```cmd
$ hugo version
```

이 정상적으로 작동한다면 이제 프로젝트를 시작해보자.

프로젝트들을 만들어둘 폴더를 만들고 터미널에서 그 폴더의 경로로 들어가

```cmd
$ hugo new site <프로젝트 이름>
```

을 실행하면, 입력한 프로젝트 이름으로 기본적인 구조가 잡혀진 프로젝트 폴더가 만들어 진다.

---
## 테마 추가하기

Hugo는 다양한 테마를 적용하여 빠르게 원하는 블로그 또는 사이트를 만들 수 있다.

[Hugo의 다양한 테마](https://themes.gohugo.io/)

마음에 드는 테마를 찾았다면 Download를 클릭하면 해당 테마의 Git 페이지로 넘어간다. 그리고 프로젝트 폴더안의 `\themes` 폴더에서

```cmd
추가한 테마 원본을 수정하고 싶다면
$ git clone <테마 git 주소>

또는

추가한 테마 원본의 수정 없이 업데이트만 추적하고 싶다면
$ git submodule add <테마 git 주소>
```

를 실행하여 테마를 추가하고 `config.toml`에

```toml
theme = "<추가한 테마 폴더 이름>"
```

을 추가하면 테마가 적용된다.

여기서 주의 할 점은 폴더의 이름을 추가한다는 점이다.  
예로 들어 `\themes\hugo_theme`라면

```toml
theme = "hugo_theme"
```

을 추가하면 된다.

참고로 테마를 추가했다면 해당 테마의 README 또는 데모 사이트를 꼭 보는게 좋다. 테마마다 `config.toml` 설정과 작성할 글의 `Front Matter` 설정이 조금씩 다르기 때문이다.

---
## 블로그 미리보기

테마가 적용된 블로그를 보고싶다면

```cmd
$ hugo server -D
```

를 실행하자. 그러면 `http://localhost:1313`에 접속하여 만들어진 블로그를 볼 수 있다. 참고로 `-D` 옵션은 문서중 `draft: true`인 아직 작업중인 문서도 보여준다는 뜻이다. `draft: true`가 있는 문서는 빌드과정에 포함되지 않기 때문에 문서가 빌드 되기를 원한다면 문서의 `Front Matter`에서 지워야한다.

그리고 Hugo는 이렇게 실행한 로컬서버는 종료하고 다시 실행하지 않아도 변경사항이 있다면 자동으로 변경사항이 바로 적용된다.

---
## 블로그에 글 추가하기

Hugo에서 글을 추가하고 싶다면 프로젝트 폴더에서

```cmd
$ hugo new <파일이름>.md
```

를 실행하면 `\content`폴더에 `파일이름.md` 문서가 만들어진다. 그리고 파일의 경로를 지정하면 그 경로가 웹페이지 경로가 되는데 예로 들어

```cmd
$ hugo new post/<파일 이름>.md
```

을 실행하면 `\content\post\파일이름.md`가 생성되고 웹페이지 경로는 `baseURL\post\파일이름`이 된다.

이러한 경로설정은 적용한 테마에 따라 조금씩 추가되거나 변경될 수 있어 적용한 테마의 README 또는 데모 사이트를 참고하면 된다.

---
## 빌드하고 Github page에 올리기

Hugo를 Github page에 올리기 위해서는 빌드하는 과정이 필요하다. 그래서 Hugo 프로젝트를 저장할 Repository와 Github page의 Repository, 이렇게 두 개의 Repository가 필요하다.

먼저 프로젝트를 저장할 Repository의 이름은 원하는 이름으로 만들고 프로젝트 폴더에 Remote하면 된다.

```cmd
$ git init
$ git remote add origin <Hugo 프로젝트 Repository URL>
```

를 프로젝트 폴더에서 실행하면 프로젝트 폴더와 Hugo 프로젝트를 저장할 Repository는 서로 연결된다.

다음으로 Github page의 Repository를 만들어야한다. 중요한 점은 이번 Repository의 이름은 꼭 `<GithubID>.github.io`로 만들어야한다. 여기서 `GithubID`는 본인의 Github ID를 뜻한다.

만들어진 Github page의 Repository는 프로젝트를 빌드하면 생성되는 `\public`폴더와 연결해야한다. 하지만 이 폴더는 처음 Repository에 포함되는 경로기 때문에 처음 Repository의 Submodule로 지정해야 한다.

```cmd
$ git submodule add -b master <Github Page의 Repository URL> public
```

를 실행하면 된다. 참고로 마지막에 public을 입력하여 `\public` 폴더를 자동으로 생성하기 때문에 프로젝트 폴더에 `\public` 폴더를 미리 생성할 필요는 없다.

이제 빌드를 하면 된다. 빌드는

```cmd
$ hugo -t <사용하는 테마 폴더 이름>
```

을 실행하면 `\public` 폴더에 빌드된 결과가 생성된다.

마지막으로 프로젝트 폴더에서 한 번, `\public` 폴더에서 한 번

```cmd
$ git add .
$ git commit -m "<커밋 메세지>"
$ git push origin master
```

를 하면 `https://<GithubID>.github.io`에서 완성된 블로그를 확인할 수 있다.

---
## 참고

- [Hugo 공식 사이트](https://gohugo.io/)

- [IALY`s BLOG | 블로그 구축기 1 (Hugo + github.io)](https://ialy1595.github.io/post/blog-construct-1/)

- [Integerous DevLog | Hugo로 github.io 블로그 만들기](https://ryan-han.com/post/etc/creating_static_blog/)
