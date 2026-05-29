# WowNow Device States Context

This project started from a Figma Make splash animation and was converted into a static GitHub Pages site.

## Current Purpose

Show device state animations for WowNow-style device flows:

- Boot / startup loading
- Shutdown loading
- Standby card placement
- NFC web loading
- Future states such as standby, updating, connecting, etc.

The page is currently a pure static site with no backend and no API connection. It is meant for visual demonstration and review.

## Current URL

GitHub repository:

```text
https://github.com/vito0131/fluid-glow-splash
```

GitHub Pages URL:

```text
https://vito0131.github.io/fluid-glow-splash/
```

## Current Files

```text
index.html
assets/
  Logo.gif
  logo-sequence/
    frame_0001.png ... frame_0118.png
  shutdown-sequence/
    frame_0001.png ... frame_0159.png
  ui-icons/
    standby-card.png
    standby-timecho.png
    wifi-status.svg
```

## Animation Rules

- Background is a WebGL aurora-style glow based on the original Figma Make `Aurora.tsx` shader.
- Background speed is slower than the original: `speed = 0.55`.
- Boot logo sequence:
  - Path: `assets/logo-sequence`
  - 118 frames
  - 18fps
  - Loops forever
- Shutdown logo sequence:
  - Path: `assets/shutdown-sequence`
  - 159 frames
  - 18fps
  - Plays once
  - Background stays bright for the first 72% of the animation
  - Background fades out during the final 28%
  - Logo clears at the end
  - Final state is black screen
- Standby card placement state:
  - Figma node: `412:53`
  - State id: `standby-card-placement`
  - Uses the shared global aurora background, top-right Wi-Fi icon, centered split content, and instruction text
  - Center content is separated into `standby-timecho.png` and `standby-card.png` so the card can animate independently
  - Main copy: `请将卡片放入示意处`
  - Developer naming details live in `DESIGN_HANDOFF.md`
- NFC web loading state:
  - Figma node: `412:622`
  - State id: `nfc-web-loading`
  - Uses the shared global aurora background and top-right Wi-Fi icon
  - Center content is CSS-rendered so the spinner and breathing circles can animate independently
  - Loading spinner rotates continuously
  - `circle1` and `circle2` are staggered expanding ripples that move at a consistent rate, pass through the circle1 size, then grow to the outer circle size and fade out
  - Main copy: `网页加载中`

## UI

There is a tiny state switcher in the top-left corner:

```text
‹ 开机 ›
```

It cycles between available states. Current states are:

- 开机
- 待机
- 加载
- 关机

Shutdown is kept as the final state. Future non-terminal states should be inserted before the shutdown state so the review order stays like:

```text
开机 -> 待机 -> 新增状态 -> 关机
```

## Local Preview

From the project directory:

```bash
python3 -m http.server 4173
```

Open:

```text
http://localhost:4173/index.html
```

## Workflow Preference

For animation tuning, work locally first. Do not push every small adjustment to GitHub Pages.

Preferred flow:

1. Edit locally
2. Preview locally
3. User reviews locally
4. Only when the user says "可以上传", commit and push

GitHub Desktop is currently used for authenticated pushes because the terminal does not have GitHub credentials.
