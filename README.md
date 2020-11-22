# Mac 초기 환경 셋업

## 맥 시스템 설정

##### 알림
웬만하면 다 끄자

##### Finder
`환경설정` -> `사이드바` -> User 이름 체크

##### Dock
- Dock은 왼쪽
- 확대 X 
- 가리기 O

##### Siri 비활성화

##### 키보드
- 맞춤법 자동 수정 X
- 자동으로 문장을 대문자로 시작 X
- 스페이스를 두 번 눌러 마침표 추가 X
- Touch Bar 입력 제안 X
- Fn 키 고정
- Caps Lock 키로 ABC 입력 소스 전환 해제

##### 캘린더
구글 계정 선택 -> 구글 캘린더와 연동

## Notion

##### 구글 계정 연동

## Chrome

##### 북마크 연동

##### 계정 연동

## Homebrew

##### Homebrew 설치
```sh
$ /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
```

##### Homebrew 설치 확인
```sh
$ brew doctor
```

## Node / Yarn

##### Node 설치
```
$ brew install node
```

##### Yarn 설치
```
$ brew install yarn
```

## Git

##### Git 설치
```sh
$ brew install git git-lfs
```

##### Git 설정
```sh
$ git config --global user.name "Your Name"
$ git config --global user.email "you@your-domain.com"
$ git config --global core.precomposeunicode true
$ git config --global core.quotepath false
```

## iTerm2

##### iTerm2 설치
```sh
$ brew cask install iterm2
```

##### iTerm2 설정
- 한글 깨짐 방지
  - `Preference` -> `Profile` -> `Text` -> `Unicode normalization form`를 `NFC`로 설정
- 단어 단위 이동
  - `Preference` -> `Profile` -> `Keys` 이동 후 숏컷 추가(`+`)
  ```
  Keyboard Shorcut: ⌘ + ←
  Action: Send Escape Sequence
  Esc+: b
  ```
  ```
  Keyboard Shorcut: ⌘ + →
  Action: Send Escape Sequence
  Esc+: f
  ```
  
##### D2Coding 폰트 설치
https://github.com/naver/d2codingfont 다운로드 및 서체 설치

##### 폰트 설정
- `Preference` -> `Profile` -> `Text` -> `Font`
  - Font : D2Coding
  - Size : 14
  
##### 창 크키 설정


##### Snazzy 컬러 설치
https://github.com/yoonje/mac-setting/blob/master/Snazzy.itermcolors 다운로드

##### 컬러 설정
`Preference` -> `Profile` -> `Colors` -> `Color presets`에서 Snazzy.itermcolors import하고 설정
  
## ZSH / OH-MY-ZSH

##### ZSH / OH-MY-ZSH 설치
```sh
$ brew install zsh zsh-completions
```
```sh
$ sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

##### 플러그인 및 유틸 설치
```sh
$ git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```
```sh
$ git clone git://github.com/zsh-users/zsh-autosuggestions $ZSH_CUSTOM/plugins/zsh-autosuggestions
```
```sh
$ brew install thefuck
```

##### 플러그인 및 유틸 설정
- .zshrc 열기
```sh
$ vi ~/.zshrc
```
- .zshrc에 설정 추가
```
ZSH_THEME="agnoster"

plugins=(
  git
  zsh-syntax-highlighting
  zsh-autosuggestions
)

