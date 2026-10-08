<a href="https://prisel.app"><picture><source media="(prefers-color-scheme: dark)" srcset="assets/hero-dark.svg"><img src="assets/hero-light.svg" alt="PRISEL, terminal service for agents" width="100%"></picture></a>

<p align="center"><a href="https://github.com/nerslm/prisel-release"><picture><source media="(prefers-color-scheme: dark)" srcset="assets/lang-en-on-dark.svg"><img src="assets/lang-en-on-light.svg" alt="English" height="30"></picture></a><a href="README.zh-CN.md"><picture><source media="(prefers-color-scheme: dark)" srcset="assets/lang-zh-off-dark.svg"><img src="assets/lang-zh-off-light.svg" alt="简体中文" height="30"></picture></a></p>

<h3 align="center">Your computer's agent, from anywhere.</h3>

<p align="center">Prisel reads code, runs commands and edits files on your own computer.<br>Terminal, browser and phone attach to the same session, and it keeps working when you close the window.</p>

<p align="center"><a href="https://prisel.app"><picture><source media="(prefers-color-scheme: dark)" srcset="assets/signin-en-dark.svg"><img src="assets/signin-en-light.svg" alt="Sign in to prisel.app" height="42"></picture></a>&nbsp;&nbsp;<a href="CHANGELOG.md"><picture><source media="(prefers-color-scheme: dark)" srcset="assets/changelog-en-dark.svg"><img src="assets/changelog-en-light.svg" alt="Changelog" height="42"></picture></a></p>

This repository holds Prisel's changelog and issue tracker. The source code is not here.

## Install

Node.js 22.19 or newer, on Linux (x64, arm64), macOS (Apple silicon, Intel) or Windows (x64).

```bash
npm install -g @nerslm/prisel
prisel            # an interactive session in the current directory
prisel web        # the same session host in your browser
prisel update     # update to the latest release
```

- The terminal and the browser attach to one session host; closing a window does not stop the work.
- Two backends: Prisel's own runtime, or Claude Code installed on your computer.
- Subagents, background tasks and workflows; the agent's actions are confirmed by mode and rule.

## On your phone and other devices

```bash
prisel host remote login   # scan the code it shows with your signed-in phone: the computer joins your account and the phone can use it
```

Then open [prisel.app](https://prisel.app) on any device. Your computer lets in only devices you paired: one more is added by scanning the code `prisel host remote pair` shows, or by a paired phone scanning the code it shows. Conversations and files stay on your computer; traffic between the browser and the computer is end-to-end encrypted.

## Feedback

- Bugs and suggestions: [Issues](https://github.com/nerslm/prisel-release/issues).
- Report security problems privately, as described in [SECURITY.md](SECURITY.md).

## License

Prisel is proprietary software, all rights reserved, used under the [Prisel Terms](https://prisel.app/terms); see [LICENSE](LICENSE). The third-party components it includes and their licenses are listed in [THIRD_PARTY_NOTICES.txt](https://prisel.app/licenses/THIRD_PARTY_NOTICES.txt), which also ships with the program.
