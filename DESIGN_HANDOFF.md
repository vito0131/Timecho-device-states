# Design Handoff

## Standby Card Placement State

Figma source:

```text
TimeEcho_UI
Frame: 待机状态-静待放卡
Node: 412:53
```

### Developer Names

| Figma layer | Developer name | Local asset / selector | Notes |
| --- | --- | --- | --- |
| `待机状态-静待放卡` | `standbyCardPlacementState` | `#standby-state` | Full standby state layer |
| `icon/wifi` | `wifiStatusIcon` | `assets/ui-icons/wifi-status.svg`, `.wifi-status-icon` | Top-right Wi-Fi icon |
| `content` | `standbyCardPlacementContent` | `.standby-card-content` | Center content group |
| `timecho` | `standbyTimeEchoDevice` | `assets/ui-icons/standby-timecho.png`, `.standby-card-timecho` | Device/base illustration without the card |
| `card` | `standbyPlacementCard` | `assets/ui-icons/standby-card.png`, `.standby-card-placement-card` | Separate card illustration for loop animation |
| `text` | `standbyCardInstructionContainer` | text wrapper in `.standby-card-content` | Instruction block |
| `请将卡片放入示意处` | `standbyCardInstruction` | `.standby-card-instruction` | User-facing copy |

### Background Rule

The aurora glow is a global scene layer shared by every device state. New states should replace only the center content/status content unless a state explicitly needs a terminal effect, such as shutdown fading to black at the end.

### Copy

```text
请将卡片放入示意处
```

Suggested i18n key:

```text
standby.cardPlacement.instruction
```

### Layout Reference

Original frame size:

```text
1280 x 720
```

Main positions from Figma:

```text
wifiStatusIcon: x=1146, y=60, width=34, height=34
standbyCardPlacementContent: x=499, y=254.5, width=272, height=273
standbyTimeEchoDevice: x=12, y=20, width=258.243, height=160.301
standbyPlacementCard: x=55, y=3, width=94, height=57
standbyCardInstruction: font=PingFang SC Medium, size=22px, color=#FFFFFF
```

## NFC Web Loading State

Figma source:

```text
TimeEcho_UI
Frame: 放入NFC卡片-网页加载中
Node: 412:622
```

### Developer Names

| Figma layer | Developer name | Local selector | Notes |
| --- | --- | --- | --- |
| `放入NFC卡片-网页加载中` | `nfcWebLoadingState` | `#nfc-loading-state` | Full NFC web loading state layer |
| `icon/wifi` | `wifiStatusIcon` | `assets/ui-icons/wifi-status.svg`, `.wifi-status-icon` | Shared top-right Wi-Fi icon |
| `content` | `nfcWebLoadingContent` | `.nfc-loading-content` | Center content group |
| `circle1` | `nfcLoadingPrimaryRipple` | `.nfc-loading-circle.ripple-primary` | First expanding ripple |
| `circle2` | `nfcLoadingSecondaryRipple` | `.nfc-loading-circle.ripple-secondary` | Second expanding ripple, offset after the first |
| `loading` | `nfcLoadingSpinner` | `.nfc-loading-spinner` | CSS spinner, rotates continuously |
| `网页加载中` | `nfcWebLoadingCopy` | `.nfc-loading-copy` | User-facing copy |

### Copy

```text
网页加载中
```

Suggested i18n key:

```text
nfc.webLoading.copy
```

### Motion

```text
nfcLoadingSpinner: 1.1s linear infinite rotation
nfcLoadingPrimaryRipple: 1.55s linear expanding circle, passes through the circle1 size and keeps fading until the outer circle size
nfcLoadingSecondaryRipple: 1.55s expanding circle, starts 0.58s after primary ripple
```

### Layout Reference

Original frame size:

```text
1280 x 720
```

Main positions from Figma:

```text
wifiStatusIcon: x=1146, y=60, width=34, height=34
nfcWebLoadingContent: x=509, y=264.5, width=262, height=253
nfcLoadingIndicator: x=51, y=0, width=160, height=160
nfcLoadingInnerBreathingCircle: x=20.87, y=20.87, width=118.26, height=118.26
nfcLoadingOuterBreathingCircle: x=0, y=0, width=160, height=160
nfcLoadingSpinner: x=44.72, y=44.72, width=70.56, height=70.56
nfcWebLoadingCopy: font=PingFang SC Medium, size=22px, color=#FFFFFF
```
