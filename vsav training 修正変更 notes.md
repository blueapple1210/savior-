# VSAV Training Mode - Project Notes

## Project Overview

Vampire Savior (VSAV) Lua Training Mode project.

Primary goals:

* Improve training functionality for AG (Advancing Guard)
* Improve Guard Cancel training
* Improve dummy automation
* Improve input analysis tools
* Add advanced matchup-specific training scenarios

---

# Important Files

## controller.lua

Responsibilities:

* Dummy input generation
* Dash actions
* Dash cancel actions
* Character-specific timing tables
* Counter attack execution

Recent changes:

* Dash attack timing table added
* Dash cancel logic modified
* Sasquatch-specific short dash experiments

---

## guardCancel.lua

Responsibilities:

* Guard Cancel trigger logic
* Reversal timing
* Counter attack scheduling

Notes:

* frameEndedGuarding bug fixed
* Guard Cancel crash resolved

---

## inputHistory.lua

Responsibilities:

* Input history display
* Input history storage
* Idle display logic

Known issue:

* P1 history displays IDLE
* Dummy-side history does not currently display neutral frames

Future work:

* Dummy-side neutral frame display
* Frame-by-frame dummy sequence debugger

---

## dummyState.lua

Responsibilities:

* Menu state access
* Counter attack settings
* Guard action selection

Recent changes:

* Added forward throw option
* Added back throw option

---

## menu.lua

Responsibilities:

* Training mode menu definitions
* Option registration

Recent changes:

* Added forward throw
* Added back throw

---

# Confirmed Findings

## Pushblock Timing

Community discussion indicates:

* PB acceptance begins before visual blockspark appears
* Blockspark is drawn after game state has already advanced
* PB counter is considered accurate
* Visual PB indicators may be off by 1–2 frames

Implication:

Internal state should be trusted over graphics.

---

## True Reversal

Testing:

Dummy Morrigan reversal DP

Results:

True Reversal OFF:

* 50/50 successful

True Reversal ON:

* 31/50 successful

Conclusion:

Behavior appears consistent with CPS2 frameskip mechanics.

No changes currently planned.

---

## Sasquatch Short Dash Investigation

Manual macro testing:

Pattern:
6 N 6 N N N N 4

Results:

* Short dash can occur
* Success rate inconsistent with external macro hardware

Pattern:
6 N 6 N N N N 4+P

Results:

* No confirmed short dash attacks
* Mostly long dash attacks

Current hypothesis:

Attack button should occur after cancel direction rather than on the same frame.

Further Lua-side testing required.

---

# Future Features

## AG Trainer Expansion

Goals:

* Display AG start timing
* Display AG frame offset
* AG-specific input history
* Show which inputs counted
* Show simultaneous presses
* Show failed inputs

Reference:
Tech-hit input analysis concepts discussed by MBD and dom.

---

## Post-AG Action System

Examples:

Dummy AG
→ Throw

Dummy AG
→ Jab

Dummy AG
→ Dash

Purpose:

Practice AG counterplay situations.

---

## AG Response Chain System

Examples:

Dummy attacks
→ Player AG
→ Dummy performs follow-up action

Purpose:

Practice common Savior AG mind games.

---

## Dummy Input Debugger

Desired display:

F1 →
F2 N
F3 →
F4 N
F5 N
F6 N
F7 ←
F8 P

Purpose:

Debug dash timing and AG/PB inputs.

High priority.

---

## Save State Expansion

Current:

* 1 save slot

Desired:

* Multiple save slots

Possible UI:
Slot A
Slot B
Slot C
Slot D

---

## Replay Trigger System

Examples:

Player dash
→ Dummy action

Player jump
→ Dummy action

Player attack
→ Dummy action

Purpose:

Recreate matchup situations.

---

# Open Questions

* Exact short dash timing for all applicable characters
* Bishamon dash behavior
* DF Zabel dash behavior
* Dummy history rendering location
* Whether AG trainer should reuse PB input infrastructure

---

Gallon

Forward Dash Cancel

13 = Long
14 = Short

Current working value:
14

---
Gallon Forward Dash Cancel

Last Updated: 2026-06-25

Current Value:

cancel_frame = 14
button_on_cancel_frame = false

Testing:

10 = Long Dash
12 = Long Dash
13 = Long Dash
14 = Short Dash
15 = Short Dash
20 = Short Dash

Conclusion:

Stable threshold appears to be:

cancel_frame = 14

Status:
Adopted

Felicia Forward Dash Cancel

Last Updated: 2026-06-25

Current Value:

cancel_frame = 14
button_on_cancel_frame = false

Testing:

11 = Long Dash
12 = Long Dash
13 = Short Dash (unstable)
14 = Stable Short Dash

Additional Notes:

Short Dash j.MK confirmed
13 occasionally produced Long Dash
14 has not reproduced the issue

Conclusion:

Theoretical minimum:

13

Practical value:

14

Status:
Adopted

Dummy Sequence Debugger

Last Updated: 2026-06-25

Modified Files:

controller.lua
hud.lua

Purpose:
Display generated pending_input_sequence for verification.

Status:
Working
-----
### 2023-02-21 Discord (nbee)

Character Specific Reversal is a known issue.

> "Feature doesnt work, we never figured out how to not make it crash."

> "Well the feature does work, it just crashes the game lol."

Conclusion:
- Crashes are a known upstream bug.
- Not introduced by this fork.
- Avoid relying on Character Specific Reversal for new features.

-----

Last Updated:
Current development cycle
