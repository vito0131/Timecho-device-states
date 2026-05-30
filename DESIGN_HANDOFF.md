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

### Motion

```text
standbyPlacementCard: 2.1s ease-in-out loop
standbyPlacementCardDrop: 15px via --standby-card-drop
sequence: transparent -> fade to 100% opacity -> drop into slot -> short hold -> quick fade out in the inserted position -> repeat
```

### Background Rule

The aurora glow is a global scene layer shared by every device state. New states should replace only the center content/status content unless a state explicitly needs a terminal effect, such as shutdown fading to black at the end.

### Responsive Display Scaling

The implementation treats `1280 x 720` as the base design size. At or below that size, state content remains at 1x so the current browser preview keeps the intended proportions.

On larger displays, JavaScript updates two CSS variables on `.stage`:

```text
--ui-scale: 1 -> 1.65
--aurora-scale: 1 -> 1.2
```

`--ui-scale` is applied to the centered state content, startup/shutdown logo, and top-right Wi-Fi status icon. `--aurora-scale` vertically expands the shared WebGL glow so TV-sized screens do not make the background feel like only a thin bottom strip.

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

## Read Card Failed State

Figma source:

```text
TimeEcho_UI
Frame: 放入NFC卡片-读卡失败
Node: 412:739
```

### Developer Names

| Figma layer | Developer name | Local asset / selector | Notes |
| --- | --- | --- | --- |
| `放入NFC卡片-读卡失败` | `readCardFailedState` | `#read-card-failed-state` | Full read-card failure state layer |
| `icon/wifi` | `wifiStatusIcon` | `assets/ui-icons/wifi-status.svg`, `.wifi-status-icon` | Shared top-right Wi-Fi icon |
| `content` | `readCardFailedContent` | `.read-card-failed-content` | Center content group |
| `timecho` | `readCardFailedTimeEchoDevice` | `assets/ui-icons/standby-timecho.png`, `.read-card-failed-timecho` | Reused device/base illustration |
| `card` | `readCardFailedInsertedCard` | `.read-card-failed-card` | CSS-rendered inserted card, static |
| `failed` | `readCardFailedDotMatrix` | `.read-card-failed-matrix`, `.read-card-failed-dot` | CSS/JS-generated dot matrix from Figma coordinates |
| `读卡失败` | `readCardFailedCopy` | `.read-card-failed-copy` | User-facing copy |

### Copy

```text
读卡失败
```

Suggested i18n key:

```text
nfc.readCard.failed.copy
```

### Motion

```text
readCardFailedDotMatrix: 4.4s signal-light loop, hidden -> lit for a few seconds -> hidden -> repeat
```

### Layout Reference

Original frame size:

```text
1280 x 720
```

Main positions from Figma:

```text
wifiStatusIcon: x=1146, y=60, width=34, height=34
readCardFailedContent: x=499, y=267, width=272, height=256
readCardFailedVisual: x=0, y=0, width=272, height=163
readCardFailedTimeEchoDevice: x=12, y=3, width=258.243, height=160.301
readCardFailedInsertedCard: x=55, y=3, width=94, height=57
readCardFailedDotMatrix: x=41, y=81, width=123, height=43
readCardFailedCopy: font=PingFang SC Medium, size=22px, color=#FFFFFF
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
| `circle1` | `nfcLoadingPrimaryRipple` | `.nfc-loading-circle.ripple-primary` | Static outer ring, 5% opacity; ripple animation disabled |
| `circle2` | `nfcLoadingSecondaryRipple` | `.nfc-loading-circle.ripple-secondary` | Static inner ring, 10% opacity; ripple animation disabled |
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
nfcLoadingPrimaryRipple: static outer ring, 5% opacity, no animation
nfcLoadingSecondaryRipple: static inner ring, 10% opacity, no animation
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

## NFC Wi-Fi Connecting State

Figma source:

```text
TimeEcho_UI
Frame: 配网-配网进行中
Node: 412:681
```

### Developer Names

| Figma layer | Developer name | Local asset / selector | Notes |
| --- | --- | --- | --- |
| `配网-配网进行中` | `nfcWifiConnectingState` | `#nfc-wifi-connecting-state` | Full Wi-Fi connecting state layer |
| `icon/wifi failed` | `wifiFailedStatusIcon` | `assets/ui-icons/wifi-failed.svg`, `.wifi-status-icon` | Top-right failed/connecting Wi-Fi icon |
| `content` | `nfcWifiConnectingContent` | `.nfc-wifi-connecting-content` | Center content group |
| `Wi-Fi connecting` | `nfcWifiConnectingIndicator` | `.nfc-wifi-connecting-indicator` | Shared indicator wrapper; ripple circles are static |
| `circle2` | `nfcWifiConnectingPrimaryRipple` | `.nfc-loading-circle.ripple-primary` | Static outer ring, 5% opacity; ripple animation disabled |
| `circle1` | `nfcWifiConnectingSecondaryRipple` | `.nfc-loading-circle.ripple-secondary` | Static inner ring, 10% opacity; ripple animation disabled |
| `第一格` | `nfcWifiConnectingTier1` | `assets/ui-icons/wifi-connecting-tier-1.svg`, `.nfc-wifi-connecting-tier-1` | Loops from 45% to 100% opacity first |
| `第二格` | `nfcWifiConnectingTier2` | `assets/ui-icons/wifi-connecting-tier-2.svg`, `.nfc-wifi-connecting-tier-2` | Loops from 45% to 100% opacity after tier 1 |
| `第三格` | `nfcWifiConnectingTier3` | `assets/ui-icons/wifi-connecting-tier-3.svg`, `.nfc-wifi-connecting-tier-3` | Loops from 45% to 100% opacity after tier 2 |
| `Wi-Fi连接中…` | `nfcWifiConnectingCopy` | `.nfc-loading-copy` | User-facing copy |

