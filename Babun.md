
# Babun  
; Windows Shell

### 1. Babun Download & Install  
[Download Babun](http://babun.github.io/)  &&  C:\Users\UserID\\.babun\install.bat    
> _vim 에서 마우스 사용 적용하기_  
_{ ~ }  >> echo "set mouse-=a" >> ~/.vimrc_  

 
 
### 2. 업데이트 하기(update.bat 실행)    
C:\Users\UserID\\.babun\update.bat  
  

### 3. Babun Powerline Font 변경
1) theme 변경

```
vim .zshrc

ZSH_THEME=”babun”    to  ZSH_THEME=”agnoster”  

```

2) [Download PowerlineFont](https://github.com/powerline/fonts) && install
```
# clone
git clone https://github.com/powerline/fonts.git --depth=1
# install
cd fonts
./install.sh
# clean-up a bit
cd ..
rm -rf fonts
```

3) [Download Navigate Font](https://github.com/powerline/fonts/blob/master/DejaVuSansMono/DejaVu%20Sans%20Mono%20for%20Powerline.ttf) && install
```
Download 후 더블클릭 Install
```

4) Babun 설정 변경  

$ vim .minttyrc  

```
Columns = 140
Rows = 40
Font=DejaVu Sans Mono for Powerline
FontHeight = 11
Charset = UTF-8
Transparency = off
BoldAsFont = no
BoldAsColour = yes
FontSmoothing = default
Term = xterm-256color

ForegroundColour = 210, 210, 210
BackgroundColour =  20,  20,  20
CursorColour     = 255, 175,   0
IMECursorColour  = 128, 224, 160
Black            =  40,  40,  40
BoldBlack        =   0,   0,   0
Red              = 220, 135, 135
BoldRed          = 255, 135, 135
Green            = 175, 220, 135
BoldGreen        = 175, 255, 135
Yellow           = 220, 220, 175
BoldYellow       = 255, 255, 175
Blue             = 135, 175, 220
BoldBlue         = 135, 175, 255
Magenta          = 220, 175, 220
BoldMagenta      = 255, 175, 255
Cyan             = 175, 220, 220
BoldCyan         = 175, 255, 255
White            = 210, 210, 210
BoldWhite        = 230, 230, 230
````

5) babun 재시작

6) pact

# Tmux 

* Windows OS & babun  
{ ~ }  >> pact install tmux  
  
* MacOS & iTerm2  
$ brew install tmux  
  
* Ubuntu  
$ sudo apt-get install tmux  

* Centos
```centos
# Install tmux on Centos release 6.5

# install deps
yum install gcc kernel-devel make ncurses-devel

curl -OL https://github.com/libevent/libevent/releases/download/release-2.0.22-stable/libevent-2.0.22-stable.tar.gz
tar -xf libevent-2.0.22-stable.tar.gz
cd libevent-2.0.22-stable
./configure --prefix=/usr/local
make
make install

curl -OL https://github.com/tmux/tmux/releases/download/2.3/tmux-2.3.tar.gz
tar -xf tmux-2.3.tar.gz
cd tmux-2.3
LDFLAGS="-L/usr/local/lib -Wl,-rpath=/usr/local/lib" ./configure --prefix=/usr/local
make
make install

