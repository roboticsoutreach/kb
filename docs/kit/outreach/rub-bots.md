---
title: Rub-bots
---

The Rub-bots are a set of physical robots constructed in July/August
2021 to facilitate [Smallpeice2021] (TODO link). For that competition, they were called the 'Forklift-bots' to keep with the theme of the game. After that, they became the 'rub-bots' - named to reflect the fact that they were designed to perfectly fit inside the 35L Really Useful Boxes ('RUBs')

The design was intended to be robust so the robots would last long enough to be used for many future events, as demo-bots and to be offered to participants for outreach events.

The bots have:
 - 2 wheel differential drive
 - a servo-driven linear gripper
 - a forward-facing ultrasound distance sensor




## Servo mechanism:



The gripper is connected to its servo via 'lightweight inextensible strings' (at least in theory). They're actually lengths of Nylon fishing line, which does stretch quite a bit. The complicated bit is connecting the grippers to the servo such that both grippers are pulled open and pulled closed symmetrically, as below:

### To string up a rub-bot:
 - String 1:
    - Tie the string to gripper 1 securely - e.g. using a overhand
    stopper knot through a pair of drilled holes in the gripper. You can double up the string to reduce the stretch of the fishing line
    - Hook the string around the nearest idler
    - Position the gripper in the middle of its range (halfway between open and closed) and the servo in the middle of its range
    - Tie the other end off on the servo. You can weave between the servo horn and the pulley to help secure this end
    TODO image
 - String 2:
    - Tie the string to gripper 1 securely, heading in the other direction to `String 1`. If `String 1` was *opening* gripper 1, `String 2` will be *closing* it
    - Hook the string around the other idler (not the one `String 1` used). The string may pass through gripper 2 without interacting with it
    - Check gripper 1 and the servo are in their middle positions, and pull `String 2` tight. `String 1` and `String 2` will stretch a bit
    - Tie the end off on the servo, as before
    TODO image
 - String 3:
    - Tie onto gripper 2
    - Hook round the idler nearest
    - Pass through **both** grippers without tying to either
    - Hook round the other idler
    - Tie off on the servo
    

The servo is powered from the secondary '5V' output of the power board. The power board is rated to supply enough current for one servo, so a separate servo board isn't needed.