### Copy

```text
Wi-Fi连接中...
```

Suggested i18n key:

```text
nfc.wifiConnecting.copy
```

### Motion

```text
nfcWifiConnectingPrimaryRipple: static outer ring, 5% opacity, no animation
nfcWifiConnectingSecondaryRipple: static inner ring, 10% opacity, no animation
nfcWifiConnectingTier1: 0.72s ease-in-out opacity loop, 45% -> 100% -> 45%
nfcWifiConnectingTier2: 0.72s ease-in-out opacity loop after tier 1, 45% -> 100% -> 45%
nfcWifiConnectingTier3: 0.72s ease-in-out opacity loop after tier 2, 45% -> 100% -> 45%
```

### Color Reference

```text
nfcWifiConnectingRipple: #FFE60A
nfcWifiConnectingSymbolGlow: rgba(255, 230, 10, 0.9)
```

### Layout Reference

Original frame size:

```text
1280 x 720
```

Main positions from Figma:

```text
wifiFailedStatusIcon: x=1146, y=60, width=34, height=34
nfcWifiConnectingContent: x=509, y=264.5, width=262, height=253
nfcWifiConnectingIndicator: x=50.5, y=0, width=161, height=161
nfcWifiConnectingOuterRipple: x=0, y=0, width=161, height=161
nfcWifiConnectingInnerRipple: x=21, y=21, width=119, height=119
nfcWifiConnectingSymbol: x=46.5, y=45, width=69, height=69
nfcWifiConnectingCopy: font=PingFang SC Medium, size=22px, color=#FFFFFF
```

## NFC Wi-Fi Connected State

Figma source:

```text
TimeEcho_UI
Frame: 配网-配网成功
Node: 412:702
```

### Developer Names

| Figma layer | Developer name | Local asset / selector | Notes |
| --- | --- | --- | --- |
| `配网-配网成功` | `nfcWifiConnectedState` | `#nfc-wifi-connected-state` | Full Wi-Fi connected state layer |
| `icon/wifi` | `wifiStatusIcon` | `assets/ui-icons/wifi-status.svg`, `.wifi-status-icon` | Top-right connected Wi-Fi icon |
| `content` | `nfcWifiConnectedContent` | `.nfc-wifi-connected-content` | Center content group |
| `success` | `nfcWifiConnectedIndicator` | `.nfc-wifi-connected-indicator` | Shared indicator wrapper; ripple circles are static |
| `circle2` | `nfcWifiConnectedPrimaryRipple` | `.nfc-loading-circle.ripple-primary` | Static outer ring, 5% opacity; ripple animation disabled |
| `circle1` | `nfcWifiConnectedSecondaryRipple` | `.nfc-loading-circle.ripple-secondary` | Static inner ring, 10% opacity; ripple animation disabled |
| `wifi not connected` | `nfcWifiConnectedWifiSymbol` | `assets/ui-icons/wifi-success-tier-1.svg` ... `wifi-success-tier-3.svg`, `.nfc-wifi-connected-symbol` | Center Wi-Fi arc icon |
| `success` | `nfcWifiConnectedSuccessBadge` | `assets/ui-icons/wifi-success-badge.svg`, `.nfc-wifi-connected-badge` | Small success badge layered over the Wi-Fi icon |
| `Wi-Fi连接成功` | `nfcWifiConnectedCopy` | `.nfc-loading-copy` | User-facing copy |

