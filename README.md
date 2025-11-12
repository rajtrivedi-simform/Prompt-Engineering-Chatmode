# Prompt-Engineering Chat Mode (Repository)

This repository contains a workspace-level instruction file that customizes the behavior of the Copilot/Chat agent when contributors use the "Prompt-Engineering" chat mode. The instructions shape how the agent formats outputs, what role it assumes, and what it does (or doesn't do) before receiving confirmation from the user.

This README explains the chat mode, summarizes the repository-level instructions, and lists steps to configure the behavior both at the workspace (repository) level and at the user level in Visual Studio Code.

## What this chat mode does

- Role: The agent switches into a "Prompt Engineer" role and focuses on rewriting/optimizing user prompts.
- Output format: The agent produces two sections on every iteration:
  1. Revised/Final Prompt — the rewritten/optimized prompt enclosed in a code block for easy copy/paste.
 2. Clarification Questions — any follow-up questions needed to finish the optimization (or `None` when no questions are needed).
- Flow control: After producing the optimized prompt the agent waits for explicit confirmation from the user before taking any implementation actions.

These rules are codified in the repository file:

- `.github/copilot-instructions.md` — the file used by the workspace to instruct the agent about the Prompt-Engineering chat mode (already present in this repo).

## Files to inspect

- `.github/copilot-instructions.md`
  - Purpose: workspace-level instructions for the chat agent. This file includes the agent behavior and output formatting rules for the Prompt-Engineering chat mode.

## Configure at the workspace (repository) level

To make the repository provide the chat-mode instructions for all contributors who open it in a compatible Copilot/Chat integration, ensure the following:

1. Add or update the file `.github/copilot-instructions.md` in the repository (this repo already contains it).
   - Place the instruction document under the `.github/` folder so the agent and integrations that look for repo-scoped instructions can pick it up.
2. Keep the instructions clear and focused (the current file in this repo is an example of a Prompt-Engineering policy). The file should state the role, required output structure, and interaction rules (for example: wait for explicit user confirmation before implementing).
3. Commit and push the changes. When contributors open the repository in VS Code (or other supported editors that read repository instruction files), the Copilot/Chat integration will typically surface or honor the repo instructions.

Notes:
- The exact behavior and how integrations honor `.github/copilot-instructions.md` depends on the editor and Copilot/Chat implementation/version. Treat the repository file as the canonical guidance for this project and keep it up to date.

## Configure at the user (VS Code) level

Users can control how Copilot/Chat behaves locally in two primary ways: adjusting VS Code settings (User or Workspace scope) and keeping repository instruction files (like `.github/copilot-instructions.md`) in the project.

Recommended steps (UI):

1. Open Visual Studio Code.
2. Open Settings (File → Preferences → Settings or use the gear icon).
3. Search for "Copilot" or "GitHub Copilot" in Settings.
4. Review and set the extension options you want. You can choose whether Copilot is enabled globally (User) or only for the current workspace (Workspace) using the scope selector in the Settings UI.

Alternative: edit `settings.json` (User or Workspace) via the command palette (`Preferences: Open Settings (JSON)`) and set Copilot-related preferences there. Use the Settings UI to discover the exact keys available in your installed Copilot/Chat extension version.

Tips:
- Prefer leaving the workspace-level file (`.github/copilot-instructions.md`) in place: it gives consistent behaviour across contributors.
- Use the Settings UI to change the enable/disable scope (User vs Workspace) so you control whether Copilot features apply to all projects or just this one.

## Example workflow when using Prompt-Engineering chat mode

1. Open this repository in VS Code.
2. Start a chat and switch to the "Prompt-Engineering" chat mode (if supported by your Copilot/Chat UI).
3. The agent will adopt the Prompt Engineer role and return a Revised/Final Prompt (in a code block) plus any Clarification Questions.
4. Review the revised prompt. If it looks good, confirm to the agent to continue or ask it to implement the prompt.

Important: The agent will not perform implementation steps automatically after generating the revised prompt — it will wait for explicit confirmation.

## Contributing and modifying the chat instructions

- If you'd like to change the repository-level behavior, edit `.github/copilot-instructions.md` and update the instructions.
- Keep changes small and well-documented. Prefer short, deterministic rules (role, required output structure, and interaction controls).

## Further reading and troubleshooting

- If your editor does not appear to respect the repository instructions, verify:
  - You have a recent Copilot/Chat extension installed.
  - The extension supports repository-level instruction files.
  - There are no conflicting workspace or user settings that override the behavior.
- Consult the extension's documentation for how it consumes repo-supplied instruction files.

## Summary

This repo contains a Prompt-Engineering chat-mode instruction file under `.github/`. The file defines a predictable, safe workflow for optimizing prompts: produce a Revised/Final Prompt and Clarification Questions, then wait for user confirmation before implementing. Configure behavior at the workspace level by editing the `.github/` instruction file and at the user level via VS Code Settings (either UI or settings.json), choosing User or Workspace scope as you prefer.

---