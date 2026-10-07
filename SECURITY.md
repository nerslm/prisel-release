# 安全问题 · Security

发现安全漏洞时，请不要发公开 issue。在本仓库的 Security 页点「Report a vulnerability」私下报告：<https://github.com/nerslm/prisel-release/security/advisories/new>。

请写清受影响的版本、复现步骤和影响，不要附上真实的密钥、令牌或别人的数据。

范围是 Prisel 程序，以及 prisel.app 的入口和中转。Prisel 以你的用户身份运行，权限确认不是系统沙箱；要先能改你的文件、环境或配置才成立的问题，不算 Prisel 的漏洞。

---

Please do not open a public issue for a security vulnerability. Report it privately with "Report a vulnerability" on this repository's Security tab: <https://github.com/nerslm/prisel-release/security/advisories/new>.

Include the affected version, steps to reproduce and the impact. Do not attach real keys, tokens or other people's data.

The scope is the Prisel program and the prisel.app entry and relays. Prisel runs as your user, and its permission prompts are not an operating-system sandbox; a problem that needs prior write access to your files, environment or configuration is not a vulnerability in Prisel.
