# CodexGPT MCP

**CodexGPT MCP** lets Codex hand research, information gathering, and long-form reasoning work to your signed-in ChatGPT browser session, wait for ChatGPT to finish, and bring the answer back into Codex.

This public repository is for **Windows release downloads** and **setup documentation**.

The source code is kept in a private repository.

## What This Is

CodexGPT MCP is a local MCP bridge that allows Codex to use your ChatGPT account through a managed browser session.

The point of this project is simple:

**Codex can focus on building your game, app, or software while ChatGPT handles the heavy research and information gathering.**

Instead of having Codex spend project time and context on large research jobs, CodexGPT MCP lets Codex send those jobs to ChatGPT through your normal ChatGPT account. ChatGPT does the research, reasoning, or summarizing, then Codex gets the finished answer back and can keep working with better information.

In a nutshell:

**Codex can control a managed ChatGPT browser session, ask it questions, wait for answers, and pull those answers back into your Codex project workflow.**

This makes CodexGPT MCP one of the best ways to improve research and information gathering for Codex projects while keeping Codex focused on the actual build.

## Why Use This?

Codex is great at:

* Reading and editing your project files.
* Writing code.
* Fixing bugs.
* Refactoring.
* Running commands.
* Working directly inside your app, game, or software project.

ChatGPT is often better for:

* Deep research.
* Web searching.
* Long-form reasoning.
* Summarizing documentation.
* Comparing tools, libraries, models, APIs, or frameworks.
* Drafting research briefs.
* Gathering outside information before Codex writes code.

CodexGPT MCP connects those strengths together.

It lets Codex offload large research jobs to ChatGPT, then bring the results back into your project. That means Codex can keep its attention on coding while ChatGPT handles the outside information work.

## What It Can Do

CodexGPT MCP can:

* Open or reuse a managed ChatGPT browser session.
* Detect when you need to sign in.
* Wait while you complete ChatGPT login manually.
* Start a new ChatGPT conversation.
* Send prompts from Codex to ChatGPT.
* Wait for ChatGPT to finish responding.
* Read the final ChatGPT answer.
* Return that answer back into Codex.
* Use faster local handoff timing with `CHATGPT_SPEED_MODE=max_speed`.
* Attempt browser UI features such as model selection and Deep Research when your ChatGPT account exposes them.

Good use cases include:

* Researching a library before Codex integrates it.
* Asking ChatGPT to compare APIs or SDKs.
* Having ChatGPT summarize documentation for Codex.
* Letting ChatGPT search the web for current information.
* Creating research briefs for game, app, or software development.
* Offloading long reasoning tasks so Codex can stay focused on implementation.
* Gathering project information without burning as much Codex-side effort on research.

## How It Works

At a high level:

1. Codex starts the local MCP server.
2. The MCP server opens or connects to a managed ChatGPT browser window.
3. You sign in to ChatGPT manually the first time.
4. Codex calls MCP tools such as `chatgpt_delegate`.
5. The MCP server sends the prompt to ChatGPT.
6. ChatGPT works through your normal signed-in account.
7. The MCP server waits for the response to finish.
8. The final answer is read back and returned to Codex.

This is **browser automation**, not an official ChatGPT API.

That means CodexGPT MCP uses your normal ChatGPT web session and can be affected by ChatGPT UI changes.

## Download

Get the latest Windows release here:

```text
https://github.com/nexus382/chatgpt-subagent-mcp-releases/releases/latest
```

Download the Windows zip asset.

It may be named like this:

```text
CodexGPT-MCP-0.8.0-windows.zip
```

Older releases may still use the previous package name:

```text
The-Codex-Buddy-0.8.0-windows.zip
```

## Easiest Codex-Assisted Setup

This guide is written so both humans and Codex can understand it.

The simple setup path is:

1. Download the latest Windows release zip.
2. Extract the release folder somewhere normal, such as Downloads or Documents.
3. Tell Codex where the extracted folder is.
4. Ask Codex to read the README or `CODEX_SETUP_HANDOFF.md` inside that folder.
5. Ask Codex to install CodexGPT MCP for you.
6. Restart Codex after installation.
7. After restart, ask Codex to open ChatGPT through the MCP.

You do not normally run the `.exe` yourself.

The executable is the MCP server that Codex starts after installation.

## Manual Install For Codex

Extract the zip somewhere normal, such as:

```text
Downloads
Documents
C:\Tools
```

Then open PowerShell inside the extracted folder and run:

```powershell
powershell -ExecutionPolicy Bypass -File .\install-the-codex-buddy.ps1
```

Restart Codex after the installer finishes.

The installer updates your user-level Codex config so CodexGPT MCP is available across Codex projects.

## First Run

After restarting Codex, ask Codex to open ChatGPT through the MCP:

```text
Use chatgpt_open.
```

If ChatGPT is not signed in, a browser window should open.

