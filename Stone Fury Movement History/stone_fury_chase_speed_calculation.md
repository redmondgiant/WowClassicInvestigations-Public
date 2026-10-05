# Stone Fury Chase-Speed Calculation

Based on:

- VMaNGOS history: https://github.com/redmondgiant/WowClassicInvestigations-Public/blob/main/Stone%20Fury%20Movement%20History/stone_fury_vmangos_speed_history_v2.md
- WoW-HC Death Appeal: https://wow-hc.com/forums/7266-fuser

## VMaNGOS movement values

| Date / state | `speed_walk` | `speed_run` |
|---|---:|---:|
| 2021-06-14 base world dump | 1.0 | 1.14286 |
| 2022-04-20 movement-speed correction | **1.55556** | **1.14286** |
| Current migration history | **1.55556** | **1.14286** |

VMaNGOS therefore gives Stone Fury an unusually high **walk** speed, while its **run/chase** speed remains the normal/common `1.14286` creature run ratio, corresponding to about **8 yd/s**.

## What the death video shows

At the point where Fuser uses **Blink + Swiftness Potion**, the Frostbite-induced root on Stone Fury has about **3 seconds remaining**.

That means Fuser effectively has a **3-second head start** before Stone Fury is able to begin running after him.

Relevant movement assumptions:

- Normal player run speed: **7 yd/s**
- Swiftness Potion: **+50% movement speed**, so Fuser runs at **10.5 yd/s**
- Swiftness Potion duration: **15 seconds**
- Blink displacement: approximately **20 yards**
- Frostbite/root remaining after Blink: approximately **3 seconds**

## Visual Closing Speed

If you take away nothing else from the video evidence, the mere closing speed alone shows something is very off.

At ~0:59–1:02 Stone Fury can visibly be seen rapidly gaining on Fuser while Fuser's +50% Swiftness Potion is still active. A normal ~8 yd/s mob cannot gain on a player moving at 10.5 yd/s at all; it must continuously lose ground. This occurs after Fuser had already Blinked away and Stone Fury remained rooted for approximately another 3 seconds, and Fuser had then run off 12 of the 15 sec of the swiftness pot. Fuser should have been very far away and ahead of the mob by the time the pot expires, not caught by it.

## Required chase speed

During the 15-second Swiftness duration, Fuser travels:

```text
10.5 yd/s × 15 s = 157.5 yd
```

Adding the approximately 20-yard Blink:

```text
157.5 yd + 20 yd = 177.5 yd
```

Because Stone Fury remains rooted for about 3 seconds after Blink, it has only about:

```text
15 s - 3 s = 12 s
```

to cover that separation before catching Fuser just before the potion expires.

Required average chase speed:

```text
177.5 yd / 12 s ≈ 14.79 yd/s
```

So Stone Fury would need to move at approximately:

```text
14.79 yd/s
```

to catch Fuser in the observed time.

For comparison:

- Fuser with Swiftness: **10.5 yd/s**
- VMaNGOS Stone Fury run speed: about **8.0 yd/s**
- Observed required chase speed: about **14.79 yd/s**

That required speed is approximately:

- **211% of normal player run speed** (`14.79 / 7.0`)
- **41% faster than Fuser while Swiftness is active** (`14.79 / 10.5`)
- **85% faster than VMaNGOS Stone Fury's ~8 yd/s run speed** (`14.79 / 8.0`)

## Short conclusion

With roughly 3 seconds of Frostbite root remaining when Blink and Swiftness are used, Stone Fury has only about 12 seconds of actual chase time before the 15-second potion expires. To overcome the Blink displacement plus Fuser's continued 150% movement speed in that interval, Stone Fury would need to average approximately **14.79 yd/s**.

That is far above the approximately **8 yd/s** run/chase speed represented by VMaNGOS for Stone Fury.
