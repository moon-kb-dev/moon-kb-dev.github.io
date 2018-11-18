# https://subicura.com/2017/11/22/mac-os-development-environment-setup.html
# 본격 macOS에 개발 환경 구축하기
## 분실대비 패스워드 메시지 설정
Security & Privacy > General > Show a message when the screen is locked: 전화번호 / 이름
혹시 분실했을 경우를 대비하여 전화번호, 이름 등을 알려줌

## 디스크 암호화
Security & Privacy > FileVault: Turn On FileVault
분실 시 복구 불가능하게 디스크를 암호화

## 모든 텍스트 자동 변경 옵션 끄기
Keyboard > Text: 모든 자동 변경 옵션 끄기
입력한 단어를 컴퓨터 마음대로 바꾸는 걸 방지

## 클릭은 터치로
Trackpad > Point & Click > Tab to click: 체크함
트랙패드 클릭 시 꾸욱 누를 필요 없이 톡톡 터치로 클릭해서 손의 피로를 줄임

## 드래그는 세손가락으로
Accessibility > Mouse & Trackpad > Trackpad options...: Enable dragging - three finger drag
창 또는 아이콘을 이동할 때 트랙패드를 누른 상태로 이동할 필요 없이 세 손가락으로 드래그 할 수 있음
이건 해봐야 감이 오는데 몰랐다면 신세계가 열림

## Finder를 실행하고 ⌘ + , (Finder > Preferences...)를 선택합니다.
### 파인더 기본 폴더 설정
General > New Finder windows show: subicura (home folder)
파인더 최초 실행 시 버벅임이 없도록 기본 폴더를 홈 폴더로 설정

### 파일 확장자 보여주기
Advanced > Show all filename extensions: 체크함
모든 파일의 확장자를 보여줌

## Downloads 폴더로 이동하고 ⌘ + J (View > Show View Options)를 선택합니다.
### 날짜그룹 + 이름 정렬
Arrange By:Date added, Sort By:Name
파일 목록을 보여줄 때 날짜별로 그룹화 하고 그룹 내에서 이름으로 다시 정렬
다운로드 폴더 특성상 최근에 받은 파일들을 찾는 경우가 많으므로 유용함

## 필수 프로그램
### Xcode
$ xcode-select --install
확인
$ gcc
clang: error: no input files

$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
$ brew doctor
Your system is ready to brew.

### git
$ brew install git git-lfs

$ git config --global user.name "Your name"
$ git config --global user.email "you@your-domain.com"
$ git config --global core.precomposeunicode true
$ git config --global core.quotepath false

## iTerm2
$ brew cask install iterm2

### snazzy Theme
https://github.com/sindresorhus/iterm2-snazzy/raw/master/Snazzy.itermcolors

iTerm을 실행하고 설정(⌘ + ,)창에서 Profiles 항목을 선택하고 Colors탭을 선택합니다.
오른쪽 하단에 Color presets... 선택 박스를 클릭하면 조금전에 추가한 Snazzy preset을 선택할 수 있습니다.

추가설정
타이틀바 배경색 어둡게 변경
Appearance > Theme: Dark
High Sierra에서는 현재 Light/Dark 테마만 선택할 수 있으며 임의의 색은 불가능
스크롤바 감추기
Appearance > Hide scrollbars: 체크함
타이틀바 밑에 1px 라인 제거
Appearance > Show line under title bar when the tab bar is not visible: 체크 안함
마진 수정
Advanced > Height of top and bottom margins in terminal panes: 10
Advanced > Width of left and right margins in terminal panes: 12

### zsh with oh-my-zsh
iTerm2도 설치하고 테마도 설치했으니 쉘을 바꿀 차례입니다.

$ brew install zsh zsh-completions

$ sh -c "$(curl -fsSL https:raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
설치스크립트를 실행하면 관련 파일을 설치하고 패스워드를 물어봅니다. 계정의 패스워드를 입력하면 기본쉘을 자동으로 bash에서 zsh로 변경해줍니다.

### 플러그인
oh-my-zsh의 가장 강력한 점은 플러그인입니다. 기본 플러그인외에 명령어 하이라이팅 플러그인 zsh-syntax-highlighting과 자동완성 플러그인 zsh-autosuggestions을 설치합니다.

#### zsh-syntax-highlighting
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting

#### zsh-autosuggestions
git clone git://github.com/zsh-users/zsh-autosuggestions $ZSH_CUSTOM/plugins/zsh-autosuggestions
플러그인을 설치하면 반드시 ~/.zshrc파일에 설정을 해야합니다. 파일을 열고 plugins항목에 플러그인을 추가합니다.

plugins=(
  git
  zsh-syntax-highlighting
  zsh-autosuggestions
)
설정 파일을 수정했으면 터미널을 재시작하거나 source ~/.zshrc 명령어를 실행하여 설정을 다시 불러와야 합니다. 이제 명령어를 입력할 때 존재하지 않는 명령어는 빨간색으로 뜨고 한번 입력했던 명령어를 회색으로 표현해주는 걸 확인할 수 있습니다.

### Theme
$ brew install nodejs
$ npm install --global pure-prompt

$ ~/.zshrc
$ autoload -U promptinit; promptinit
$ prompt pure

## vim -> neovim
$ brew install neo vim
$ brew tap caskroom/fonts
$ brew cask install font-hack-nerd-font

$ vi ~/.zshrc
alias vim="nvim"
alias vi="nvim"
alias vimdiff="nvim -d"
export EDITOR=/usr/local/bin/nvim
$ source ~/.zshrc

## plugins
$ curl -sLf https://spacevim.org/install.sh | bash
$ vi
(1)

## fzf
$ brew install fzf
$ $(brew --prefix)/opt/fzf/install 
y 
$ source ~/.zshrc 

## fasd 
$ brew install fasd 
$ vi ~/.zshrc 
plugins=(
    ...
    fasd
    )

$ source ~/.zshrc 

## tmux
$ brew install tmux

## tmuxinator
$ brew install ruby
$ gem install tmuxinator


# Like Application
## docker
## tig 
## jq
## ngrok
## asciinema
## neofetch


