复制：Ctrl + Shift + C
粘贴：Ctrl + Shift + V
看历史输出：Ctrl + Shift + H
跳到上一条命令：Ctrl + Shift + Z
跳到下一条命令：Ctrl + Shift + X
New tab
	

ctrl+shift+t (also ⌘+t on macOS)

Close tab
	

ctrl+shift+q (also ⌘+w on macOS)


修改bash开头
export PS1='\n\[\e[1;32m\]\u@\h\[\e[0m\]:\[\e[1;34m\]\w\[\e[0m\]\$ '
\n：提示符前先空一行
\e[1;32m：绿色
\u：用户名，比如 agiuser
\h：主机名，比如 5CG5482LZ8
\w：当前路径，比如 ~/isaac_projects
\$：普通用户显示 $，root 显示 #
\e[0m：颜色恢复默认
agiuser@5CG5482LZ8:~/isaac_projects$

是 bash 的提示符，变量叫 PS1。
<img width="494" height="113" alt="图片" src="https://github.com/user-attachments/assets/7222c29d-2c3b-49d9-8d0b-077adb1e2ca2" />



七、建议你再配一下 kitty 外观

如果你觉得 kitty 默认太黑太素，可以改它的配置。

1. 打开 kitty 配置文件
mkdir -p ~/.config/kitty
gedit ~/.config/kitty/kitty.conf
2. 先放一份简单好看的配置
font_size 14.0

background #1e1e2e
foreground #cdd6f4

selection_background #44475a
selection_foreground #f8f8f2

cursor #f5e0dc
cursor_text_color background

window_padding_width 10
enable_audio_bell no
confirm_os_window_close 0
shell_integration enabled
3. 保存后重载

在 kitty 里按：

Ctrl + Shift + F5

less操作
可以，我直接按你现在这个场景来讲。

你按了 **`Ctrl+Shift+G`** 之后，kitty 会把那条命令的输出放到一个 **pager** 里看。
这个 pager 通常就是 **less**，所以翻页操作基本按 **less** 的习惯来。

---

# 一、`Ctrl+Shift+G` 之后怎么上下翻页

进入那个界面后，常用键是这些：

## 上下滚动

* **向下翻一行**：`↓`
* **向上翻一行**：`↑`

## 按页翻

* **下一页**：`Space`
* **上一页**：`b`

这个最常用，记住这两个就够了：

* `Space`：往下翻一页
* `b`：往上翻一页

## 半页翻动

* **下半页**：`d`
* **上半页**：`u`

## 到开头/结尾

* **到开头**：`g`
* **到结尾**：`G`

## 搜索

* **向下搜索关键字**：`/关键字`
* 回车确认
* **找下一个匹配**：`n`

## 退出

* **退出 pager**：`q`

---

# 二、最实用的一套你先记住

你先只记这几个：

* `Space`：下一页
* `b`：上一页
* `g`：到最上面
* `G`：到最下面
* `/`：搜索
* `q`：退出

这套已经够你平时看长输出了。

---

# 三、怎么配置“复制输出”

你这张图里已经提到了一个非常实用的配置：

```conf
mouse_map right press ungrabbed mouse_select_command_output
```

它的意思是：

**右键点击某条命令的输出区域时，自动选中整条命令的输出。**

这个很适合你。

---

## 1. 打开 kitty 配置文件

在终端里输入：

```bash
mkdir -p ~/.config/kitty
gedit ~/.config/kitty/kitty.conf
```

如果不用 gedit，也可以：

```bash
nano ~/.config/kitty/kitty.conf
```

---

## 2. 把下面这几行加进去

我建议你直接加这一组：

```conf
# Right click selects current command output
mouse_map right press ungrabbed mouse_select_command_output

# Open last visited command output in pager
map f1 show_last_visited_command_output

# Scroll to previous/next prompt
map ctrl+shift+z scroll_to_prompt -1
map ctrl+shift+x scroll_to_prompt 1
```

---

## 3. 保存后重新加载配置

在 kitty 里按：

```text
Ctrl + Shift + F5
```

如果没反应，就把 kitty 关掉再打开。

---

# 四、配置好后怎么复制输出

## 方法 1：右键整块选中，再复制

配置好后：

1. 先用 `Ctrl+Shift+Z` 跳到你想要的那条命令附近
2. **右键点击那条命令的输出区域**
3. 它会自动选中这一整块输出
4. 然后按：

```text
Ctrl + Shift + C
```

就复制了

这个是最适合你的方式。

---

## 方法 2：先打开输出，再手动选中复制

如果你按了：

```text
Ctrl + Shift + G
```

在 pager 里看输出，通常可以：

* 鼠标拖选
* 然后 `Ctrl+Shift+C`

但不同环境里，pager 里鼠标体验不一定总是最顺手。
所以对你来说，**右键整块选中再复制**更实用。

---

# 五、你可能会遇到的一个问题

你现在文档里这一句：

```conf
mouse_map right press ungrabbed mouse_select_command_output
```

只负责：

**选中命令输出**

它**不会自动复制到剪贴板**。
所以你还需要再按一次：

```text
Ctrl + Shift + C
```

---

# 六、你要的“尽量傻瓜式”方案

我建议你最终就这样用：

## 看上一条输出

```text
Ctrl + Shift + G
```

## 在终端里快速定位上一条命令

```text
Ctrl + Shift + Z
```

## 右键选中整条命令输出

配置：

```conf
mouse_map right press ungrabbed mouse_select_command_output
```

## 复制

```text
Ctrl + Shift + C
```

---

# 七、再给你一套完整可直接贴的 kitty.conf 片段

你可以把下面这段直接加到 `~/.config/kitty/kitty.conf`：

```conf
# Appearance
font_size 14.0
background #1e1e2e
foreground #cdd6f4
selection_background #44475a
selection_foreground #f8f8f2
cursor #f5e0dc
cursor_text_color background
window_padding_width 10
enable_audio_bell no
confirm_os_window_close 0
shell_integration enab思想led

# Prompt navigation
map ctrl+shift+z scroll_to_prompt -1
map ctrl+shift+x scroll_to_prompt 1

# Browse command output
map f1 show_last_visited_command_output

# Right click selects current command output
mouse_map right press ungrabbed mouse_select_command_output
```

保存后按：

```text
Ctrl + Shift + F5
```

---

# 八、最后帮你总结成最短操作流程

你以后想复制某次长输出，可以这样：

1. `Ctrl+Shift+Z` 跳到那条命令附近
2. 右键点输出区域
3. `Ctrl+Shift+C` 复制
4. 发给我

如果你想在 pager 里浏览：

1. `Ctrl+Shift+G`
2. `Space` 下一页
3. `b` 上一页
4. `q` 退出

---

如果你愿意，我下一条可以直接给你一份：

**“适合你现在 Ubuntu + kitty + bash 的完整配置文件”**

你只要整份复制进去就能用了。

