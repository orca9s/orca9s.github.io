---
title: Jekyll로 Blog생성하기
description: <center> jekyll로 블로그를 생성하고 GitHub에서 테마를 적용시킨다.</center>
categories:
 - Setting
tags:
---

## mac에서 rbenv를 사용해 Jekyll블로그를 생성하고, 이를 GitHub에 배포하기.

## Jekyll
Jekyll : 일반적으로 블로그를 만들기 위해 사용하는 사이트 생성기이다. 포스트 형태를 `HTML` 이 아닌 마크업을 사용할 수 있으며, 데이터 베이스를 쓰지 않는다는 점은 버전관리 시스템을 사용해서 작성한 글 들을 편리하게 관리할 수 있다는 장점을 준다.

## Install
`Jekyll` 를 로컬환경에서 실행하려면 특정 버전 이상의 `Ruby`가 필요하다. mac에 기본으로 설치된 `Ruby`는 버전이 낮기 때문에, `Ruby`버전을 업그레이드 해주어야한다. `Ruby`버전을 업그레이드 하기 위해 버전관리도구인 `rbenv`를 사용한다.

## Hombrew 설치하기
mac에서 `rbenv`를 설치하기 위해서는 `Homebrew`를 사용해야한다. <br> `Homebrew`가 설치되어 있지 않다면 아래의 코드를 터미널에 입력하여 `Homebrew`를 설치 해주도록 한다.
<br>
```c
code/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install
/master/install)"
```
`Homebrew`가 이미 설치 되어 있다면 `brew update`를 사용해서 `Homebrew`를 최신버전으로 업데이트를 해주도록 한다.
## rbenv설치
아래의 코드를 사용하여 `rbenv`를 설치 해주도록 한다.
```c
brew install rbenv ruby-build
```

## rbenv를 위한 설정을 셸 설정파일에 추가하기
`zsh`를 사용하는 경우에는 `~/.zshrc`, 기본 `bash`를 쓰는 경우에는 `~/.bash_profile`에 작성한다.
```c
# rbenv
export PATH="$HOME/.rbenv/bin:$PATH"
eval "$(rbenv init -)"
```
설정파일을 추가한 후 터미널을 종료하고 새로 열어주면된다.

## rbenv를 이용해 ruby설치, 전역에서 사용할 ruby버전 지정
```c
➜ rbenv install 2.4.1
➜ rbenv global 2.4.1
➜ rbenv versions
  system
 *2.4.1 (set by /Users/JSM/.rbenv/version)
 ```
## 새ruby버전 설치 후 rehash작업
```c
rbenv rehash
```
`rehash`는 `rbenv`가 관리하는 루비 명령어들을 `~/.rbenv/shims`디렉토리에 셸 스크립트 파일로 복사해주는 역할을 한다.
새`gem`을 설치하거나 새 `ruby`버전을 설치한 경우 해당 명령을 실행해주어야 한다. 셸 설정파일에 추가한 `rbenv init -`명령어에 `rehash`기능이 포함되어있다. 터미널을 새로 열면 자동으로 `rehash`명령이 수행되니 명령어를 직접 실행하거나 새 터미널 창을 열면 된다.

## RubyGems, Gem, bundler
RubyGems는 `ruby`패키지 관리자이며, 각 패키지는`gem`이라고 불린다.<br>
설치해야할 `gem`은 `jekyll`과 `bundle`,`github-pages`이다. 일반적으로 `ruby`의 패키지들은 `rubygems`를 이용해 관리되며, 시스템 어디에서나 설치된 `gem`들을 사용할 수 있다. 하지만 프로젝트별로 필요한 각 패키지`gem`들의 버전이 다를 수 있으며, 이러한 의존성 문제를 해결하기 위해 [bundler](https://ruby-korea.github.io/bundler-site/),라는 패키지를 사용한다.`bundler`역시 `rubygem`의 패키지이다.`bundler`는 `Gemfile`과`Gemfile.lock`파일을 이용해 현재 프로젝트 폴더에서 사용하는 패키지 버전들을 관리한다.
`github-pages`는`github`에서 사용하는 `jekyll`과 관련된 의존성 패키지들을 지원하는 `gem`이다. 로컬에서 `jekyll`을 이용해서 생성할때와는 다르게, `github`에 코드를 업로드 했을 때 자동으로 사이트가 생성될때는 `github`에서 사이트가 생성되기 위한 여러 요소들이 필요한데, 이러한 부분들을 처리해주기 위한 지원 패키지 역할을 한다.
```c
gem install jekyll bundler github-pages
```

## Jekyll블로그 생성 및 로컬 실행
필요한 `gem`들을 설치한 후, `jekyll`블로그를 생성할 폴더의 상위 폴더에서 아래 명열을 실행한 후 결과를 확인 하도록 한다.
```c
➜ jekyll new 블로그명
➜ cd 블로그명
➜ ls -al
drwxr-xr-x   9 JSM  staff   306B  6 17 17:13 .
drwxr-xr-x@ 61 JSM  staff   2.0K  6 17 17:12 ..
-rw-r--r--   1 JSM  staff    35B  6 17 17:13 .gitignore
-rw-r--r--   1 JSM  staff   953B  6 17 17:13 Gemfile
-rw-r--r--   1 JSM  staff   1.2K  6 17 17:13 Gemfile.lock
-rw-r--r--   1 JSM  staff   1.4K  6 17 17:13 _config.yml
drwxr-xr-x   3 JSM  staff   102B  6 17 17:13 _posts
-rw-r--r--   1 JSM  staff   525B  6 17 17:13 about.md
-rw-r--r--   1 JSM  staff   213B  6 17 17:13 index.md
```
`jekyll`패키지 대신 `github-pages`를 사용하도록 `Gemfile`의 내용을 수정해준다.
`gem "jekyll"...`부분은 주석처리하고, `gem "github-pages"...`부분을 활성화시킨다.
```c
➜ vi Gemfile
...
# gem "jekyll", "3.4.3"
# This is the default theme for new Jekyll sites. You may change this to anything you
like. gem "minima", "~> 2.0"

# If you want to use GitHub Pages, remove the "gem "jekyll"" above and
# uncomment the line below. To upgrade, run `bundle update github-pages`.
gem "github-pages", group: :jekyll_plugins
...
```
실행 전 `bundle`로 관리되는 패키지들을 업데이트 시켜준다
```c
bundle install
bundle update
```
실제 정적 사이트를 생성하고, 테스트를 위한 로컬 서버를 실행한다.
```c
bundle exec jekyll serve
```
<http://127.0.0.1:4000>으로 접속하면 아래와 같은 페이지를 확인할 수 있다.
