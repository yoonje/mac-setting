# Mac 초기 환경 셋업

## Homebrew

#### 설치
```sh
$ /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
```

#### 확인
```sh
$ brew doctor
```

## Git

#### 설치
```sh
$ brew install git git-lfs
```

#### 설정
```sh
$ git config --global user.name "Your Name"
$ git config --global user.email "you@your-domain.com"
$ git config --global core.precomposeunicode true
$ git config --global core.quotepath false
```

## iTerm2

##### 설치
```sh
$ brew cask install iterm2
```

##### 설정
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
## ZSH / OH-MY-ZSH

##### 설치
```sh
$ brew install zsh zsh-completions
```
```sh
$ sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

##### 플러그인 설치
```sh
$ git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```
```sh
$ git clone git://github.com/zsh-users/zsh-autosuggestions $ZSH_CUSTOM/plugins/zsh-autosuggestions
```

##### 설정
```sh
$ vi ~/.zshrc
```
```
ZSH_THEME="agnoster"

plugins=(
  git
  zsh-syntax-highlighting
  zsh-autosuggestions
)
```

##### D2Coding 폰트 설치
https://github.com/naver/d2codingfont 다운로드

##### 설정
`Preference` -> `Profile` -> `Text` -> `Font`에서 D2Coding 선택

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
    prompt_newline //이부분을 추가 꼭 순서 지켜서
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
- IDE에도 반영
`Preferences`에서 `Tools` -> `Terminal`에 간 후 Shell path를 `/bin/zsh`로 수정

## 개발환경
- VS CODE
- Pycharm
- Postman
- IntelliJ
- Jetbrain Toolbox

## 유료 유틸리티
- KakaoTalk
- Yoink
- HW Viewer
- Office 365

## 유료 유틸리티
- Magnet
- Alfred
- i Stat
- Parallels
- App Cleaner & Uninstaller
