<p align="center"><img src="assets/prisel-mark.svg" width="88" alt=""></p>
<h1 align="center">PRISEL</h1>
<p align="center">在你自己的电脑上读代码、跑命令、改文件的 agent。终端、浏览器和手机连到同一个会话。<br>
A coding agent that reads code, runs commands and edits files on your own computer. Terminal, browser and phone attach to the same session.</p>
<p align="center"><a href="https://prisel.app">prisel.app</a> · <a href="CHANGELOG.md">更新日志 Changelog</a> · <a href="https://github.com/nerslm/prisel-release/issues">反馈 Issues</a></p>

这个仓库放 Prisel 的更新日志和问题反馈，不含源码。

## 安装

需要 Node.js 22.19 或更新版本。支持 Linux（x64、arm64）、macOS（Apple 芯片、Intel）和 Windows（x64）。

```bash
npm install -g @nerslm/prisel
prisel            # 在当前目录打开交互会话
prisel web        # 在浏览器里打开同一个会话宿主
prisel update     # 更新到最新版本
```

- 终端和网页连着同一个会话宿主，关掉窗口任务也继续跑。
- 两种后端：Prisel 自己的运行时，或者你电脑上已安装的 Claude Code。
- 子 agent、后台任务和工作流；按模式和规则确认 agent 的操作。

## 在手机和其他设备上用

```bash
prisel host remote login --server https://prisel.app   # 打开给出的链接，用你的账号确认这台电脑
prisel host remote enable
```

然后在任何设备上打开 [prisel.app](https://prisel.app)。对话和文件留在你的电脑上，浏览器和电脑之间端到端加密。

## 反馈

- Bug 和建议：[Issues](https://github.com/nerslm/prisel-release/issues)。
- 安全问题请不要公开发，见 [SECURITY.md](SECURITY.md)。

## 许可

Prisel 是专有软件，保留所有权利，按 [Prisel 条款](https://prisel.app/terms)使用，见 [LICENSE](LICENSE)。它包含的第三方组件及其许可列在 [THIRD_PARTY_NOTICES.txt](https://prisel.app/licenses/THIRD_PARTY_NOTICES.txt) 里，程序也附带一份。

---

## English

This repository holds Prisel's changelog and issue tracker. It contains no source code.

**Install.** Node.js 22.19 or newer, on Linux (x64, arm64), macOS (Apple silicon, Intel) or Windows (x64).

```bash
npm install -g @nerslm/prisel
prisel            # an interactive session in the current directory
prisel web        # the same session host in your browser
prisel update     # update to the latest release
```

- The terminal and the browser attach to one session host; closing a window does not stop the work.
- Two backends: Prisel's own runtime, or Claude Code installed on your computer.
- Subagents, background tasks and workflows; the agent's actions are confirmed by mode and rule.

**On your phone and other devices.** Run `prisel host remote login --server https://prisel.app`, confirm the computer with your account at the link it prints, then `prisel host remote enable`, and open [prisel.app](https://prisel.app) anywhere. Conversations and files stay on your computer; traffic between the browser and the computer is end-to-end encrypted.

**Feedback.** Bugs and suggestions go to [Issues](https://github.com/nerslm/prisel-release/issues); report security problems privately as described in [SECURITY.md](SECURITY.md).

**License.** Prisel is proprietary software, all rights reserved, used under the [Prisel Terms](https://prisel.app/terms); see [LICENSE](LICENSE). The third-party components it includes and their licenses are listed in [THIRD_PARTY_NOTICES.txt](https://prisel.app/licenses/THIRD_PARTY_NOTICES.txt), which also ships with the program.
