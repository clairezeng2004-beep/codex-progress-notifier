# Codex Progress Notifier

一个给 Codex 桌面应用用的 macOS 本地提醒小工具。

它会在后台检查 Codex 窗口的可见状态：当 Codex 不在最前面，并且窗口里出现“需要授权/允许/批准”或“完成/finished/done”等状态时，右上角会弹出系统通知。你回到 Codex 后，通知会自动清掉。

## 使用

启动：

```sh
"/Users/claire/coding project/codex-progress-notifier/bin/start"
```

停止：

```sh
"/Users/claire/coding project/codex-progress-notifier/bin/stop"
```

查看日志：

```sh
open "$HOME/Library/Application Support/CodexProgressNotifier"
```

## 第一次运行需要打开的权限

1. `系统设置 > 隐私与安全性 > 辅助功能`
   允许你用来启动它的终端应用。这个权限用于读取 Codex 窗口里可见的按钮和文字。
2. `系统设置 > 通知`
   允许来自“终端”或 `terminal-notifier` 的通知。

## 点击通知回到 Codex

macOS 自带的 `display notification` 能弹通知，但点击后的行为由系统限制，不一定能稳定激活指定应用。

想要更完整的“点击通知直接回到 Codex”，安装 `terminal-notifier` 后重启本工具即可：

```sh
brew install terminal-notifier
"/Users/claire/coding project/codex-progress-notifier/bin/stop"
"/Users/claire/coding project/codex-progress-notifier/bin/start"
```

## 可调设置

默认每 2 秒检查一次。可以在启动前设置：

```sh
export CODEX_NOTIFY_POLL_SECONDS=3
"/Users/claire/coding project/codex-progress-notifier/bin/start"
```

如果你的 Codex 进程名不同，可以设置：

```sh
export CODEX_APP_NAME="Codex"
```

## 局限

Codex 当前没有公开的本地任务事件接口，所以这个工具使用 macOS 辅助功能读取窗口中的可见文字来判断状态。它不会读取隐藏的推理内容，也不会记录完整对话，只会根据可见按钮和状态词生成很短的提醒。
