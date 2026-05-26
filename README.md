# ChatGPT Subagent MCP Releases

ChatGPT Subagent MCP lets Codex hand work to your signed-in ChatGPT browser session, wait for ChatGPT to finish, and bring the answer back into Codex.

This public repository is for Windows release downloads and setup docs. The source code is kept in a private repository.

## What This Does

ChatGPT Subagent MCP gives Codex a local bridge to ChatGPT so Codex can ask ChatGPT to handle work that is better suited for your ChatGPT account and tool surface.

It can:

- Open or reuse a managed ChatGPT browser session.
- Detect when you need to sign in and wait for login to finish.
- Start a new ChatGPT conversation.
- Send prompts from Codex to ChatGPT.
- Wait for ChatGPT's response to finish.
- Return the final ChatGPT answer back into Codex.
- Use faster local handoff timing with `CHATGPT_SPEED_MODE=max_speed`.
- Attempt browser UI features such as model selection and Deep Research when your ChatGPT account exposes them.

Good uses include:

- Heavy research that you want ChatGPT to do outside the Codex model budget.
- Long reasoning tasks where ChatGPT's consumer app tools are useful.
- Asking ChatGPT to search the web, summarize findings, or draft a research brief for Codex.
- Letting Codex continue coding while ChatGPT handles a parallel research or analysis request.

## How It Works

At a high level:

1. Codex starts the local MCP server.
2. The MCP server opens or connects to a managed ChatGPT browser window.
3. You sign in to ChatGPT manually the first time.
4. Codex calls MCP tools such as `chatgpt_delegate`.
5. The MCP server types the prompt into ChatGPT, waits for the answer, reads it back, and returns it to Codex.

This is browser automation, not an official ChatGPT API. That means it uses your normal ChatGPT web session and can be affected by ChatGPT UI changes.

## Download

Get the latest Windows release here:

https://github.com/nexus382/chatgpt-subagent-mcp-releases/releases/latest

Download the zip asset named like this:

```text
chatgpt-subagent-mcp-0.8.0-windows.zip
```

## Install For Codex

Extract the zip somewhere normal, such as your Downloads folder or Documents folder.

Then run this from inside the extracted folder:

```powershell
powershell -ExecutionPolicy Bypass -File .\install-codex-chatgpt-subagent.ps1
```

Restart Codex after the installer finishes.

The installer updates your user-level Codex config so the MCP is available across Codex projects.

## First Run

After restarting Codex, ask Codex to open ChatGPT through the MCP:

```text
Use chatgpt_open.
```

If ChatGPT is not signed in, a browser window should open. Sign in manually.

Then ask Codex to wait for login:

```text
Use chatgpt_wait_for_login.
```

After login is ready, test a normal delegation:

```text
Use chatgpt_delegate to ask ChatGPT: Reply with exactly "MCP smoke test passed."
```

If it returns that phrase back into Codex, the bridge is working.

## Are The Tools Commands?

The `chatgpt_*` tools are MCP tools. They are mainly for Codex or another MCP-capable model client to call.

They are not normal PowerShell commands that you type directly like `git status`.

In practice, you use them by asking Codex to call them. For example:

```text
Use chatgpt_delegate to ask ChatGPT to research the latest MiniMax model news and bring the answer back here.
```

Codex sees the MCP tool, chooses the right parameters, calls it, waits for the result, and then shows you the answer.

Advanced users can run the MCP executable manually for debugging, but normal users should let Codex launch it.

## Available MCP Tools

These are the current tool names Codex can use:

| Tool | What it does |
| --- | --- |
| `chatgpt_open` | Opens or attaches to the managed ChatGPT browser session. |
| `chatgpt_status` | Reports whether the browser is ready, signed in, and usable. |
| `chatgpt_wait_for_login` | Waits while the user signs in manually. |
| `chatgpt_new_chat` | Starts a clean ChatGPT conversation. |
| `chatgpt_select_model` | Attempts to select a visible ChatGPT model by label. |
| `chatgpt_enable_deep_research` | Attempts to enable Deep Research in the ChatGPT UI. |
| `chatgpt_get_last_response` | Reads the latest visible ChatGPT assistant response. |
| `chatgpt_delegate` | Sends a prompt to ChatGPT and waits for the completed response. |
| `chatgpt_client_info` | Reports backend mode and capability flags. |

Most users will mainly use `chatgpt_delegate`.

## Browser Mode

Browser mode is the recommended and supported backend.

It uses a managed browser profile so your ChatGPT login can persist between runs. The first time, you sign in manually. After that, Codex can usually reuse the session.

Browser mode is currently the best path for:

- Normal prompt delegation.
- Response readback.
- New chats.
- Deep Research attempts.
- Faster handoff timing.

## Speed Mode

The MCP cannot make ChatGPT itself think, search, or run Deep Research faster. Those parts take however long ChatGPT takes.

What it can make faster is the local handoff between Codex and ChatGPT:

- Detecting when ChatGPT has stopped generating.
- Returning the completed response back to Codex sooner.
- Reducing local UI settle waits.

To opt into faster local polling, set this in the MCP `.env` file:

```text
CHATGPT_SPEED_MODE=max_speed
```

The default is safer and more conservative:

```text
CHATGPT_SPEED_MODE=token_saver
```

## Current Limitations

- This is an unofficial automation bridge.
- It does not use an official ChatGPT control API.
- ChatGPT UI changes can break selectors.
- Deep Research and model selection depend on what your ChatGPT account exposes.
- The Windows app backend is experimental and not recommended for public use yet.
- Browser mode is the production path right now.

## Safety Notes

- The MCP never asks for your ChatGPT password.
- You sign in directly inside the ChatGPT browser window.
- Prompts delegated through this MCP are sent to ChatGPT through your own account.
- Do not share a browser profile folder that contains your login state.

## Quick Troubleshooting

If Codex does not see the tools, restart Codex after running the installer.

If ChatGPT opens but says login is required, sign in manually, then ask Codex to call `chatgpt_wait_for_login`.

If a prompt times out, the ChatGPT response may still be running. Use a longer timeout for heavy research.

If model selection or Deep Research fails, leave your preferred model or mode selected in ChatGPT manually and try delegation again.
