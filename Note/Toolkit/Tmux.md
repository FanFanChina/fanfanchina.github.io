# 层级

**会话  > 窗口 > 格子**

# 会话

```python
# 新建会话(session), 并支持中文显示
tmux -u new -s 会话名称
# 查看所有会话
tmux ps
# 连接上一个会话
tmux a
# 连接指定会话
tmux a -t sessionName
# 修改会话名称
tmux rename -t 原名 目标名称
# 断开当前会话
tmux detach
前缀 + d
# 关闭会话
进入后 exit
tmux kill-session -t xxx
# 关闭所有会话
tmux kill-ser
```

# 窗口

```python
# 新建窗口
前缀 + c
# 切换窗口
前缀 + 窗口标号 || 前缀 + p / n
```

# 格子(分屏)

| 前缀 + % | 横分屏 |
| --- | --- |
| 前缀 + “ | 竖分屏 |
| 前缀 + 上/下/左/右 | 向上/下/左/右 切换格子 |

# 命令模式

```bash
前缀 + : # 进入命令模式
source-file ~/.tmux.conf # 刷新配置
```

# 配置文件

```bash
set-option -g status-keys vi
setw -g mode-keys vi

setw -g monitor-activity on

# setw -g c0-change-trigger 10
# setw -g c0-change-interval 100

# setw -g c0-change-interval 50
# setw -g c0-change-trigger  75

set-window-option -g automatic-rename on
set-option -g set-titles on
set -g history-limit 100000

#set-window-option -g utf8 on

# set command prefix
set-option -g prefix C-a
unbind-key C-b
bind-key C-a send-prefix

bind h select-pane -L
bind j select-pane -D
bind k select-pane -U
bind l select-pane -R

bind -n M-Left select-pane -L
bind -n M-Right select-pane -R
bind -n M-Up select-pane -U
bind -n M-Down select-pane -D

bind < resize-pane -L 7
bind > resize-pane -R 7
bind - resize-pane -D 7
bind + resize-pane -U 7

bind-key -n M-l next-window
bind-key -n M-h previous-window

set -g status-interval 1
# status bar
set -g status-bg black
set -g status-fg blue

#set -g status-utf8 on
set -g status-justify centre
set -g status-bg default
set -g status-left " #[fg=green]#S@#H #[default]"
set -g status-left-length 20

# mouse support
# for tmux 2.1
# set -g mouse-utf8 on
set -g mouse on
#
# for previous version
#set -g mode-mouse on
#set -g mouse-resize-pane on
#set -g mouse-select-pane on
#set -g mouse-select-window on

#set -g status-right-length 25
set -g status-right "#[fg=green]%H:%M:%S #[fg=magenta]%a %m-%d #[default]"

# fix for tmux 1.9
bind '"' split-window -vc "#{pane_current_path}"
bind '%' split-window -hc "#{pane_current_path}"
bind 'c' new-window -c "#{pane_current_path}"

# run-shell "powerline-daemon -q"

# vim: ft=conf
```