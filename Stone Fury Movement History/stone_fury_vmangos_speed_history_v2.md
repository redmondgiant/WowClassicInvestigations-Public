# Stone Fury (Entry 2258) --- VMaNGOS Movement-Speed History


## TL;DR

| Date / state | `speed_walk` | `speed_run` |
|---|---:|---:|
| 2021-06-14 base world dump | 1.0 | 1.14286 |
| 2022-04-20 movement-speed correction | **1.55556** | 1.14286 |
| Current migration history | **1.55556** | 1.14286 |

**Only the walk value changed:** Stone Fury (entry 2258) went from `speed_walk=1.0` to `1.55556` on 2022-04-20, while its `speed_run` remained `1.14286`. No later migration changes either value.

## Purpose

This note summarizes the investigation of **Stone Fury**, rare elite
creature **entry 2258** in Alterac Mountains, focusing on VMaNGOS
`speed_walk` and `speed_run` values and their history.

The investigation was prompted by a WoW-HC death in which Stone Fury
appeared to chase at an exceptionally high speed. The goal here is
narrower: establish what VMaNGOS data says Stone Fury's walk/run speeds
are, how those values changed, and whether they changed again later.

## Sources and method

We used two VMaNGOS-related sources:

1.  **Historical VMaNGOS world database base dump** from the GitHub
    repository `brotalnia/database`: `world_full_14_june_2021.7z`. After
    extraction, the SQL dump contains the `creature_template` row for
    entry 2258 (`Stone Fury`).
2.  **Current `vmangos/core` Git repository**, specifically the
    timestamped SQL files under `sql/migrations/`.

The June 14, 2021 dump establishes the starting values. We then searched
the migration tree for the exact numeric token `2258` to identify later
changes affecting Stone Fury. We separately filtered occurrences
involving `speed_walk` or `speed_run` so unrelated uses of the number
2258 would not be mistaken for Stone Fury speed changes.

A key distinction is that some migration hits contain `2258` as a
**display ID** in `creature_display_info_addon`; those do **not** refer
to creature entry 2258 and therefore do not change Stone Fury's
`creature_template` movement speeds.

## June 14, 2021 base-dump values

The historical `creature_template` row for Stone Fury is:

``` text
(2258, ..., 'Stone Fury', ..., 2366, 91, 0, 1, 1.14286, 20, 5, ...)
```

From the `creature_template` column positions, the relevant values are:

-   `speed_walk = 1.0`
-   `speed_run = 1.14286`

Thus, in the June 14, 2021 base database, Stone Fury had the
ordinary/default VMaNGOS walk and run ratios.

## Intervening migrations before April 20, 2022

We searched the migrations after the June 2021 base dump and before the
target April 20, 2022 movement update for exact occurrences of `2258`.

No intervening migration changed Stone Fury's `speed_walk` or
`speed_run`. One February 24, 2022 `creature_template` update includes
entry 2258 but changes `school_immune_mask`, not movement speed. Other
occurrences are unrelated uses of the same number.

Therefore, immediately before the April 20, 2022 movement-speed
migration, Stone Fury was still:

-   `speed_walk = 1.0`
-   `speed_run = 1.14286`

## April 20, 2022 movement-speed update

Migration:

``` text
sql/migrations/20220420011159_world.sql
```

explicitly includes creature entry **2258** in both movement-speed
assignments:

``` sql
UPDATE `creature_template`
SET `speed_walk`=1.55556
WHERE `entry` IN (..., 2258, ...);
```

and:

``` sql
UPDATE `creature_template`
SET `speed_run`=1.14286
WHERE `entry` IN (..., 2258, ...);
```

The resulting Stone Fury values are therefore:

-   `speed_walk = 1.55556`
-   `speed_run = 1.14286`

The important point is that the migration **explicitly assigns both
values**. It increases Stone Fury's walk ratio from 1.0 to 1.55556 while
explicitly retaining/assigning the ordinary 1.14286 run ratio.

## Search for later changes

We searched the current VMaNGOS migration tree for exact `2258`
occurrences on lines involving `speed_walk` or `speed_run`.

The filtered search returned only the April 19--20, 2022 lines. The
April 19 lines operate on `creature_display_info_addon` using
`display_id`; their `2258` is a display ID and is not Stone Fury's
creature entry.

The only relevant `creature_template` movement assignments for **entry
2258** are therefore the April 20, 2022 assignments above. No subsequent
migration in the current repository changes Stone Fury's walk or run
speed.

## Movement-speed history summary

  ----------------------------------------------------------------------------------------
  VMaNGOS state/date                     `speed_walk`          `speed_run` What happened
  ------------------------------ -------------------- -------------------- ---------------
  June 14, 2021 base dump                     **1.0**          **1.14286** Historical
                                                                           starting state

  Immediately before Apr. 20,                 **1.0**          **1.14286** No intervening
  2022 migration                                                           speed change
                                                                           found

  Apr. 20, 2022                           **1.55556**          **1.14286** Walk explicitly
  (`20220420011159_world.sql`)                                             increased; run
                                                                           explicitly
                                                                           set/retained at
                                                                           1.14286

  After Apr. 20, 2022 through             **1.55556**          **1.14286** No later Stone
  current migration tree                                                   Fury walk/run
                                                                           change found
  ----------------------------------------------------------------------------------------

## Interpretation

VMaNGOS distinguishes Stone Fury's unusual **walk** speed from its
**run/chase** speed. The April 2022 movement correction deliberately
assigns Stone Fury a high `speed_walk` value while assigning
`speed_run = 1.14286`, the ordinary/common VMaNGOS creature run ratio.

Using the VMaNGOS/MaNGOS movement conventions discussed during the
investigation:

-   walk base: about **2.5 yd/s**
-   run base used by the ratio: about **7.0 yd/s**
-   `1.55556 × 2.5 ≈ 3.89 yd/s` walk
-   `1.14286 × 7.0 ≈ 8.0 yd/s` run

So the data represents Stone Fury as an unusually fast **walker**
(\~3.89 yd/s) but an ordinary **runner/chaser** (\~8 yd/s).

## Short conclusion

**Stone Fury (entry 2258) had `speed_walk=1.0` and `speed_run=1.14286`
in the June 14, 2021 VMaNGOS base dump. On April 20, 2022, VMaNGOS
explicitly changed its walk speed to `1.55556` while explicitly
setting/retaining its run speed at `1.14286`. No later migration changes
either value. Thus the VMaNGOS historical record consistently supports
special fast walking for Stone Fury, not a special high combat/chase run
speed.**
