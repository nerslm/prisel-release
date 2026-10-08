<p align="center"><a href="CHANGELOG.md"><picture><source media="(prefers-color-scheme: dark)" srcset="assets/lang-en-on-dark.svg"><img src="assets/lang-en-on-light.svg" alt="English" height="30"></picture></a><a href="CHANGELOG.zh-CN.md"><picture><source media="(prefers-color-scheme: dark)" srcset="assets/lang-zh-off-dark.svg"><img src="assets/lang-zh-off-light.svg" alt="简体中文" height="30"></picture></a></p>

# Changelog

Changes in each Prisel release.

## [0.10.3]

### Breaking Changes

- Remote access lets a browser in only after the computer trusts it, whatever account it is signed in to. Pair each browser once per computer: scan the code `prisel host remote pair` prints (`enable` prints it while the computer trusts no device), or let a device the computer already trusts scan the code the browser shows. An entry ticket alone now reaches only that pairing step, so neither the entry nor its signing key can let a device in. Browsers that connected before pair once. The browser and the computer must both run this release: the computer's first message on a remote channel now says whether the device is trusted, which older browsers do not understand, and a browser from this release reports an older computer's Prisel as too old. The browser keeps its device key in WebCrypto, which signs with it but never hands it to the page, so script that gets into the page cannot carry the device away. Signing out in a browser forgets its pairings; adding the computer to an account anew and `host remote logout` clear the computer's trusted devices.
- A computer joins an account from one code, and the entry's device-code page `/device` is gone. `prisel host remote login` shows a QR code; a browser signed in to the account that opens it asks first, then adds the computer to the account and pairs with it, and the computer turns on remote access and connects. Only a self-hosted entry needs `--server`: the default is prisel.app. `enable` now only turns remote access back on for a computer that is logged in. The entry adds `POST /api/computers/enroll`, `/api/computers/enroll/collect` and `/api/computers/claim`, and drops device authorization and `/api/computers/bind`, so an older Prisel can no longer be added to an account. The website, the READMEs and Add a computer on prisel.app show the two commands.
- Prisel is proprietary software: all rights reserved, used under the Prisel Terms (https://prisel.app/terms), which now cover the software as well as the prisel.app service. It is no longer under the MIT License. Every package ships `THIRD_PARTY_NOTICES.txt` with the license of each bundled third-party component, including pi (MIT), from which Prisel was forked; the web client serves it at `/licenses/THIRD_PARTY_NOTICES.txt` and prisel.app's footer links to it. 0.10.0 and 0.10.1, and the Linux and macOS platform packages of 0.9.0, were withdrawn from npm.

### Added

- Devices in the host menu, on the local web and remotely: the computer's trusted devices with their fingerprints and dates, revoking one (its connections close at once), a one-time code for adding a device, and Scan to approve a device by the code it shows. The computer list has Scan for either kind of code. Scanning uses the camera, or a photo where the browser cannot use one. In the terminal, `prisel host remote pair` prints the code as a QR code and waits for a device, and `prisel host remote devices [revoke <fingerprint>]` lists and revokes. The protocol adds `host/remote/devices`, `host/remote/devices/revoke`, `host/remote/devices/approve`, `host/remote/pairing` and the `host/remote/devicesChanged` notification.
- The web app can be installed on phones and computers. The entry and the local host serve a manifest and icons; under the computer list, Install shows the browser's prompt where it has one, and on iPhone and iPad the page explains Share → Add to Home Screen. The installed app opens at `/app`, full screen, and on iPhone keeps its pairings even when it is not opened for a while.
- Delete your prisel.app account from the web's Account dialog: the account, its sign-in methods, every signed-in browser and every bound computer go at once, and the relays drop its computers and browsers. It asks for the password, or, for Google, GitHub and email-code accounts, a sign-in within the last 10 minutes (`POST /api/account/delete`).

### Changed

- prisel.app's sign-in joins the entrance instead of replacing it. Signed out, the stage stays: on the desktop the card with the particle knot remains on the right, tilting with the pointer, and the sign-in panel takes the entrance's readout on the left; on phones the mark and its PRISEL line move up and the form follows, centred under them. The readout's request line follows the sign-in (sign-in required, sending a code, code sent, verifying, not accepted), decoding each change, and a refused attempt scatters the knot and condenses it again. Buttons and fields follow the product page's square style, and a status line names the entry and its encryption.
- The privacy policy says what the program itself contacts (the configured model and MCP services, the web search service, models.dev, npm and, with remote access, prisel.app); it has no telemetry. Accounts are deleted in the web instead of by asking on GitHub. The terms say that using Prisel or signing in means accepting them, set the clauses that exclude or limit liability in bold, and warn that an agent may run commands and change or delete files. The sign-in page says signing in or registering accepts the terms and the privacy policy, and the host menu's "Signed-in devices" is now "Account", like the dialog it opens.
- Prisel's changelog, help and feedback links, prisel.app's GitHub link, the terms' feedback link and the npm package's repository and issue links point to the public [nerslm/prisel-release](https://github.com/nerslm/prisel-release) repository (changelog, issues and release notes; the source stays private). npm's package page shows a README for users instead of the source workspace's notes, and OpenRouter attribution names https://prisel.app.
- Prisel calls itself an agent rather than a coding agent: the terminal's startup header and prisel.app's first page read "TERMINAL SERVICE FOR AGENTS", and the site's title, description and headline drop "coding" (in Chinese, 编程), as does the npm package's description.

## [0.10.1]

### Changed

- On phones, the app's mark is the living particle knot of the desktop stage and prisel.app instead of a Canvas2D sketch that froze into a static logo: it condenses during startup and keeps drifting, breathing and pulsing on New Chat, larger than before (up to 196 px). It pauses when New Chat is hidden, behind the keyboard or in the background; tapping it condenses it again, and without WebGL the static mark stands in.
- prisel.app's product page fits each page on one phone screen. Phones get a compact header, the page's number and name with page ticks along the bottom, the devices as a row of tabs with one device in front at a time, the entry's ledger side by side, and sideways swipes to move through devices, backends, the remote steps and features. A page that would not fit its phone's screen, measured with whatever the browser's toolbars leave, tightens and then drops secondary sentences rather than scrolling, and a swipe that starts at a page's edge always turns it (iOS rubber-banding no longer swallows it). The particle canvas and the pages take the visible viewport's size instead of `100vh`, which on iPhone Safari stretched the mark over the words. Desktop is unchanged.
- The entry serves prisel.app's product page at `/` and the app at `/app`; a signed-in browser opening `/` goes straight to the app, and the app's old addresses there (`/?computer=…`, `/?error=…`) are forwarded with their query. `/device`, `/privacy`, `/terms` and `/admin` are unchanged, and a Web build without the product page still shows the app at `/`. Google and GitHub sign-in failures, and the monitor's sign-in link, lead to `/app`.

## [0.10.0]

### Breaking Changes

- The npm launcher is published as `@nerslm/prisel` (`npm install -g @nerslm/prisel`), because npm refuses the unscoped name `prisel` as too similar to `prisma`. The installed command is still `prisel`, the platform packages keep their names, and updates follow the new package name.

### Added

- A backend the host's computer cannot run is dimmed in the Web switch, and choosing it explains why instead of switching. For Claude Code that is not installed, it gives Claude Code's own install commands for that computer's system, each with Copy, a link to the installation guide, and Check again, which opens the backend once the host finds it; from a phone it says the commands run on the computer. `/backend` in the terminal marks it not installed and prints the same commands. Backend descriptors carry them as `install`.
- Run remote relays as their own processes, on any machine, and let the entry assign them (`packages/remote`). A relay registers with `add-relay` on the entry and runs with `relay --config`. It reports its load, connected computers and held authorizations every 10 seconds, and at once when a computer connects or leaves. The entry stops assigning a relay that is shutting down, draining, full or silent for 30 seconds. Sign-outs and revoked computers close on the relay with its next report; if the entry is unreachable, current connections continue. The relay inside the entry stays available (`embeddedRelay`).
- A computer going online times a request to each relay the entry offers, and the entry assigns the closest one it reached unless that relay is much busier; browsers meet the computer on its relay. A relay the computer cannot reach is never assigned, and older computers or entries without the choice keep working.
- Let the entry sit behind a local TCP balancer that shares port 443 by TLS host name (`proxyProtocol`): it reads each visitor's address from the balancer's PROXY protocol header (version 1 or 2) for its rate limits and terminates TLS itself. Headers are accepted only on a loopback listener, from a loopback peer, and required on every connection.
- Sign in to the remote entry with a code sent by email (through Resend), or with Google or GitHub. The first sign-in creates the account, and one verified email address is one account however it signs in. Codes are 6 digits, last 5 minutes and three tries, and their sending is budgeted per recipient, per requesting address and per day; Google and GitHub tokens are discarded. Existing username accounts keep their passwords and can link Google or GitHub from the Account dialog. `passwordSignIn: false` turns username/password sign-in off and `passwordRegistration: false` stops only new password accounts. The entry serves a privacy policy (`/privacy`) and terms (`/terms`); the monitor page uses the site's sign-in instead of its own form, and the entry's sign-in and account pages have no language switch (the language follows the browser). `monitor-access` also takes an account's email address.
- The Web build includes prisel.app's product page (`site.html`): one screen per page over a particle field, with the mark condensing from Halvorsen's system on the first and last pages, replicas of the real terminal, Web and phone clients playing one session, the remote-access path with its packets, and installation. It follows the system's LAB/PRTS choice and shares the app's `prisel.theme` setting.
- Fenced blocks labelled `latex`, `tex` or `katex` show their formulas: each blank-line-separated paragraph becomes a display equation, with or without its own delimiters. A whole document, or a paragraph KaTeX cannot render, stays a code block; the message's copy button keeps the source.
- Show each relay in the administrator monitor: its state, region and current load, plus history charts of connections, forwarding rate, CPU and memory over the last hour, day, week, month or everything recorded. The entry keeps one row per relay per minute (14 days) and per hour (kept) in its own SQLite file, and the page fetches history only for relays on screen, once a minute.

### Changed

- The mark on the Web stage is drawn by particles instead of a glass tube: they swirl on Halvorsen's attractor while `a` rises from 1.4 to 1.89, settle on its periodic orbit, and then drift along it with the same breathing and light pulses. Boot timing is unchanged.

### Fixed

- Show the model and effort a Claude session will really use from the start, as Claude Code's `get_settings` reports them (its messages never report the effort): asked once of a temporary CLI for new sessions and once when a session's own CLI starts. A new session no longer shows no model, and choosing a model keeps the effort slider. When the effort is still unknown, the effort control offers the model's levels with none marked instead of calling the level fixed.
- Name Claude Code's "Default" after the model it runs ("Default (Opus 5.5)") and list Claude's own description of each model instead of its alias. A stored session shows the model it ran ("Opus 5.5") rather than "Default", which today resolves to the same model; context variants such as `claude-opus-5-5[1m]` show as their model.
- Find Claude Code where its native installer puts it (`~/.local/bin`) when that directory is not on the host's PATH, as for a host started before the install.

## [0.9.3]

### Breaking Changes

- Session protocol version 2 is a display and control protocol shared by every backend. Clients receive display entries (`session/history` appends and resets, with `replaces` ending a stream) and display events (`run_*`, `stream_*`, `tool_*`) instead of a session log replica and runtime events; every session request and notification carries `backend` with `sessionId`; sessions declare capabilities, and the host refuses undeclared operations with `Unsupported` (1006) and unavailable backends with `BackendUnavailable` (1007). Settings, projects, pins, model lists and session listing are per backend; native settings use `defaultModel: { provider, id }`. Version 1 clients are refused at `initialize`.

### Added

- Run sessions on a locally installed Claude Code through the same host as native sessions. The host drives `claude` over stream-json and its control protocol (permission prompts as shared questions, model, effort and Claude's permission modes, interrupts, compaction, `!` commands, `/btw`, forks, renames, background tasks, slash commands, statistics, deletion with confirmation) and reads stored transcripts as display history without starting the program. Plan approval shows the plan, the agent's own questions are answered in the shared question card, a subagent's conversation can be watched, and a `!` command run during a turn joins the conversation when it ends. Choosing bypass mode (Full access) restarts Claude Code able to enter it, declaring a sandbox for that process so it also works as root. Claude Code reads its own settings files as usual. Claude Code is never used as a model provider; when it is not installed the backend is listed as unavailable with the reason and nothing falls back to the native runtime. Claude Code's own configuration is never written.
- Switch backends in the terminal with `/backend` (remembered for new terminals) and in the Web/phone client with a switch under the brand; each backend keeps its own workspace of chats, projects, pins, drafts and settings, and the Web settings page configures either backend.
- Add bounded Web history subscriptions with current-branch cursor pages, explicit chunked content reads and viewport-triggered image loading. Keep compact boundaries navigable, preserve live updates and scroll anchors while prepending history, invalidate stale branch cursors, and leave model context unchanged. Retain only the active browser view in memory; no persistent conversation cache or account-server history store.
- Add independent account/device entry and opaque relay source (`packages/remote`), entry-signed one-use admissions, computer-held identities and authenticated Noise channels. Node/Bun/bytecode fixtures cover concurrent clients and live revocation. Add shared-Web account login, device approval, remembered sessions and independent computer switching; isolate browser state and retain per-computer drafts without reloading or replaying commands.
- Add opt-in `host remote login|enable|disable|status|logout` and outbound Host reconnection. Remote enable/disable uses the existing Host without restarting sessions; local startup stays account-independent when remote is off. Remove the superseded computer-password, per-computer HTTPS and callback routes rather than maintaining incompatible login systems.
- Add entry-served Web assets with negotiated compression and font ETags, plus a lightweight administrator-only monitor with aggregate traffic/resource counters and no chat/3D bundle.
- Adapt the shared Web client to the mobile design: Canvas2D knot on the shared boot clock, session/task drawers, keyboard-aware layout, touch model/effort/context sheets and remote device management. Phone Enter inserts a newline; desktop behavior is unchanged.
- Sign in to and out of either backend from any client, including a phone. The host runs the sign-in (`auth/providers`, `auth/login`, `auth/cancel`, `auth/logout`; capability `auth`) and keeps the credentials on its own computer; only the client that started a sign-in sees its links, device codes and questions, and every client learns when someone signed in or out. Claude Code signs in with its own `claude auth` (Claude subscription or Anthropic Console); native providers use their subscription and API-key flows, with ChatGPT's device code offered first to clients on other devices. `/login` and `/logout` now work in Claude sessions too, and the Web client adds an Accounts settings page and a sign-in dialog (`/login` and `/logout` in the composer open it).
- Show a backend account's plan limits and recent usage with `/usage`, in a terminal panel and a Web dialog (`usage/get`; capability `usage`). Claude Code reports its session window, weekly and per-model weekly limits with their reset times, and this computer's usage over the last day and week.

### Changed

- Share one session mirror between the terminal and the Web client and render both from display types. Edit previews, cache-miss notices, `/session` statistics, `/btw`, the model list and the branch tree come from the host; clients no longer rebuild execution context, read working files for previews or match streamed messages by timestamp. Tools of other backends render by their declared kind. A draft's first Web send creates the session with its model, effort and permission mode.
- Anchor mobile startup decoding below the large logo in the final title area, with 12px of extra clearance; slide the Prisel title and subtitle into that area after decoding while retaining the shared boot timing and desktop layout.
- Accept 10–128 character account passwords with matching registration-form and server validation.
- Use device system fonts for Web interface body text and Chinese, including 3D archive labels; retain Montserrat and JetBrains Mono while removing the bundled MiSans downloads.
- Make folded operation segments summary-only in the terminal and Web client: hide all tool cards, file previews, delegated tasks and errors until expanded, preserving manual disclosure state.
- Remove automatic per-turn changed-file summaries from Web conversations; keep the session changes side panel available.
- Display Web activity token counts in trailing parentheses without a down-arrow prefix.
- Replace the hand-written Node WebSocket handshake/frame parser with pinned `ws`, retaining a small Bun-native adapter and shared JSON envelope validation. Add Node/Bun/bytecode transport regressions and an isolated real-native browser acceptance command.
- Distinguish terminal user messages with an adaptive warm surface and expanded tool groups with a lighter surface. Click group whitespace to collapse without resetting individual tool details or intercepting text selection and image rows.
- Trust projects by default: `defaultProjectTrust` now defaults to `always`, so a project's `.prisel` resources load without a prompt and a new installation never stops at one. A project saved as not trusted stays excluded, and `ask` restores the prompt. Claude sessions no longer show the native project-trust warning.
- Never open a browser for a sign-in. The terminal shows the link and copies it to the clipboard; the Web client offers Open and Copy, so a link can be opened on whichever device holds the account. ChatGPT's sign-in methods are named by where they work ("Browser sign-in", "Device code (sign in from any device)"); from another device, the browser sign-in ends on a page whose address is pasted back.

### Fixed

- List only the built-in tools that exist (read, bash, edit, write) in `--help`, with a working read-only example, and say how the default provider is chosen instead of naming one.
- Keep a settings menu (the default permission mode, queue delivery) above the setting cards after it, on an opaque surface, instead of under them.
- Show Web subagent completion and incoming agent messages as independent, initially folded notice rows, outside consecutive-tool groups. Reveal full reports only on opening the notice, preserve sender/completion metadata for referenced history bodies, and leave tool calls and model delivery unchanged.
- Keep the mobile New Chat project menu above recent sessions by lifting only its open picker and containing mobile App. Retain its original anchored placement and all other menu, dialog and keyboard behavior.
- Keep the page-level mobile logo/title behind session and task drawers and settings. Lift the containing mobile App above the external hero while an overlay or its exit scrim is present, without hiding the hero or changing startup timing.
- Own Web startup at the top-level page before access discovery, account lookup or remembered-computer selection. Initialize those routes behind the first-render visibility gate, keep one scene/clock through the handoff, and suppress the intermediate empty computer chooser while restoration is pending. Retain the approved mobile geometry, copy timing and reduced-motion behavior.
- Remove the Web transport-preview/full-content disclosure layer. Deliver complete ordinary page content, automatically fetch large referenced bodies when visible or expanded, keep images viewport-loaded and tool groups folded, and preserve the reading position while details arrive. Retain true history paging, bounded chunk transport, branch guards and unchanged model context/logs.
- Consolidate remote computer switching, signed-in device management and account sign-out into the existing sidebar Host menu. Remove the duplicate computer/account rows without changing local token-based access or stopping computer-owned tasks.
- Keep mobile tool code/diff rows at their declared text size instead of allowing per-row browser inflation. Reserve independent touch-layout space for sidebar session timestamps/status indicators and the always-visible More button, without its desktop overlay or highlight background.
- Make the mobile entrance entirely page-local: a resident logo/title slot exists before Host authentication or remote metadata, so offline connections, slow lists and historical routes cannot consume or hide the animation. Keep the decoder in that stable slot, finish text 240ms before the knot handoff, and reveal the title without relocating the logo or restarting on data arrival.
- Use Noise's maintained WASM ChaCha20-Poly1305 backend when the native runtime lacks that cipher, preventing Bun/bytecode remote channels from disconnecting on session/model responses above the library's small-packet threshold. Retain the protocol, authentication, message limits and Node acceleration; test threshold-sized and multi-frame payloads across all three runtimes.
- Detect silently broken outbound relay connections with Host-initiated, matching-pong heartbeats and bounded timeouts; reconnect automatically instead of reporting stale online status after a network or proxy change.
- Show running shell activity to observing Web clients from shared Host state, not only the browser that launched the command.
- Probe apparently open connections when a browser resumes after suspension; reconnect dead paths without replaying commands or interrupting host-owned work.
- Use Bun's native HTTP/WebSocket upgrade API in native builds instead of writing raw handshakes through Bun's Node HTTP compatibility sockets. Preserve token checks, security headers and the shared session protocol.
- Bound WebSocket connection/initialization attempts and show connecting/reconnecting text while the startup animation awaits the host, rather than leaving an unexplained blank entrance. Ignore stale connection callbacks, reject pending requests without replaying uncertain work, and close upgraded peers during host shutdown.
- Update a Claude session's context usage with every model call of a run, from what that call was sent, instead of only when the run ends; the end of a run still settles it with Claude Code's own count.
- Return from `prisel host stop` only once the host process has exited. `prisel host stop && prisel host run` could start the new host while the old one was still closing its sessions; the old one then removed the new host's socket on its way out, leaving a host that kept serving the web port but that no command could reach.

### Removed

- Remove the unused deprecation-warning helper and superseded Web tool-kind/exploration-summary helpers. Keep the active tool grouping and labels unchanged.

## [0.9.2]

### Changed

- Group consecutive tool calls into operation segments in the terminal and Web client, independent of tool type or assistant-message boundaries. Preserve narration order, manual expansion and hidden thinking; keep file-change previews, delegated tasks and failures visible inside folded segments instead of collapsing whole turns.
- Bound write previews to 10 lines and edit diffs to 20 lines, with explicit expansion and single-column Web diff line numbers. Failed edits show their error rather than speculative successful change counts.
- Show Web thinking, tool execution, retries, approvals and manual/automatic compaction in one bottom-of-transcript activity line. Display growing output-token estimates during generation and reconcile them with provider usage, using the terminal's shared progress tracker.

### Added

- Browse host-side folders from New Chat's working-directory picker, with parent/home navigation, hidden folders, paging, recent locations and explicit selection. Browsing is read-only and does not create/trust a session or change project membership.

### Fixed

- Use the same model-and-reasoning control in Web New Chat and existing sessions. Resolve default-model capabilities without creating a runtime, normalize effort like the host, and apply the chosen pair only on first send.
- Keep typed directory destinations intact when earlier directory listings arrive late.

## [0.9.1]

### Fixed

- Reserve a dedicated history-scroll footer above the terminal composer instead of overwriting a transcript row. Keep it bottom-aligned for short histories, account for resizing and editor/task height changes, and exclude footer/padding rows from transcript selection and mouse routing.

## [0.9.0]

### Breaking Changes

- Rename the product from atria to Prisel (普瑞塞尔). The npm package and command are `prisel`, platform packages are `prisel-<platform>`, global and project configuration use `.prisel`, project instructions use `.prisel/PRISEL.md`, package manifests use the `prisel` key, and environment variables use `PRISEL_*`.
- Prisel has no automatic atria configuration migration or browser-storage import. It does not move `~/.atria`, rename project `.atria/` or `ATRIA.md`, import `atria.*` browser keys, or stop or wait for an atria process. A manual configuration copy must be converted to an independent Prisel configuration.
- Extensions import `prisel`, `prisel-ai`, `prisel-agent`, and `prisel-tui` instead of the atria package names. Internal workspace libraries are not separately published SDK packages.
- Interactive sessions run in a session host and the terminal attaches as a client. Extensions see `ctx.mode === "rpc"`; component-based UI, custom editors, autocomplete providers, and raw terminal input hooks do not render in the attached terminal. Dialogs, notifications, status text, string widgets, working messages, and tool/message/entry renderers remain supported. See the `docs/session-host.md` bundled reference.
- `ask_user` in the interactive terminal uses the select-and-input fallback. Direct users of the internal subagent factory and in-process child entry point must pass a tree-local agent registry; `liveAgentIds()` takes that registry.
- Custom `modelCatalogUrl` mirrors must serve a Models.dev-compatible `catalog.json` containing `providers` and canonical `models`. Legacy provider shards and `provider-catalog.json` are not read by this runtime.

### Added

- A shared session host with terminal and Web clients, synchronized output and settings, background shells, subagents, workflows, and cross-client approvals. `prisel --daemon` keeps sessions running when a terminal disconnects; `prisel attach`, `prisel sessions`, and `prisel host start|run|stop|status` manage them.
- `prisel web` serves the Web client from the session host; `prisel host run --listen [host:]port` enables it at startup. WebSocket clients authenticate with the token under `~/.prisel/host/web-token`.
- Shared Web configuration for new-chat defaults, model selection, reasoning, compaction, retries, queued messages, transport, and model-directory updates. Host update controls can install a newer release and restart the host explicitly.
- A documented session protocol and client API for additional clients, with read-only archive inspection separate from opening or executing sessions. `sessions/inspect` uses current-branch selection, storage-root isolation, and explicit partial results.
- Manually named projects independent of working directories. Create or rename collections, assign each session to at most one project, and transfer or remove membership without moving files or opening historical sessions. Revisioned host storage synchronizes clients; new sessions are unclassified unless explicitly assigned, and forks inherit membership.
- Confirmed deletion for Web projects and sessions. Deleting a project returns its sessions to unclassified without stopping them. Deleting an idle session removes only its own record; busy/approval and concurrent-operation checks protect active work. Cleanup warnings distinguish record deletion from metadata cleanup failures.
- Web appearance settings for Chinese and English, applied immediately and stored per browser without changing the TUI language or model replies.
- An interactive Web context ring with hard-threshold and Context Archive launch markers, actual usage, and keyboard-accessible threshold controls saved through the session protocol.
- Local KaTeX rendering for explicit inline/display math and `math` fences, with bundled fonts, restricted commands, bounded expansion, and escaped-source fallback. Ordinary code and Unicode text are not reinterpreted as formulas.
- `SessionSummary.live.isWorking` and global approval-state notifications keep archive cards, sidebar markers, and activity counts current without requiring model streaming or a session attachment.
- A skippable Prisel knot startup animation using the terminal header. Quiet, resumed, non-interactive, and `PRISEL_NO_ANIMATION=1` starts remain immediate; ordinary typing is preserved.
- Automatic model-directory checks, enabled by default through `autoModelUpdates`, run without blocking startup and hourly while a session or host is active. Manual `prisel model update`, Web Settings → Configuration → Models, and host `models/refresh` remain available when automatic updates are off. Status exposes refresh progress, last attempt, last successful check, and errors; failures retain usable data and make the CLI exit nonzero.

### Changed

- Precompile native releases with Bun ESM bytecode to reduce startup latency while retaining the default terminal opening animation. Bytecode and minification do not encrypt the bundled JavaScript.
- Rebuild the Web client around the approved LAB/PRTS design: local licensed fonts, the Prisel knot, a resident Three.js stage, real session archive, chat/tasks/approvals, and matching settings/host controls. Reduced motion, narrow screens, and unavailable WebGL retain usable static views.
- Synchronize Web startup text, the corner logo, and the resident 3D stage on one timeline with a transparent overlay and a single interface entrance. Restore view/list entrances and retained-panel/popover exits without replaying animations during streaming or clock updates.
- Make Web New Chat an immediate local draft. The host session is created only on first send, and the resident home scene does not wait for runtime initialization. Draft text, images, and choices survive clear failures; prepared sessions are reused for retries. Stale navigation responses cannot steal focus, and uncertain disconnected sends require verification before retrying.
- Replace cwd-based Web project groups with explicit projects and unclassified chats, including the 3D archive. Browser-local file numbers use a host-wide index stable across project transfers, remain display-only, and stay unassigned for drafts. Simplify the Web brand to the knot and PRISEL, and replace canned homepage suggestions with the three most recent real sessions.
- Replace the terminal's large getting-started frame with the unframed knot lockup and live HOST/MODEL/DIR/CONTEXT/SESSION fields. Keep project guidance compact, with full help and release notes available separately.
- Refresh built-in terminal palettes with copper/amber accents and adaptive secondary colors while inheriting the terminal background and main foreground. Custom themes retain their explicit colors. Use the Prisel knot as the working indicator and retain `AGENT` labels for delegation and communication without adding message role headers.
- Display clipboard images as compact `[image #N]` attachment labels instead of temporary paths. Labels retain their underlying file references for submission and external editing; supported custom editors can opt into the attachment API.
- Read Models.dev directly instead of relying on a Prisel-hosted catalog or scheduled pi-ai catalog generation. Matching canonical capabilities take precedence over service defaults; absent or unrecognized metadata retains existing values. New providers still require a locally supported protocol.
- Store public metadata in `~/.prisel/model-catalog.json`, separately from native discovery in `models-store.json`. A bundled, reviewable Models.dev capability snapshot complements the AI package's transport/model snapshot for offline use.
- Newly discovered providers do not read environment variables declared by remote metadata. Log in to the provider or configure its `apiKey` in local `models.json` before use. Built-in and user-configured providers retain their environment mappings, OAuth, and transports.
- Separate human guides in root `docs/` from embedded agent references in `agent-docs/`. Keep `docs/...` and `examples/...` tool lookups, derive the bundled README from the agent reference index, and exclude repository policies, design guides, and the roadmap from the bundle. Correct outdated configuration, permissions, SDK, and development instructions.
- Rename native Windows source launchers from `pi-test.bat` / `pi-test.ps1` to `dev.bat` / `dev.ps1`, and resolve source aliases through the repository TypeScript configuration. `--no-env` clears selected environment variables; it does not disable credential-file loading.
- Route repository and workspace tests through a shared offline runner with temporary home/state/config directories, an environment allowlist, bounded concurrency, explicit live-suite exclusions, and Web test/typecheck coverage. The shell wrapper no longer moves user credentials. Test-only OAuth access requires explicit opt-in and never writes refreshed credentials to disk.
- Audit root/workspace development, production, optional, and peer dependencies, with installed-package signature checks and a separate push/PR/scheduled/manual audit workflow. Explicit flags prevent inherited workspace or offline settings from narrowing or skipping the audit.
- Refresh reviewed dependencies to Undici 8.11.2, minimatch 10.2.6, Vitest/coverage 4.1.11, and patched transitive versions of brace-expansion, PostCSS, nanoid, protobufjs, and shell-quote. Retain existing SDK/framework major versions and update the sandbox example's independent lockfile.
- Replace shx build operations with fixed-workspace Node filesystem tasks, removing the shelljs/fast-glob/micromatch/braces build-only chain without replacing runtime glob matching.

### Removed

- The scheduled pi-ai fallback-update workflow. Model-directory refreshes do not require a Prisel-owned generation job; release snapshots remain manually reviewable.

### Fixed

- Isolate subagent registries by session tree and extension-module caches by project. Contain exceptions in `AgentSession.subscribe()` listeners, and load finished subagent transcripts from saved sessions when needed.
- Keep persistent runtime-test sessions in explicit temporary storage and make host session creation default to its own agent directory rather than the process-global directory.
- Prevent release preparation from overwriting existing version artifacts. Serialize preparations with a repository lock, reserve version paths exclusively, promote validated tarballs without replacement, and expose the manifest only after the entire batch is ready. Retain incomplete reservations for inspection and reject source changes during a build.
- Resolve each workspace's actual Vitest installation in both package-local and npm-hoisted layouts without falling back outside the repository. Align coding-agent's production TypeScript build with NodeNext for JSON import attributes on the supported Node baseline.
- Keep the terminal startup guide at the beginning of the scrollable transcript rather than deleting it on first send. Fill short views below their content so the editor remains aligned above the footer/tasks area.
- Gate terminal input/footer chrome before the first startup paint to prevent flashing before the opening animation. Early input or skip gestures during theme detection neither replay the animation nor lose typed text.
- Route complete empty bracketed-paste notifications to image paste, covering terminal Paste actions that do not send a raw Ctrl+V key. Preserve nonempty and whitespace pastes as text and handle fragmented framing without changing terminal, Bash, or WSL configuration.
- Improve WSL clipboard image/text reads through a direct Windows memory bridge, preserve text fallback after image-read failures, provide safe diagnostics, and support Alt+V alongside Ctrl+V. Image attachments remain private temporary files.
- Make terminal drag selections visible with paired high-contrast foreground/background colors without repainting normal content; custom selection backgrounds remain respected.
- Keep the built-in knot indicator synchronized with theme changes without replacing custom frames or restarting a disposed indicator. Place shell summaries before workflows/subagents and preserve task selection by ID as entries change.
- Keep focused No/Deny buttons authoritative for keyboard approvals, and prevent archive navigation shortcuts from intercepting PIN/export/tab controls. Preserve drafts and failed approvals, roll back failed pin changes, and invalidate stale archive inspections and deleted records across clients.
- Return 404 for missing, directory, and prototype-key static asset requests instead of crashing the Web host.
- Use canonical total context (`limit.context`) and independent output limits rather than treating input limits or 272K pricing thresholds as context-window caps. Apply explicit `models.json` model overrides last, including after custom entries and extension updates.
- Refresh same-ID model capabilities immediately for idle sessions or at safe turn boundaries for busy sessions, without changing selection or history. Compaction continues using the configured ratio and refreshed context window.
- Update Codex effort/context metadata for known and newly discovered IDs, prefer `max_context_window` over `context_window`, and preserve cached capabilities when fields are absent. OpenAI canonical metadata enriches subscription entries without adding API-only models to discovery.