Sign in manually.

Then ask Codex to wait for login:

```text
Use chatgpt_wait_for_login.
```

After login is ready, test a normal delegation:

```text
Use chatgpt_delegate to ask ChatGPT: Reply with exactly "MCP smoke test passed."
```

If Codex receives that exact phrase back, CodexGPT MCP is working.

## Are The Tools Commands?

The `chatgpt_*` tools are MCP tools.

They are mainly for Codex or another MCP-capable model client to call.

They are not normal PowerShell commands that you type directly like:

```powershell
git status
```

In practice, you use them by asking Codex to call them.

Example:

```text
Use chatgpt_delegate to ask ChatGPT to research the latest MiniMax model news and bring the answer back here.
```

Codex sees the MCP tool, chooses the right parameters, calls it, waits for the result, and then shows you the answer.

Advanced users can run the MCP executable manually for debugging, but normal users should let Codex launch CodexGPT MCP.

## Available MCP Tools

These are the current tool names Codex can use:

| Tool                           | What it does                                                    |
| ------------------------------ | --------------------------------------------------------------- |
| `chatgpt_open`                 | Opens or attaches to the managed ChatGPT browser session.       |
| `chatgpt_status`               | Reports whether the browser is ready, signed in, and usable.    |
| `chatgpt_wait_for_login`       | Waits while the user signs in manually.                         |
| `chatgpt_new_chat`             | Starts a clean ChatGPT conversation.                            |
| `chatgpt_select_model`         | Attempts to select a visible ChatGPT model by label.            |
| `chatgpt_enable_deep_research` | Attempts to enable Deep Research in the ChatGPT UI.             |
| `chatgpt_get_last_response`    | Reads the latest visible ChatGPT assistant response.            |
| `chatgpt_delegate`             | Sends a prompt to ChatGPT and waits for the completed response. |
| `chatgpt_client_info`          | Reports backend mode and capability flags.                      |

Most users will mainly use:

```text
chatgpt_delegate
```

## Browser Mode

Browser mode is the recommended and supported backend.

It uses a managed browser profile so your ChatGPT login can persist between runs.

The first time, you sign in manually.

After that, Codex can usually reuse the session.

Browser mode is currently the best path for:

* Normal prompt delegation.
* Response readback.
* New chats.
* Deep Research attempts.
* Faster handoff timing.

## Speed Mode

CodexGPT MCP cannot make ChatGPT itself think, search, or run Deep Research faster.

Those parts take however long ChatGPT takes.

What it can make faster is the local handoff between Codex and ChatGPT:

* Detecting when ChatGPT has stopped generating.
* Returning the completed response back to Codex sooner.
* Reducing local UI settle waits.

To opt into faster local polling, set this in the MCP `.env` file:

```text
CHATGPT_SPEED_MODE=max_speed
```

The default mode is safer and more conservative:

```text
CHATGPT_SPEED_MODE=token_saver
```

Use `max_speed` when you want faster handoff timing.

Use `token_saver` when you want the more conservative default behavior.

## Current Limitations

CodexGPT MCP is powerful, but it is still an unofficial automation bridge.

Important limitations:

* It is not an official ChatGPT control API.
* It uses browser automation.
* ChatGPT UI changes can break selectors.
* Model selection depends on what is visible in your ChatGPT account.
* Deep Research depends on whether your ChatGPT account exposes it.
* Heavy research still takes as long as ChatGPT needs.
* The Windows app backend is experimental and not recommended for public use yet.
* Browser mode is the production path right now.

## Safety Notes

CodexGPT MCP does not ask for your ChatGPT password.

You sign in directly inside the ChatGPT browser window.

Prompts delegated through this MCP are sent to ChatGPT through your own signed-in ChatGPT account.

Do not share a browser profile folder that contains your login state.

## Quick Troubleshooting

### Codex does not see the tools

Restart Codex after running the installer.

### ChatGPT opens but says login is required

Sign in manually, then ask Codex to call:

```text
chatgpt_wait_for_login
```

### Prompt times out

The ChatGPT response may still be running.

Use a longer timeout for heavy research or Deep Research tasks.

### Model selection fails

Leave your preferred model selected manually in ChatGPT, then try delegation again.

### Deep Research fails

Make sure Deep Research is available in your ChatGPT account and visible in the browser UI.

If it still fails, start the Deep Research mode manually in ChatGPT and then retry delegation.

## Recommended First Test

After install and login, use this test from Codex:

```text
Use chatgpt_delegate to ask ChatGPT: Reply with exactly "CodexGPT MCP is working."
```

If Codex receives that answer back, the bridge is live.

## Summary

CodexGPT MCP gives Codex a way to hand research and information gathering to ChatGPT, then bring the finished answer back into your Codex workflow.

Use Codex for coding.

Use ChatGPT for research.

Let CodexGPT MCP bridge the two.