eval $(thefuck --alias)
```

##### 추가 작업
- 터미널 출력 변경
  - .zshrc 열기
  ```sh
  $ vi ~/.zshrc
  ```
  - .zshrc에 함수 추가
  ```
  prompt_context() {
  if [[ "$USER" != "$DEFAULT_USER" || -n "$SSH_CLIENT" ]]; then
    prompt_segment black default "%(!.%{%F{yellow}%}.)$USER"
  fi
  }
  ```
- 뉴라인 적용
  - agnoster 테마 파일 열기
  ```sh
  $ vi ~/.oh-my-zsh/themes/agnoster.zsh-theme
  ```
  - 테마 파일에 함수 추가
  ```
  build_prompt() {
    RETVAL=$?
    prompt_status
    prompt_virtualenv
    prompt_context
    prompt_dir
    prompt_git
    prompt_bzr
    prompt_hg
    prompt_newline // 이 부분을 추가 꼭 순서 지켜서
    prompt_end
  }
  prompt_newline() {
  if [[ -n $CURRENT_BG ]]; then
    echo -n "%{%k%F{$CURRENT_BG}%}$SEGMENT_SEPARATOR
  %{%k%F{blue}%}$SEGMENT_SEPARATOR"
  else
    echo -n "%{%k%}"
  fi

  echo -n "%{%f%}"
  CURRENT_BG=''
  }
  ```
- Syntax Hightlight 적용
  - 설치
  ```sh
  $ brew install zsh-syntax-highlighting
  ```
  - 적용
  ```sh
  $ source /usr/local/share/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh
  ```
- 보안 옵션
  - .zshrc 열기
  ```sh
  $ vi ~/.zshrc
  ```
  - 적용
  ```
  ZSH_DISABLE_COMPFIX="true" // source $ZSH/oh-my-zsh.sh 앞에서 
  source $ZSH/oh-my-zsh.sh 
  ```
  
##### 샘플 .zshrc에서 확인해야할 부분
```sh
export ZSH="/Users/yoonje/.oh-my-zsh" // 계정 정보 확인 필요

# Add node npm yarn
export NODE_PATH="/usr/local/lib/node_modules"
export PATH="/usr/local/Cellar/node/14.3.0/bin:$PATH" // 노드 버전 확인 필요
export PATH="$(yarn global bin):$PATH"

# Add Visual Studio Code (code)
export PATH="$PATH:/Applications/Visual Studio Code.app/Contents/Resources/app/bin"
function code () { VSCODE_CWD="$PWD" open -n -b "com.microsoft.VSCode" --args $*; }
```

##### 샘플 

## JetBrains 계열 IDE 설정 - PyCharm / IntelliJ

##### 폰트 설치
https://ko.cooltext.com/Download-Font-ubuntu / https://ko.cooltext.com/Download-Font-DejaVu+Sans+Mono 다운로드 및 서체 설치

##### 파일 인코딩
- `Preference` -> `Editor` -> `Code Style` -> `File Encodings`
  - 프로퍼티 파일 `Default encoding for properties files`: UTF-8 설정 및 Transparent native-to-ascii convention 옵션 체크

##### 폰트
- `Preference` -> `Apperance & Behavior` -> `Apperance`
  - Theme : Dracula 
  - Use custom font : Ubuntu
  - Size : 14 
- `Preference` -> `Editor` -> `Font`
  - Font : DejaVu Sans Mono
  - Size : 17
  - Line spacing : 1.2

##### 파일에 라이선스 / Author 설정

##### 쉘 설정
- `Preference` -> `Tools` -> `Terminal`
  - Application settings: /bin/zsh
  
##### 플러그인 설치
- 깃 툴박스
- CheckStyle-IDEA

## VS Code IDE 설정
  
##### 쉘 설정
- `F1` -> `Termianl: Select Default Shell`
  - /bin/zsh

##### 폰트 설정
- `Preference` -> `Setting`
  - Font Size : 17

##### 플러그인 설치
- git lens
- git history
- eslint
- prettier
- IntelliJ IDEA Keybindings

## 개발환경
- VS CODE
- Postman
- Chrome
- Jetbrain Toolbox / PyCharm
- Jetbrain Toolbox / IntelliJ
- Docker Desktop
- MySQL workbench

## 무료 유틸리티
- KakaoTalk (app store)
- HW Viewer (app store)
- MS Office 365
- Keka (web)
- IINA (web)
- Notion (web)

## 유료 유틸리티
- Magnet
- Unclutter
- Mate translater
