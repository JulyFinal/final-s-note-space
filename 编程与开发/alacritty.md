# Alacritty Option
#Alacritty
[from source](https://zhuanlan.zhihu.com/p/436024560)
```shell
live_config_reload: true
tabspaces: 4
window.opacity: 0.60

shell:
  program: /bin/zsh
  args:
    - --login

window:
  # 窗口大小
  dimensions:
    columns: 120
    lines: 60

  # 边缘空白
  padding:
    x: 10
    y: 15
  dynamic_padding: false
  startup_mode: Maximized
  # 窗口修饰
  # - full: 有边界+标题栏
  # - none: 无边界+标题栏
  decorations: none

scrolling:
  # 历史保留行数
  history: 2000

  # 每次滚动行数
  multiplier: 20

  # 每次滚动行数（分屏时）
  faux_multiplier: 100

  # 自动滚动至最新行
  auto_scroll: true


font:
  size: 10
  # 字体
  normal:
    family: 'FiraCode Nerd Font'
    style: Regular
  bold:
    family: 'FiraCode Nerd Font'
    style: Bold
  italic:
    family: 'FiraCode Nerd Font'
    style: Italic
  bold_italic:
    family: 'FiraCode Nerd Font'
    style: Bold Italic
  # 细描边
  use_thin_strokes: true

key_bindings:
  - { key: C, mods: Command, action: Copy }
  - { key: V, mods: Command, action: Paste }
  - { key: N, mods: Command, action: SpawnNewInstance }
  - { key: W, mods: Command, action: Quit }

cursor:
  # Cursor style
  #
  # Values for `style`:
  #   - Block
  #   - Underline
  #   - Beam
  style: Beam
  unfocused_hollow: true

custom_cursor_colors: true

debug:
  # Display the time it takes to redraw each frame.
  render_timer: false

  # Keep the log file after quitting Alacritty.
  persistent_logging: false

  # Log level
  #
  # Values for `log_level`:
  #   - Off
  #   - Error
  #   - Warn
  #   - Info
  #   - Debug
  #   - Trace
  log_level: Warn

  # Print all received window events.
  print_events: false
```
