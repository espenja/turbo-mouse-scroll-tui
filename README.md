# Explanation
Running `turbo watch dev` on Windows and cancelling the process with `ctrl + c` does not gracefully shut down the process and causes the terminal to act in weird ways.  

This happens when running `turbo` from global install (shown in video #1).  
Running `turbo` from `pnpm` does not seem to cause this "effect" (shown in video #2).  

Testing conditions:
- OS: Windows 11
- pnpm version: 9.5.0
- turbo version: 2.0.9
- tested terminals: pwsh and GitBash MINGW64 with xterm
- tested conditions:
  - Inside VSCode with pwsh with extensions enabled
  - Inside VSCode with pwsh with all extensions disabled
  - Outside of VSCode in Windows Terminal with pwsh
  - Outside of VSCode in GitBash MINGW64 with xterm

# What happens after ctrl + c after running global turbo install?
* Residual fragments of tui's interface is left on the screen
* Scrolling with the mouse wheel acts like arrow up/down instead of scrolling the terminal window/buffer

# Reproduction steps
- Be on Windows 11
- Have turbo version 2.0.9 installed globally
- clone reproduction repo: https://github.com/espenja/turbo-mouse-scroll-tui
- `pnpm install -g turbo`
- `pnpm install`
- `turbo watch dev`
- Cancel process with `ctrl+c`
- Scroll with mouse in terminal
  - **Expected behavior**: Terminal exits to previous state without fragments from TUI, and mouse scrolls the terminal buffer/window
  - **Actual behavior**: Terminal has lots of fragments from TUI, and mouse acts like arrow up and down and scrolls through terminal command history

# Screencap of what happens

## Failure scenario: Screencap of running turbo as a global install and scrolling with mouse wheel after cancelling process with ctrl+c (clicking image will take you to a YouTube video showing what happens)
[![Running global turbo install with turbo watch dev](https://github.com/user-attachments/assets/f6ec9c8a-fb16-4fb0-ba40-67a94b285b2b)](https://www.youtube.com/watch?v=9sa5KuQZIIY)

## Working scenario: Screencap of running turbo from pnpm and scrolling with mouse wheel after cancelling process with ctrl+c (clicking image will take you to a YouTube video showing what happens)

[![Running global turbo install with turbo watch dev](https://github.com/user-attachments/assets/72c50cf2-e9fb-4103-9920-c771fbdd3ebe)](https://youtu.be/vbiLEYmnAxo)
