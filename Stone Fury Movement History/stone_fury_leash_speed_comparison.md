# Stone Fury — 12-Second Leash / Chase Comparison

Screenshot at [leash countdown start](https://github.com/redmondgiant/WowClassicInvestigations-Public/blob/main/Stone%20Fury%20Movement%20History/stone_fury_leash_countdown.JPG) (as Frostbite root proc expires)

Screenshot at [leash countdown end](https://github.com/redmondgiant/WowClassicInvestigations-Public/blob/main/Stone%20Fury%20Movement%20History/stone_fury_leash_countdown_after_12sec.JPG) (assuming ~12sec for a level 37 mob with no leash resetting or extending conditions occurring)

## TL;DR

At the moment Stone Fury is free of movement-impairing effects, **Fuser has 12 seconds remaining on Swiftness**. For a level-37 Stone Fury, this also begins/resumes the **12-second leash interval**.

By that point Fuser already has an estimated **51.5-yard head start**:

```text
20 yd Blink + (3 sec rooted × 10.5 yd/s Swiftness) = 51.5 yd
```

From that common starting point:

| Stone Fury scenario | Mob speed | Relative to Fuser at 10.5 yd/s | Position at 12-sec leash boundary |
|---|---:|---:|---:|
| **Actual chase shown in video** | **~14.79 yd/s (211%)** | Gains ~4.29 yd/s | **Catches Fuser (~0 yd behind)** |
| **130% run-speed estimate** | **9.1 yd/s** | Loses 1.4 yd/s | **~68.3 yd behind** |
| **VMaNGOS Stone Fury** | **~8.0 yd/s** | Loses 2.5 yd/s | **~81.5 yd behind** |

## Why this matters

The end of Fuser's Swiftness and the end of Stone Fury's 12-second leash interval occur at approximately the same time.

At **130% movement speed**, Stone Fury is still slower than Fuser's 150% Swiftness:

```text
10.5 - 9.1 = 1.4 yd/s slower
51.5 + (1.4 × 12) = 68.3 yd behind
```

At the **VMaNGOS run speed** of about 8 yd/s:

```text
10.5 - 8.0 = 2.5 yd/s slower
51.5 + (2.5 × 12) = 81.5 yd behind
```

But in the actual video Stone Fury instead erases the entire head start and reaches Fuser at approximately the leash boundary. To do that:

```text
Fuser travels during Swiftness: 10.5 × 15 = 157.5 yd
Add Blink:                         +20.0 yd
Total Stone Fury must cover:      177.5 yd

Stone Fury chase time after root: 12 sec

177.5 / 12 ≈ 14.79 yd/s
```

That is approximately **211% of normal 7 yd/s player run speed**, equivalent to roughly a `speed_run` ratio of **2.11** on the same 7 yd/s base.

## Bottom line

**At any near-normal speed, Stone Fury should reach the 12-second leash boundary tens of yards behind Fuser and disengage—not reach melee range.**

- At **130% speed:** ~**68 yd behind**
- At **VMaNGOS speed:** ~**82 yd behind**
- In the **actual video:** **catches Fuser**

The anomalously high chase speed is what allows Stone Fury to reach Fuser at approximately the same moment the leash interval would otherwise expire.