### Copy

```text
Wi-Fi连接成功
```

Suggested i18n key:

```text
nfc.wifiConnected.copy
```

### Motion

```text
nfcWifiConnectedPrimaryRipple: static outer ring, 5% opacity, no animation
nfcWifiConnectedSecondaryRipple: static inner ring, 10% opacity, no animation
nfcWifiConnectedWifiSymbol: static white Wi-Fi arcs
nfcWifiConnectedSuccessBadge: static green badge offset to the lower right of the Wi-Fi arcs
```

### Color Reference

```text
nfcWifiConnectedRipple: #27FF0A
nfcWifiConnectedSymbol: #66FFAE -> #0FB44B
nfcWifiConnectedSymbolGlow: rgba(60, 255, 42, 0.75)
```

### Layout Reference

Original frame size:

```text
1280 x 720
```

Main positions from Figma:

```text
wifiStatusIcon: x=1146, y=60, width=34, height=34
nfcWifiConnectedContent: x=509, y=264.5, width=262, height=253
nfcWifiConnectedIndicator: x=50.5, y=0, width=161, height=161
nfcWifiConnectedOuterRipple: x=0, y=0, width=161, height=161
nfcWifiConnectedInnerRipple: x=21, y=21, width=119, height=119
nfcWifiConnectedCopy: font=PingFang SC Medium, size=22px, color=#FFFFFF
```

## NFC Wi-Fi Disconnected State

Figma source:

```text
TimeEcho_UI
Frame: 放入NFC卡片- Wi-Fi未连接-静
Node: 412:637
```

### Developer Names

| Figma layer | Developer name | Local asset / selector | Notes |
| --- | --- | --- | --- |
| `放入NFC卡片- Wi-Fi未连接-静` | `nfcWifiDisconnectedState` | `#nfc-wifi-disconnected-state` | Full Wi-Fi disconnected state layer |
| `icon/wifi failed` | `wifiFailedStatusIcon` | `assets/ui-icons/wifi-failed.svg`, `.wifi-status-icon` | Top-right failed Wi-Fi icon |
| `content` | `nfcWifiDisconnectedContent` | `.nfc-wifi-disconnected-content` | Center content group |
| `not connect` | `nfcWifiDisconnectedIndicator` | `.nfc-wifi-disconnected-indicator` | Shared indicator wrapper; ripple circles are static |
| `circle1` | `nfcWifiDisconnectedPrimaryRipple` | `.nfc-loading-circle.ripple-primary` | Static outer ring, 5% opacity; ripple animation disabled |
| `circle1_2` | `nfcWifiDisconnectedSecondaryRipple` | `.nfc-loading-circle.ripple-secondary` | Static inner ring, 10% opacity; ripple animation disabled |
| `wifi not connected` | `nfcWifiDisconnectedSymbol` | `.nfc-wifi-disconnected-symbol` | Center failed Wi-Fi icon with yellow glow |
| `Wi-Fi未连接` | `nfcWifiDisconnectedCopy` | `.nfc-loading-copy` | User-facing copy |

### Copy

```text
Wi-Fi未连接
```

Suggested i18n key:

```text
nfc.wifiDisconnected.copy
```

### Motion

```text
nfcWifiDisconnectedPrimaryRipple: static outer ring, 5% opacity, no animation
nfcWifiDisconnectedSecondaryRipple: static inner ring, 10% opacity, no animation
```

### Color Reference

```text
nfcWifiDisconnectedRipple: #FFE60A
nfcWifiDisconnectedSymbolGlow: rgba(255, 230, 10, 0.9)
```

### Layout Reference

Original frame size:

```text
1280 x 720
```

Main positions from Figma:

```text
wifiFailedStatusIcon: x=1146, y=60, width=34, height=34
nfcWifiDisconnectedContent: x=509, y=264.5, width=262, height=253
nfcWifiDisconnectedIndicator: x=50.5, y=0, width=161, height=161
nfcWifiDisconnectedOuterRipple: x=0, y=0, width=161, height=161
nfcWifiDisconnectedInnerRipple: x=21, y=21, width=119, height=119
nfcWifiDisconnectedCopy: font=PingFang SC Medium, size=22px, color=#FFFFFF
```

## NFC Wi-Fi Connection Failed State

This state intentionally mirrors the Wi-Fi disconnected visual treatment and motion, with only the user-facing state name/copy changed for handoff clarity.

### Developer Names

