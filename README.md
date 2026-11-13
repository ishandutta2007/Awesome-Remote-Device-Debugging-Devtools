# Awesome-Remote-Device-Debugging-Devtools

# Awesome Remote Device Debugging & DevTools

> A curated list of top Remote Device Debugging and DevTools platforms — both SaaS/Hosted commercial solutions and open-source alternatives for inspecting, controlling, and debugging web pages, apps, and network traffic on remote devices.
> 🌟 Star this repo if you find it useful! 🌟

---

## 📋 Table of Contents

- [SaaS / Hosted Platforms](#-saas--hosted-platforms)
  - [BrowserStack Remote Debugging](#browserstack-remote-debugging)
  - [Proxyman](#proxyman)
  - [Charles Proxy](#charles-proxy)
  - [Fiddler](#fiddler)
- [Open-Source Software](#-open-source-software)
  - [Device Farmer STF](#device-farmer-stf)
  - [tapflow](#tapflow)
  - [nectoproxy](#nectoproxy)
  - [Rockxy](#rockxy)
  - [Remote WebView Debugger](#remote-webview-debugger)
  - [adb-tui](#adb-tui)
  - [ios-safari-remote-debug-kit](#ios-safari-remote-debug-kit)
  - [spy-debugger](#spy-debugger)
  - [cdp-ninja](#cdp-ninja)
- [Comparison at a Glance](#-comparison-at-a-glance)
- [Contributing](#-contributing)

---

## 🟦 SaaS / Hosted Platforms

Commercial, cloud-hosted Remote Device Debugging platforms. These are not open-source but are included as reference points for feature comparison.

### BrowserStack Remote Debugging
**Type:** Real-device cloud with interactive debugging  
BrowserStack provides interactive remote debugging on real devices and browsers, allowing inspection of DOM, console, and network requests through a cloud-hosted interface. It is the long-standing commercial standard for cross-browser debugging without maintaining an in-house device lab.

### Proxyman
**Type:** Native macOS HTTP debugging proxy  
Proxyman is a polished, native macOS proxy for intercepting and inspecting HTTP/HTTPS traffic, with a modern UI, breakpoints, and map local/remote capabilities. It is a commercial alternative to Charles Proxy and Fiddler, popular among macOS developers.

### Charles Proxy
**Type:** Cross-platform HTTP debugging proxy  
Charles Proxy is a long-standing commercial web debugging proxy for macOS, Windows, and Linux, supporting HTTP/HTTPS interception, breakpoints, and bandwidth throttling. It is frequently cited as the benchmark that open-source proxies like nectoproxy aim to replace [citation:4].

### Fiddler
**Type:** Web debugging proxy (Telerik)  
Fiddler captures HTTP/HTTPS traffic for inspection and debugging, with a focus on Windows environments. It is commonly used alongside dedicated API clients for network-level debugging.

---

## 🟩 Open-Source Software

Self-hosted, community-driven Remote Device Debugging and DevTools. The open-source ecosystem spans **real-device device farms**, **browser-based simulator access**, **HTTP debugging proxies**, **in-app WebView debuggers**, **ADB terminal interfaces**, and **iOS Safari remote debugging kits**.

### Device Farmer STF
**Stack:** Node.js / TypeScript / RethinkDB / ADB | **License:** Apache-2.0  
Device Farmer STF (Smartphone Test Farm) is the leading open-source **real-device device farm** for Android, allowing teams to share and control physical devices remotely via a web interface [citation:15]. For remote debugging specifically, STF provides a **Remote Debug panel** that exposes an `adb connect` command; running it locally connects the remote device to your workstation, after which you can use `chrome://inspect` in Chrome or `opera:debug` in Opera to debug pages and WebViews on the device [citation:1]. It supports the full ADB workflow including shell, logcat, and file management through the web UI. Deployment via Docker Compose with RethinkDB is documented [citation:15].  
**Best for:** Android QA teams wanting to share physical devices across a distributed team with genuine remote ADB debugging access, accepting the operational overhead of a full device farm.

### tapflow
**Stack:** Node.js / WebSocket / H.264 | **License:** MIT  
tapflow is a self-hosted **BrowserStack alternative for mobile QA** that lets teams access iOS Simulators and Android Emulators running on their own Macs through a browser dashboard [citation:3]. It connects a relay server, a macOS agent that drives the simulators, and a browser dashboard for the rest of the team. Key differentiators include **no WebDriverAgent** (touch injection is direct), **no cloud uploads** (builds and streams stay on your infrastructure), and **H.264 streaming** for low latency. It also includes an MCP server for LLM agents and a deterministic flow runner. Requirements: macOS with Xcode for the agent, Node.js ≥20 for the relay, and ~512 MB RAM.  
**Best for:** Mobile QA teams wanting browser-based access to their own simulators without uploading builds to a third-party cloud, accepting that agents must run on macOS.

### nectoproxy
**Stack:** Node.js / React | **License:** Open Source (npm)  
nectoproxy is a **free, open-source alternative to Charles Proxy and Fiddler**, providing HTTP/HTTPS interception with a modern web UI [citation:4]. Key features include **MITM proxying** with auto-generated per-domain SSL certificates, real-time traffic monitoring via WebSocket, a **rules engine** with 8 actions (Mock, Block, Modify Request/Response, Map Local/Remote, Delay, Throttle), **breakpoints** for manual request/response editing, **network conditioning** (3G, slow Wi-Fi profiles), and **HAR import/export** with code generation in 7 languages. It runs on Node.js 20+ and installs via `npm install -g nectoproxy`. CA certificate installation instructions are provided for macOS, Windows, and Linux.  
**Best for:** Developers wanting a modern, open-source HTTP debugging proxy with a rich rules engine and web UI, particularly those wanting to replace Charles Proxy or Fiddler without licensing costs.

### Rockxy
**Stack:** Native macOS (Swift) | **License:** Open Source  
Rockxy is an open-source **native macOS HTTP debugging proxy** for intercepting HTTPS, inspecting APIs, mocking responses, and debugging WebSocket & GraphQL [citation:10]. It is positioned alongside Burp Suite, ZAP, and Requestly in the interception tool category, but with a focus on being a general-purpose native debugging proxy rather than a security testing suite. It supports MCP for AI client integration.  
**Best for:** macOS developers wanting a native, open-source proxy alternative with a focus on API debugging and WebSocket/GraphQL inspection.

### Remote WebView Debugger
**Stack:** Go / WebSocket / MCP | **License:** Open Source  
Remote WebView Debugger lets **AI agents debug WebViews inside apps and H5 pages on real users' phones over MCP** [citation:9]. A single script tag (or native injection) puts a page online; the user sees a small pill with a device code and can request assistance. Your agent (Claude Code, Cursor) then connects via MCP after user approval, reading accessibility snapshots, console, network, and screenshots, and clicking/typing/scrolling like a person. Admins can also open **real Chrome DevTools** on any online page. **User control is central:** the user sees what the AI is doing and can take over or end the session. Passwords, phone and card numbers are masked before leaving the device. Self-hosted as a single Go binary with SQLite or Postgres.  
**Best for:** Teams wanting AI-assisted debugging of real user WebViews with strong privacy controls, particularly for production support scenarios.

### adb-tui
**Stack:** Go | **License:** Open Source  
adb-tui is a **full-featured terminal UI and MCP server for Android Debug Bridge** [citation:6]. It provides 11 interactive views covering devices, shell, logcat, files, packages, port forwarding, input injection, processes, settings, and performance. It doubles as an **MCP server with 120+ tools**, allowing Claude or other agents to install apps, stream logs, capture screens, manage files, and control touch input autonomously. Wireless debugging (USB ↔ TCP/IP) is one key away. All shell commands use parameterized execution to avoid injection. Installable via Homebrew, script, Go, or pre-built binaries.  
**Best for:** Android developers and QA engineers wanting a terminal-based ADB dashboard with AI agent integration, particularly for automation and remote device control.

### ios-safari-remote-debug-kit
**Stack:** Shell / WebKit WebInspector | **License:** Open Source  
ios-safari-remote-debug-kit is a **free and open-source alternative to inspect.dev** for debugging iOS Safari from Windows or Linux [citation:13]. It downloads the latest WebKit WebInspector, patches it to work with `ios-webkit-debug-proxy`, and makes it compatible with Chromium-based browsers. Requirements include `ios-webkit-debug-proxy`, a Chromium or WebKit browser, and a USB-connected iOS device with Web Inspector enabled in Safari settings. Setup scripts (`generate.sh` or `generate.ps1`) handle the WebKit download and patching.  
**Best for:** Developers on Windows or Linux needing to debug iOS Safari remotely without a Mac, accepting the USB tethering requirement and setup steps.

### spy-debugger
**Stack:** Node.js | **License:** Open Source  
spy-debugger is a **one-stop remote network debugger** for mobile pages, supporting HTTP/HTTPS interception, WebView style debugging, and page debugging without requiring a USB connection [citation:2]. It has 8k+ GitHub stars and 825 forks, making it one of the more popular open-source remote debugging tools. It is particularly relevant for WeChat and WebView debugging scenarios common in Chinese mobile development.  
**Best for:** Developers needing wireless remote debugging of mobile pages and WebViews, particularly in WeChat or similar embedded browser environments.

### cdp-ninja
**Stack:** Python / Chrome DevTools Protocol | **License:** Open Source (PyPI)  
cdp-ninja is a **Chrome DevTools Protocol bridge** that exposes 89 endpoints across 14 domains for direct browser control [citation:5]. It is explicitly positioned as a **browser hacking framework for security testing and chaos engineering**, with no input validation, no rate limiting, and raw CDP access. It includes remote deployment features: `--tunnel` for SSH tunneling, `--install-agents` for remote agent deployment, and `--invoke-claude` for remote AI interface access. **Critical warning:** The project explicitly states it is intentionally dangerous and should only be used in secure, isolated environments for authorized testing.  
**Best for:** Security researchers and chaos engineers wanting raw, unrestricted CDP access for deliberate testing, not for production debugging workflows.

---

## 📊 Comparison at a Glance

| Software | License | Stack | Primary Focus | Real Device | Self-Hosted | Best For |
|----------|---------|-------|---------------|-------------|-------------|----------|
| **BrowserStack** | Proprietary | Cloud | Real-device debugging | ✅ | ❌ | Cross-browser debugging |
| **Proxyman** | Proprietary | macOS | HTTP proxy | ❌ | ❌ | Native macOS proxy |
| **Device Farmer STF** | Apache-2.0 | Node.js/ADB | Android device farm | ✅ Physical | ✅ | Shared Android devices + ADB |
| **tapflow** | MIT | Node.js | Simulator access | ❌ (Sims) | ✅ | Browser access to simulators |
| **nectoproxy** | Open Source | Node.js | HTTP proxy | ❌ | ✅ | Charles/Fiddler replacement |
| **Rockxy** | Open Source | Swift (macOS) | HTTP proxy | ❌ | ✅ | Native macOS proxy |
| **Remote WebView** | Open Source | Go | AI agent WebView debug | ✅ (Real users) | ✅ | AI-assisted production debug |
| **adb-tui** | Open Source | Go | ADB terminal + MCP | ✅ (ADB) | ✅ | Terminal ADB dashboard |
| **ios-safari-kit** | Open Source | Shell | iOS Safari debug | ✅ (USB) | ✅ | Windows/Linux iOS debugging |
| **spy-debugger** | Open Source | Node.js | Wireless mobile debug | ✅ (Wireless) | ✅ | WeChat/WebView debugging |
| **cdp-ninja** | Open Source | Python | Raw CDP bridge | (Browser) | ✅ | Security/chaos testing |

---

## 🤝 Contributing

Contributions are welcome! If you know of an open-source Remote Device Debugging or DevTools platform that should be listed here, please open a pull request with:

- Project name and URL
- Brief description (1–2 sentences)
- Stack and license
- Why it stands out

Please ensure the project is actively maintained (releases within the last 12 months) and genuinely open-source. Note that the open-source ecosystem **splits** between **real-device access** (Device Farmer STF for shared Android devices with ADB debugging [citation:1][citation:15]), **simulator access** (tapflow for browser-based iOS/Android simulators [citation:3]), **HTTP debugging proxies** (nectoproxy, Rockxy [citation:4][citation:10]), **AI-assisted in-app debugging** (Remote WebView Debugger [citation:9]), and **platform-specific bridges** (ios-safari-remote-debug-kit for iOS on Windows/Linux [citation:13], adb-tui for Android terminal control [citation:6]). **nectoproxy** is the most complete open-source Charles/Fiddler replacement with a modern web UI and rich rules engine, while **Device Farmer STF** remains the standard for shared Android device farms with genuine remote ADB access.

---

## 📄 License

This list is released under CC0 1.0 Universal (Public Domain). The software projects listed retain their respective licenses.

---

⭐ **If this list helped you discover a useful tool, please star the repo!** ⭐
