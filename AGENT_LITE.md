# Warp Agent Lite (experimental)

This branch keeps the native GUI terminal and its CLI agent integration. It does not change terminal input handling, PTY, alternate screen, keymaps, mouse tracking, selection, clipboard, tab/pane navigation, scrollback limits or renderer.

## Changes

- The desktop launch mode no longer builds/restores Warp's own repository indices or RepoOutlines indexing. External agents manage their own repository context. Native Warp agents still run, but built-in codebase indexing is unavailable in the desktop app. Headless/remote launch modes retain their original behavior.
- Codebase context, project explorer, global search, Warp Drive and telemetry are off by default. Existing explicit preferences may override these defaults. Disabling Drive in settings hides its surface, not all cloud infrastructure. No user data is deleted.
- The initial feature set excludes global AI analytics, active-app event recording, Figma detection, the Get Started tab and automatic opening of code review. No shortcut definitions are removed.
- Agent session tracking and CLI detection remain unchanged (Codex, Claude Code, Antigravity/agy, OpenCode, etc.).

## Build on macOS

```bash
./script/bootstrap --skip-common-skills
WARP_SKIP_COMMON_SKILLS_INSTALL=1 ./script/run --release
```

Use the release build for performance comparisons. For an existing profile, check the five defaults in Settings; stored settings can override defaults. Keep the existing OEM app until the new build has been validated.

## Validation checklist

- Build the macOS app and run relevant existing input/keymap/terminal tests before daily use.
- Compare identical workloads at 1, 5, 10 and 20 tabs, each using the same CLI and repository; compare idle and active CPU, resident memory, GPU and memory pressure. Include child agent processes separately.
- Verify all existing custom shortcuts, tab switching, split panes, clipboard, drag selection, mouse reporting, wheel scrolling, alternate screen, bracketed paste, Ctrl+C, IME and resizing.
- Launch Codex, Claude, agy and OpenCode and verify typing, redraws, mouse events, notifications and session switching. Test native Warp agent separately with indexing unavailable.

No macOS compilation, benchmark or interactive regression testing was performed when this change was prepared. This is a first runtime-reduction pass, not a fully stripped binary; shared libraries and other singleton services remain. Do not infer measured performance gains from the feature list.