| Figma layer | Developer name | Local asset / selector | Notes |
| --- | --- | --- | --- |
| `Wi-Fi连接失败` | `nfcWifiConnectionFailedState` | `#nfc-wifi-connection-failed-state` | Full Wi-Fi connection failure state layer |
| `icon/wifi failed` | `wifiFailedStatusIcon` | `assets/ui-icons/wifi-failed.svg`, `.wifi-status-icon` | Top-right failed Wi-Fi icon |
| `content` | `nfcWifiConnectionFailedContent` | `.nfc-wifi-connection-failed-content` | Center content group |
| `not connected` | `nfcWifiConnectionFailedIndicator` | `.nfc-wifi-connection-failed-indicator` | Center indicator wrapper |
| `not connected` contents | `nfcWifiConnectionFailedSymbol` | `assets/ui-icons/wifi-connection-failed.svg`, `.nfc-wifi-connection-failed-symbol` | Figma-matched composite with yellow rings, white Wi-Fi arcs, and red failure badge |
| `Wi-Fi连接失败` | `nfcWifiConnectionFailedCopy` | `.nfc-loading-copy` | User-facing copy |

### Copy

```text
Wi-Fi连接失败
```

Suggested i18n key:

```text
nfc.wifiConnectionFailed.copy
```

### Motion

```text
nfcWifiConnectionFailedSymbol: static composite SVG with static outer/inner rings, Wi-Fi arcs, and failure badge
```

### Color Reference

```text
nfcWifiConnectionFailedRipple: #FFE60A
nfcWifiConnectionFailedBadge: #FF9694 -> #D42C2A
nfcWifiConnectionFailedBadgeGlow: rgba(255, 42, 42, 0.8)
```

### Layout Reference

Matches the Figma Wi-Fi connection failed layout:

```text
wifiFailedStatusIcon: x=1146, y=60, width=34, height=34
nfcWifiConnectionFailedContent: x=509, y=264.5, width=262, height=253
nfcWifiConnectionFailedIndicator: x=50.5, y=0, width=161, height=161
nfcWifiConnectionFailedSymbol: x=0, y=0, width=161, height=161
nfcWifiConnectionFailedCopy: font=PingFang SC Medium, size=22px, color=#FFFFFF
```

## NFC Web Loading Failed State

Figma source:

```text
TimeEcho_UI
Frame: 放入NFC卡片-网页加载失败
Node: 412:722
```

### Developer Names

| Figma layer | Developer name | Local selector | Notes |
| --- | --- | --- | --- |
| `放入NFC卡片-网页加载失败` | `nfcWebLoadingFailedState` | `#nfc-loading-failed-state` | Full NFC web loading failed state layer |
| `icon/wifi` | `wifiStatusIcon` | `assets/ui-icons/wifi-status.svg`, `.wifi-status-icon` | Shared top-right Wi-Fi icon |
| `content` | `nfcWebLoadingFailedContent` | `.nfc-loading-failed-content` | Center content group |
| `circle1` | `nfcLoadingFailedPrimaryRipple` | `.nfc-loading-circle.ripple-primary` | Static outer ring, 5% opacity; ripple animation disabled |
| `circle2` | `nfcLoadingFailedSecondaryRipple` | `.nfc-loading-circle.ripple-secondary` | Static inner ring, 10% opacity; ripple animation disabled |
| `loaed failed` | `nfcLoadingFailedSymbol` | `.nfc-loading-failed-symbol` | CSS-rendered red failure icon |
| `网页加载失败` | `nfcWebLoadingFailedCopy` | `.nfc-loading-copy` | User-facing copy |

### Copy

```text
网页加载失败
```

Suggested i18n key:

```text
nfc.webLoading.failed.copy
```

### Color Reference

```text
nfcLoadingFailedRipple: #FF3C39 -> #D42C2A
nfcLoadingFailedSymbol: #FF9694 -> #D42C2A
nfcLoadingFailedSymbolGlow: rgba(255, 42, 42, 0.8)
```

### Layout Reference

Original frame size:

```text
1280 x 720
```

Main positions from Figma:

```text
wifiStatusIcon: x=1146, y=60, width=34, height=34
nfcWebLoadingFailedContent: x=509, y=263.5, width=262, height=254
nfcLoadingFailedIndicator: x=50.5, y=0, width=161, height=161
nfcLoadingFailedOuterRipple: x=0, y=0, width=161, height=161
nfcLoadingFailedInnerRipple: x=21, y=21, width=119, height=119
nfcLoadingFailedSymbol: x=48, y=48.5, width=64, height=64
nfcWebLoadingFailedCopy: font=PingFang SC Medium, size=22px, color=#FFFFFF
```
