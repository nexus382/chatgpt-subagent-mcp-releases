# CodexGPT MCP

**CodexGPT MCP** is a Windows MCP release that lets Codex hand work to your signed in ChatGPT browser session, wait for ChatGPT to finish, and bring the answer back into Codex.

This public repository is for **release downloads and setup documentation**. The source code is kept in a private TnT Studios development repository.

## Latest Release

Current production release:

```text
CodexGPT MCP v1.0.0
```

Download it here:

```text
https://github.com/TnT-Studio-s/TnTs-CodexGPT-MCP/releases/latest
```

Download the Windows zip asset from the latest release page.

SHA256 for the v1.0.0 Windows zip:

```text
CB67D6B466986CE0F332C477A461B59C51F3347C89175FA4F6D599BC1617BCA7
```

## What It Does

CodexGPT MCP gives Codex a local MCP tool bridge into ChatGPT Web.

It can:

* Open or reuse a managed ChatGPT browser session.
* Detect when you need to sign in.
* Wait while you sign in manually.
* Start a new ChatGPT conversation.
* Send prompts from Codex to ChatGPT.
* Wait for ChatGPT to finish responding.
* Bring the final response back into Codex.
* Try UI based model selection and Deep Research when your ChatGPT account exposes those controls.
* Export the latest response to a file.
* Extract links from responses.
* Run health checks with clear fix instructions.
* Build prompt templates for research, code review, comparison, and summarizing.
* Retry the last delegated task safely.

## How It Works

At a high level:

1. Codex starts the local MCP server from the extracted release folder.
2. The MCP server opens or attaches to a managed ChatGPT browser window.
3. You sign in to ChatGPT manually the first time.
4. Codex calls MCP tools such as `chatgpt_delegate`.
5. The MCP server sends the prompt to ChatGPT Web.
6. ChatGPT does the research, reasoning, or answering inside your normal signed in account.
7. The MCP server reads the final response and returns it to Codex.

This is browser automation, not an official ChatGPT API. That means ChatGPT UI changes can affect behavior, and you should keep normal account safety in mind.

## Easiest Setup With Codex

This guide is meant to be read by your Codex instance too.

Simple path:

1. Download the latest Windows zip.
2. Extract the folder somewhere normal, like Downloads or Documents.
3. Tell Codex where the extracted folder is.
4. Tell Codex to read `CODEX_SETUP_HANDOFF.md` and install it for you.
5. Restart Codex when the install is done.
6. After restart, tell Codex to open ChatGPT through CodexGPT MCP.

You normally do **not** run the `.exe` yourself. The executable is the MCP server that Codex starts after installation.

## Manual Install

After extracting the zip, open PowerShell in the extracted folder and run:

```powershell
powershell -ExecutionPolicy Bypass -File .\install-the-codex-buddy.ps1
```

Then restart Codex.

The installer updates your user level Codex config so CodexGPT MCP is available across Codex projects.

## First Test

After restarting Codex, ask Codex:

```text
Use chatgpt_open.
```

If ChatGPT asks you to sign in, sign in manually in the browser window.

Then ask Codex:

```text
Use chatgpt_wait_for_login.
```

Then run a smoke test:

```text
Use chatgpt_delegate to ask ChatGPT: Reply with exactly "CodexGPT MCP is working."
```

If Codex receives that exact response, the bridge is live.

## Are The Tools Commands?

The `chatgpt_*` tools are MCP tools, not normal PowerShell commands.

You use them by asking Codex to call them. Codex sees the tools, chooses parameters, runs them, waits for the result, and shows you the answer.

Main tools:

| Tool | What it does |
| --- | --- |
| `chatgpt_open` | Opens or attaches to the managed ChatGPT browser session. |
| `chatgpt_status` | Reports browser, login, and readiness state. |
| `chatgpt_wait_for_login` | Waits while you sign in manually. |
| `chatgpt_new_chat` | Starts a clean ChatGPT conversation. |
| `chatgpt_select_model` | Attempts UI based model selection by label. |
| `chatgpt_enable_deep_research` | Attempts to enable visible Deep Research UI. |
| `chatgpt_get_last_response` | Reads the latest visible ChatGPT assistant response. |
| `chatgpt_delegate` | Sends a prompt and waits for the completed response. |
| `chatgpt_retry_last` | Repeats the last delegated task. |
| `chatgpt_export_last_response` | Saves the latest response as md, txt, or json. |
| `chatgpt_extract_links` | Extracts structured URLs from text or the latest response. |
| `chatgpt_health_check` | Checks setup and gives exact fix guidance. |
| `chatgpt_prompt_template` | Builds reusable prompts for common workflows. |
| `chatgpt_client_info` | Reports backend mode and capability flags. |

## Speed Modes

CodexGPT MCP cannot make ChatGPT search or think faster. That part takes as long as ChatGPT takes.

What it can make faster is the local handoff between Codex and ChatGPT.

Default stable mode:

```text
CHATGPT_SPEED_MODE=token_saver
```

Faster local polling mode:

```text
CHATGPT_SPEED_MODE=max_speed
```

Use max speed when you want Codex to notice completed ChatGPT responses as quickly as possible.

## Current Production Path

Browser mode is the supported production path right now.

Windows app automation exists as an experimental target in the private source, but public users should use browser mode until parity is proven.

## Safety Notes

CodexGPT MCP never asks for your ChatGPT password.

You sign in directly inside the ChatGPT browser window.

Do not share browser profile folders that contain login state.

Delegated prompts are sent to ChatGPT through your own signed in account.

## TnT Studios

This is the first live TnT Studios production release of CodexGPT MCP.

Use Codex for coding.

Use ChatGPT for research.

Let CodexGPT MCP bridge the two.