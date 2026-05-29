# WowNow Device States Context

This project started from a Figma Make splash animation and was converted into a static GitHub Pages site.

## Current Purpose

Show device state animations for WowNow-style device flows:

- Boot / startup loading
- Shutdown loading
- Standby card placement
- Read card failure
- Wi-Fi connecting
- Wi-Fi connected
- Wi-Fi disconnected
- Wi-Fi connection failure
- NFC web loading
- NFC web loading failure
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
    wifi-connecting-tier-1.svg
    wifi-connecting-tier-2.svg
    wifi-connecting-tier-3.svg
    wifi-failed.svg
    wifi-success.svg
    wifi-status.svg
```

## Animation Rules

- Background is a WebGL aurora-style glow based on the original Figma Make `Aurora.tsx` shader.
- Background speed is slower than the original: `speed = 0.55`.
- Large-screen scaling:
  - The page uses `1280 x 720` as the base design size.
  - `--ui-scale` stays at `1` at or below the base size, then grows with the viewport up to `1.65` so center icons/text and the top-right Wi-Fi status icon do not look tiny on TV-sized displays.
  - `--aurora-scale` grows up to `1.2` on larger screens to keep the bottom glow visually fuller.
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
- Read card failure state:
  - Figma node: `412:739`
  - State id: `read-card-failed`
  - Uses the shared global aurora background, top-right Wi-Fi icon, centered Timecho device, inserted card, and failure copy
  - Reuses `standby-timecho.png` as the device base and CSS-renders the inserted card to match Figma
  - The `failed` dot-matrix content is generated from Figma dot coordinates and loops like a signal light: appears, stays lit briefly, fades out, then appears again
  - Main copy: `读卡失败`
- NFC web loading state:
  - Figma node: `412:622`
  - State id: `nfc-web-loading`
  - Uses the shared global aurora background and top-right Wi-Fi icon
  - Center content is CSS-rendered so the spinner and breathing circles can animate independently
  - Loading spinner rotates continuously
  - `circle1` and `circle2` are staggered expanding ripples that move at a consistent rate, pass through the circle1 size, then grow to the outer circle size and fade out
  - Main copy: `网页加载中`
- Wi-Fi disconnected state:
  - Figma node: `412:637`
  - State id: `nfc-wifi-disconnected`
  - Uses the shared global aurora background and a failed Wi-Fi icon in the top-right status position
  - Reuses the NFC ripple animation timing for `circle1` and `circle2`
  - Ripple color follows Figma: `#FFE60A`
  - Center symbol uses `assets/ui-icons/wifi-failed.svg` with a yellow glow
  - Main copy: `Wi-Fi未连接`
- Wi-Fi connecting state:
  - Figma node: `412:681`
  - State id: `nfc-wifi-connecting`
  - Uses the shared global aurora background and a failed/connecting Wi-Fi icon in the top-right status position
  - Reuses the NFC ripple animation timing for `circle1` and `circle2`
  - Ripple color follows Figma: `#FFE60A`
  - Center Wi-Fi symbol is split into three local SVG tiers:
    `wifi-connecting-tier-1.svg`, `wifi-connecting-tier-2.svg`, and `wifi-connecting-tier-3.svg`
  - First tier stays at 100% opacity; second and third tiers loop from 45% to 100% opacity in sequence
  - Main copy: `Wi-Fi连接中...`
- Wi-Fi connected state:
  - Figma node: `412:702`
  - State id: `nfc-wifi-connected`
  - Uses the shared global aurora background and normal top-right Wi-Fi icon
  - Reuses the NFC ripple animation timing for `circle1` and `circle2`
  - Ripple color follows Figma: `#27FF0A`
  - Center symbol uses `assets/ui-icons/wifi-success.svg`
  - Main copy: `Wi-Fi连接成功`
- Wi-Fi connection failed state:
  - State id: `nfc-wifi-connection-failed`
  - Uses the same style, motion, top-right failed Wi-Fi icon, and yellow ripple treatment as the Wi-Fi disconnected state
  - Ripple color follows Figma Wi-Fi failure style: `#FFE60A`
  - Center symbol uses `assets/ui-icons/wifi-failed.svg` with a yellow glow
  - Main copy: `Wi-Fi连接失败`
- NFC web loading failure state:
  - Figma node: `412:722`
  - State id: `nfc-web-loading-failed`
  - Uses the shared global aurora background and top-right Wi-Fi icon
  - Reuses the NFC loading ripple animation, with red UI colors from Figma
  - Center symbol is a CSS-rendered red failure icon
  - Main copy: `网页加载失败`

## UI

There is a tiny state switcher in the top-left corner:

```text
‹ 开机 ›
```

It cycles between available states. Current states are:

- 开机
- 待机
- 读卡失败
- Wi-Fi未连接
- Wi-Fi连接中
- Wi-Fi连接成功
- Wi-Fi连接失败
- 加载
- 加载失败
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
