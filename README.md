# ChatGPT Subagent MCP Releases

This repository hosts public Windows release downloads for ChatGPT Subagent MCP.

ChatGPT Subagent MCP lets Codex delegate work to a signed-in ChatGPT browser
session and return the completed answer back into Codex.

## Download

Use the latest release:

```text
https://github.com/nexus382/chatgpt-subagent-mcp-releases/releases/latest
```

Download the Windows zip asset, extract it to a normal user-writable folder, and
run:

```powershell
powershell -ExecutionPolicy Bypass -File .\install-codex-chatgpt-subagent.ps1
```

Restart Codex after installation.

## First Run

After Codex restarts, ask Codex to call:

```text
chatgpt_open
```

If login is required, sign into ChatGPT in the managed browser window opened by
the MCP. Then ask Codex to call:

```text
chatgpt_wait_for_login
```

Finally, test delegation:

```text
Use chatgpt_delegate to ask ChatGPT: Reply with exactly "MCP smoke test passed."
```

## Notes

- Browser mode is the supported backend.
- Windows app mode is not recommended in the public release.
- `max_speed` makes local response detection faster. It does not make ChatGPT's
  own model, search, or Deep Research work complete faster.
- This public release repository does not contain the private source code.
