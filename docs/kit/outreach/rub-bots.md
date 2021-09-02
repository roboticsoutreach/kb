---
title: Rub-bots
---

The Rub-bots are a set of physical robots constructed in July/August
2021 to facilitate [Smallpeice 2021](/events/history/2021). For that competition, they were called the 'Forklift-bots' to keep with the theme of the game. After that, they became the 'rub-bots' - named to reflect the fact that they were designed to perfectly fit inside the 35L Really Useful Boxes ('RUBs')

The design was intended to be robust so the robots would last long enough to be used for many future events, as demo-bots and to be offered to participants for outreach events.

The bots have:

- 2 wheel differential drive
- a servo-driven linear gripper
- a forward-facing ultrasound distance sensor

## Servo mechanism

The gripper is connected to its servo via 'lightweight inextensible strings' (at least in theory). They're actually lengths of Nylon fishing line, which does stretch quite a bit. The complicated bit is connecting the grippers to the servo such that both grippers are pulled open and pulled closed symmetrically, as below:

### To string up a rub-bot

- String 1:
    1. Tie the string to gripper 1 securely - e.g. using a overhand
    stopper knot through a pair of drilled holes in the gripper. You can double up the string to reduce the stretch of the fishing line
    2. Hook the string around the nearest idler
    3. Position the gripper in the middle of its range (halfway between open and closed) and the servo in the middle of its range
    4. Tie the other end off on the servo. You can weave between the servo horn and the pulley to help secure this end
    ![Diagram of String 1](/img/kit/rub-bots/rub-bot_string_1.png)  
    This string pulls gripper 1 open
- String 2:
    1. Tie the string to gripper 1 securely, heading in the other direction to `String 1`. If `String 1` was *opening* gripper 1, `String 2` will be *closing* it
    2. Hook the string around the other idler (not the one `String 1` used). The string may pass through gripper 2 without interacting with it
    3. Check gripper 1 and the servo are in their middle positions, and pull `String 2` tight. `String 1` and `String 2` will stretch a bit
    4. Tie the end off on the servo, as before
    ![Diagram of String 2](/img/kit/rub-bots/rub-bot_string_2.png)  
    This string pulls gripper 1 closed
- String 3:
    1. Tie onto gripper 2
    2. Hook round the idler nearest
    3. Pass through **both** grippers without tying to either
    4. Hook round the other idler
    5. Tie off on the servo
    ![Diagram of String 3](/img/kit/rub-bots/rub-bot_string_3.png)  
    This string pulls gripper 2 open. By going around both idlers like this, *gripper 2 opening* and *gripper 1 opening* happen when the servo goes *clockwise*. Otherwise, gripper 2 *closes* when gripper 1 *opens*, which is not very useful.
- String 4:
    1. Tie onto gripper 2, heading the other way
    2. Hook round the near idler
    3. Go through both grippers
    4. Hook round other idler
    5. Tension the strings and tie off on servo
    ![Diagram of String 4](/img/kit/rub-bots/rub-bot_string_4.png)  
    This string pulls gripper 2 closed, synchronised with gripper 1 closing

The servo is powered from the secondary '5V' output of the power board. The power board is rated to supply enough current for one servo, so a separate servo board isn't needed.
