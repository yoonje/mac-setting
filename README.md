# Mac 초기 환경 셋업

## 맥 시스템 업데이트
Stable 버전의 최신 OS로 업데이트

## 맥 시스템 설정

##### 배터리
퍼센트 보기

##### Bluetooth
메뉴 막대에서 Bluetooth 보기 

##### 일반
- 화면 모드: 다크
- 스크롤 막대 보기: 항상

##### 알림
웬만하면 다 끄자

##### Mission Control
Spaces를 최근  사용 내역에 따라 자동으로 재정렬 체크박스를 해제

##### Finder
- `환경설정` -> `사이드바` -> User 이름 체크
- 보기 -> 계층

##### Dock
- Dock은 아래
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

## Unclutter

##### 설정
- `Unclutter Preferences` ->  `General`
  - Launch Unclutter at startup 

## Magnet

##### 설정
`환경 설정` -> 로그인 시 론칭

## Chrome

##### 북마크 연동

##### 계정 연동

##### 화면 비율 110

## Homebrew

##### Homebrew 설치
```sh
$ /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
```

##### Homebrew 설치 확인
```sh
$ brew doctor
```

##### 설정
- 설정 -> 조작 -> 단축키 1
  - opt -> cmd
  - 윈도우가 보일 곳: 모든 앱, 보이는 Space, AltTab이 보여지는 화면

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
$ git config --global core.ignorecase false
```

## iTerm2

##### iTerm2 설치
```sh
$ brew install --cask iterm2
```

##### iTerm2 설정
- 한글 깨짐 방지
  - `Preference` -> `Profile` -> `Text` -> `Unicode normalization form`를 `NFC`로 설정
- 단어 단위 이동
  - `Preference` -> `Profile` -> `Keys` 이동 후 숏컷 추가(`+`)
  ```
  Send ^[b
  Keyboard Shorcut: Opt + ←
  Action: Send Escape Sequence
  Esc+: b
  ```
  ```
  Send ^[f
  Keyboard Shorcut: Opt + →
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
- `Preference` -> `Profile` -> `Window` -> `Setting for New Windows`
  - Columns: 90
  - Rows: 30
  
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
- 플러그인 설치
  - 설치
  ```sh
  $ git clone https://github.com/zsh-users/zsh-autosuggestions ~/.oh-my-zsh/custom/plugins/zsh-autosuggestions
  $ git clone https://github.com/zsh-users/zsh-syntax-highlighting ~/.oh-my-zsh/custom/plugins/zsh-syntax-highlighting
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
  ....
)
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
  
##### 샘플 .zshrc에서 확인해야할 부분
```sh
export ZSH="/Users/user/.oh-my-zsh" // 계정 정보 확인 필요
```

## 기타

#### tree 설치
```sh
$ brew install tree
```

#### wget 설치
```sh
$ brew install wget
```

## IntelliJ 

##### 폰트 설치
https://ko.cooltext.com/Download-Font-ubuntu / https://ko.cooltext.com/Download-Font-DejaVu+Sans+Mono 다운로드 및 서체 설치

##### 프로젝트 경로 숨김
- idea.properties 열고 아래 설정 추가
```yml
project.tree.structure.show.url=false
ide.tree.horizontal.default.autoscrolling=false
```

#### import 설정
- `Preferences > Editor > Auto Import > Optimize Imports on the Fly`

#### formatting 설정
- `Actions on Save` > Reformat code, Optimize imports, Rearrange code 

##### 파일 인코딩
- `Preference` -> `Editor` -> `Code Style` -> `File Encodings` -> `Default encoding for properties files`: UTF-8 설정 및 Transparent native-to-ascii convention 옵션 체크

##### 어노테이션 프로세서
- Preference -> Build, Execution, Deloyment -> Compiler → Enable Annotation Processing 옵션 체크 

##### Doc 설정
- Preferences > Editor > File and Code Templates > Files

##### 폰트
- `Preference` -> `Appearance & Behavior` -> `Appearance`
  - Theme : Dracula 
  - Use custom font : Ubuntu
  - Size : 14
- `Preference` -> `Editor` -> `Font`
  - Font : DejaVu Sans Mono
  - Size : 14
  - Line spacing : 1.2

##### Auto import Optimize 설정
- Preferences -> Editor -> Auto import -> Optimize imports on the fly와 Add unambiguous imports on the fly 옵션 체크

##### 파일에 라이선스 / Author 설정
- Preferences -> Editor -> File and Code Templates -> Files

##### 쉘 설정
- `Preference` -> `Tools` -> `Terminal`
  - Application settings: /bin/zsh
  
##### 플러그인 설치
- Git ToolBox(License)
- CheckStyle-IDEA
- .ignore
- Indent Rainbow
- Rainbow Brackets
- SonarLint
- DTO Generator
- POJO to JSON
- Tab Shifter
- MyBatisX or JPA Buddy(License)
- Lombok

## 개발환경
- Postman
- Chrome
- Jetbrain Toolbox / IntelliJ
- visualvm
- vscode

## 무료 유틸리티
- KakaoTalk (app store)
- Notion (web)
- App cleaner (web)
- Albtab (web)

## 유료 유틸리티
- Magnet
- Unclutter
