---
title: 개발 환경 설정하기
tags:
- iOS 개발 환경
- MacBook Pro
- Apple M1 Pro
---

iOS 개발 환경과 맥북에 설정하면 편리한 기능을 정리해 봅니다.
:information_desk_person: :computer:

<!--more-->

- [프로그램](#프로그램)
- [편리한 설정](#편리한-설정)
- [참고자료](#참고자료)

# 프로그램
## 개발 관련

### [Xcode](https://developer.apple.com/kr/xcode/)
> iOS 개발을 위해서 따로 말이 필요 없는 프로그램

- 사용 방법
    + Mac App Store 에서 앱 다운로드 및 사용
    + [다운로드 사이트](https://developer.apple.com/download/all/) 를 통해서 특정 버전을 따로 설치 가능

- 설정

`Themes 에서 원하는 색상 테마와 폰트 선택하기`{:.info}
![xcode theme-1](/attachments/2022-03-25/xcode-setting-1.png){:width="700px"}
    
`Locations > Derived Data 를 Relative 로 변경해서 사용하기`{:.info}
![xcode theme-2](/attachments/2022-03-25/xcode-setting-2.png){:width="700px"}

### [Visual Studio Code](https://code.visualstudio.com)
> 텍스트 편집기로 Sublime Text 보다 더 좋은 것 같음

- 사용 방법
    + 사이트를 통해서 앱 설치

### [iTerm2](https://iterm2.com)
> 맥의 터미널 보조 프로그램으로 터미널 보다 사용하기 편함

- 사용 방법
    + 사이트를 통해서 앱 설치

### [Oh My ZSH](https://ohmyz.sh)
> 쉘(Shell)을 더 쉽게 사용해주는 플러그인

- 사용 방법

```zsh
# 설치
$ sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

- 설정

`테마 변경하기`{:.info}
```zsh
# macOS 의 기본 쉘인 zsh 파일 Visual Studio Code 편집기로 열기
## 다른 편집기를 사용해도 상관 없음
$ open -a Visual\ Studio\ Code ~/.zshrc

# 파일에서 ZSH_THEME 부분을 원하는 테마로 변경
## 예시: ZSH_THEME="refined"

# zsh 재실행하기
$ exec zsh
```

- 관련 링크
    + [테마 찾아보기](https://github.com/ohmyzsh/ohmyzsh/wiki/Themes)
    + [Oh My ZSH+ iTerm2로 터미널을 더 강력하게](https://medium.com/harrythegreat/oh-my-zsh-iterm2로-터미널을-더-강력하게-a105f2c01bec)
    + [터미널 초보의 필수품인 Oh My ZSH!를 사용하자](https://nolboo.kim/blog/2015/08/21/oh-my-zsh/)


### [Homebrew](https://brew.sh)
> 맥에서 라이브러리나 플러그인등을 쉽게 설치하게 도와주는 패키징 매니저

- 사용 방법

```zsh
# 설치
$ /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# 설치 시 shallow clone 이 발생 시 아래 실행 (터미널 메시지 확인 필요)
$ git -C /usr/local/Homebrew/Library/Taps/homebrew/homebrew-core fetch --unshallow
$ git -C /usr/local/Homebrew/Library/Taps/homebrew/homebrew-cask fetch --unshallow

# 업데이트
$ brew update
 
# 청소
$ brew cleanup
 
# 문제 진단
$ brew doctor
 
# doctor 진단 시 링크 이슈가 있는 경우 대응 방법
$ brew unlink {package}
$ brew link --overwrite {package} (or brew link --overwrite --dry-run {package})
```

- 관련 링크
    + [[Homebrew] brew 명령어 모음집](https://sukvvon.tistory.com/7)

### [CocoaPods](https://cocoapods.org)
> Swift and Objective-C 라이브러리의 의존성 관리 매니저

- 사용 방법

```zsh
# 설치
$ brew install cocoapods
 
# 버전 확인
$ pod --version
```

- 관련 링크
    + [CocoaPods 유용한 정보 모음](https://github.com/ClintJang/cocoapods-tips)

### [Fastlane](https://fastlane.tools)
> Ruby 기반 앱 자동 빌드 오픈소스 라이브러리

- 사용 방법

```zsh
# 설치
$ brew install fastlane
 
# 버전 확인
$ fastlane --version
```

## 유틸리티
### [App Cleaner](https://freemacsoft.net/appcleaner/)
- 맥에서 앱을 삭제하는 프로그램
- 앱 삭제 시 모든 관련 파일을 삭제할 수 있어서 좋음

### [Get Plain Text](https://apps.apple.com/kr/app/get-plain-text/id508368068?mt=12)
- 복사한 글자의 서식을 지우는 프로그램
- Copy & Paste 시에 텍스트만 가져올 수 있기에 유용함

### [The Unarchiver](https://apps.apple.com/kr/app/the-unarchiver/id425424353?mt=12)
- 압축 해제 프로그램
- 분할 압축 해제 등을 지원하고 있어서 유용함

### [Magnet 마그넷](https://apps.apple.com/kr/app/magnet-마그넷/id441258766?mt=12)
- 맥의 실행 중인 앱들을 단축키로 빠르게 화면 분할해서 볼 수 있는 프로그램
- `유료`{:.warning} 앱 이지만 써보면 편리성 때문에 후회하지 않음


# 편리한 설정
## OSX 설정
```zsh
# Finder - 숨김 파일 디폴트 보기
$ defaults write com.apple.finder AppleShowAllFiles true; killall Finder

# Dock - 아이콘 아래에 indicator 표시
$ defaults write com.apple.dock show-process-indicators -bool true; killall Dock

# Dock - 앱 숨김 시 반투명 표시
$ defaults write com.apple.dock showhidden -bool yes; killall Dock

# Dock - 최근 사용 앱 표시
$ defaults write com.apple.dock persistent-others -array-add '{"tile-data" = {"list-type" = 1;}; "tile-type" = "recents-tile";}'; killall Dock

# 맥세이프 - 연결 시 소리 재생
$ defaults write com.apple.PowerChime ChimeOnAllHardware -bool true; open /System/Library/CoreServices/PowerChime.app &
```
`info`{:.info}    
Finder 앱에서 숨김 파일 보기/숨김 단축키
`Command` + `Shift` + `.`
{:.info}

## 터미널 설정
### zsh
#### 기본 쉘 변경하기
```zsh
# 기본 쉘이 bash 인 경우 zsh 로 변경
$ chsh -s /bin/zsh
```

#### 별칭(alias) 설정
```zsh
# .zshrc 파일 열기
$ open -a Visual\ Studio\ Code ~/.zshrc

# 파일에 별칭 추가
## 예시: alias cddev="~/Downloads/my/develop" // 경로 이동
## 예시: alias gitlog="git log --oneline --decorate --graph --all" // git log 출력

# zsh 재실행하기
$ exec zsh
```

### Git
#### 텍스트 편집기 변경
```zsh
# Visual Studio Code 사용
$ git config --global core.editor "/Applications/Visual\ Studio\ Code.app/Contents/Resources/app/bin/code --wait"
```

#### PR(Pull Request) 브랜치 포인터 보기
```zsh
# remote(origin) 의 PR 내용이 보이도록 설정
$ git config --add remote.origin.fetch '+refs/pull-requests/*/from:refs/remotes/origin/pr/*'
```

## 시스템 환경설정
### 키보드
- 한/영 단축키 변경
    + 입력 소스 > 이전 입력 소스 선택 : `Command` + `Space`
    + Spotlight > Spotlight 검색 보기 : `Control` + `Space`

![system keyboard](/attachments/2022-03-25/system-keyboard.png){:width="700px"}

- 키보드로 팝업 버튼 선택하기
    + 하단 **키보드 탐색을 사용하여 컨트롤 간에 초점 이동** 체크
    + OS 팝업에서 `Tap` 키로 버튼 이동 후 `Space` 로 선택 가능

# 참고자료
- M1 맥북 프로 설정 : [macOS/iOS 개발 환경 설정하기](https://medium.com/codesquad-kr/macos-ios-개발-환경-설정하기-180dab308d31)
- OSX 기본 설정 방법 : [OSX defaults setttings](https://gist.github.com/sohooo/3199249)