# pkill tmux
# close your terminal window (flushes cached tmux executable)
# open new shell and check tmux version
tmux -V
```
  
> _{ ~ }  >> vim [.tmux.conf](https://gist.github.com/mousavian/11df288233502e30a09b) 등록_  
_{ ~ }  >> tmux source-file ~/.tmux.conf_  
  
### 4. tmux 실행
{ ~ }  » tmux  
  
  
# Tmux
### Session
* $ tmux new -s <session-name> -n <window-name> : 새 세션 생성
* >>> ctrl + b, d  : 세션 중단하기 (detached)
* >>> ctrl + b, $  : 세션 이름 수정
* $ tmux attach -t <session-number or session-name> : 세션 다시 시작 (attach)
* >>> (tmux에서) exit   or   $ tmux kill-session -t [name]  : 세션 종료
* $ tmux ls : 세션 목록 보기 (list-session)


### Window
* Ctrl-b c : 새창을 생성합니다.
* Ctrl-b d : 현재 클라이언트에서 떨어집니다.
* Ctrl-b l : 이전에 선택한 윈도우로 이동합니다.
* Ctrl-b n : 다음 윈도우로 이동합니다.
* Ctrl-b p : 이전 윈도우로 이동합니다.
* Ctrl-b w : 윈도우의 리스트를 보여주고 번호를 입력하면 이동합니다.
* Ctrl-b 윈도우번호 : 해당 윈도우로 이동합니다.
* Ctrl-b & : 현재 윈도우를 종료합니다.
* Ctrl-b , : 현재 윈도우의 이름을 바꿉니다.

### 팬(pane) 사용하기
tmux는 윈도우뿐만 아니라 윈도우를 분할하는 팬(pane)기능도 지원합니다.

* Ctrl-b % : 세로로 2개의 팬으로 나눕니다.
* Ctrl-b " : 가로로 2개의 팬으로 나눕니다.
* Ctrl-b q : 팬 번호를 보여준다.(팬사이를 이동하는데 사용된다.)
* Ctrl-b % 를 입력하면 아래처럼 화면을 2개의 팬으로 나누어 줍니다.

tmux를 2개의 팬으로 분리한 화면

* Ctrl-b q 를 입력하면 각 팬의 번호를 보여줍니다.

tmux의 팬 번호를 확인한 화면

단축키를 이용해서 팬간의 전환을 할 수 있습니다.

* Ctrl-b o : 다음 팬으로 이동합니다.
* Ctrl-b { : 왼쪽 팬으로 이동합니다.
* Ctrl-b } : 왼쪽 팬으로 이동합니다.
* Ctrl-b 방향키 : 방향키 위치의 팬으로 이동합니다.
* Ctrl-b <alt>-방향키 : 현재 팬의 사이즈를 조정합니다.

tmux를 팬을 배치하는 여러가지 레이아웃(가로, 세로 등등)가지고 있는데 아래 단축키로 현재의 팬들을 레이아웃에 따라 순차적으로 바꾸어줍니다.

* Ctrl-b <스페이스> : 팬의 레이아웃 변경


### tmux.conf
tmux.conf 파일 설정을 통해 단축키, 창 스타일등을 변경할 수 있.  
$ vim ~/.tmux.conf

```tmux

unbind C-b                  // Ctrl+b 단축키를 해제
set-option -g prefix C-a    // Ctrl+a 를 기본동작으로 설정한다
bind-key C-a send-prefix    // 프리픽스로 Ctrl+a를 설정

# split panes using | and -
bind | split-window -h      // 창을 세로로 자르기 | 키 등록
bind - split-window -v      // 창을 가로로 자르기 - 키 등록
unbind '"'                  // 기존에 사용한 가로키 " 을 해제
unbind %                    // 기존에 사용한 세로키 " 을 해제  

# reload config file (change file location to your the tmux.conf you want to use)
bind r source-file ~/.tmux.conf; display "Reloaded"

# switch panes using Alt-arrow without prefix
bind -n M-Left select-pane -L
bind -n M-Right select-pane -R
bind -n M-Up select-pane -U
bind -n M-Down select-pane -D

## 상대바 스타일 수정
set -g status-justify left
set -g status-bg black
set -g status-fg white
set -g status-left "#[fg=green]#H"
set -g status-right "#[fg=yellow]#(uptime | cut -d ',' -f 2-)"
set -g status-interval 2

```

참조 :
https://www.sorendam.com/take-control-of-your-console-in-windows-with-babun-oh-my-zsh-and-powerline-fonts/
