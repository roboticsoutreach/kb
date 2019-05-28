---
title: Game Design Desiderata
author: Alistair Lynn
---

Written by Alistair Lynn, for SR2019.

The way I see it, there are 8 main requirements, or criteria to assess a game by:

1. Differentiation,
2. Game length,
3. Proof against first-order optimal strategies,
4. Reasonableness to prototype,
5. Presenting axes of exploration,
6. Fairness,
7. Practicality and robustness,
8. Spectacle.

To go into more detail:

1. Differentiation

    Scoring in games must always incentivize robot improvements.
    Specifically, making a robot more capable, intelligent and robust
    should produce a meaningful improvement in expected score. Games
    should also consistently rank better robots above worse robots.

    There's quite a bit to unpack here. The key thing is that all levels
    of ability, making the robot 'better' should meaningfully improve your
    score. For teams right at the very bottom, going from a robot which
    does nothing to one which does something should improve their score.
    For teams with middling ability, moving parts of their strategy from
    dead reckoning to something more intelligent should improve their
    score. For the teams right at the top, they should be able to make
    marginal gains and clever strategy tweaks which will improve their
    score. This always encourages teams to push forward.

    We want to avoid ties. A preponderance of ties is an indication that a
    game isn't differentiating well enough between some types of robots.
    This somewhat implies a wide range of ways to score points.

    Modelling points scored as geometric (which is common for sports), we
    can arrive at the following table for how many points robots should be
    scoring to achieve some level of ties:

    N. robots per game / % of games with ties / Mean score / Median score

    2 robots / 50% ties / 0.5 / 1
    2 robots / 20% ties / 2.0 / 2
    2 robots / 10% ties / 4.5 / 4
    2 robots / 5% ties / 9.5 / 7
    2 robots / 1% ties / 49.5 / 35
    4 robots / 50% ties / 4.1 / 4
    4 robots / 20% ties / 13.2 / 10
    4 robots / 10% ties / 28.2 / 20
    4 robots / 5% ties / 58.2 / 41
    4 robots / 1% ties / 298.2 / 208

    A corollary to this condition is that the game needs to have a low
    barrier to entry. In other words, from a cardboard box and some
    boards, we should be able to differentiate consistently between a team
    which assembles them in a basic fashion and a team which doesn't.


2. Game length

    All games must take exactly the same amount of time. This is actually
    a differentiating factor from sports (which often have rules around
    tie-breaking, or pausing) and from something like Robot Wars (where
    games can end early). This is needed to be able to sensibly schedule
    the competition, since we are packing such a huge amount of matches
    into such a short space of time, but also means that robots experience
    an even amount of wear and tear.

    Wear and tear is often a significant factor – robots are occasionally
    quite beaten up by the time we reach the finals.

    Implied by the game length criterion and the Differentiation criterion
    is that robots should never be incentivised to 'camp' or 'body-block'.
    Games should be designed so that it's never in a robot's interests to,
    for instance, get some tokens into a zone and then switch off and no
    longer move to block other robots from getting in.


3. Proof against first-order optimal strategies

    This is a bit of game design. A relevant blog post:

    http://www.realityrefracted.com/2011/03/first-order-optimal-strategies.html

    Essentially, there should be no one simple strategy which obviously
    dominates all other strategies. The game should be designed so that
    there are a range, preferably a very large range, of possible options.
    This improves spectacle, and makes the challenge more interesting, but
    it also avoids a situation where a small number of teams find this
    strategy and the competition devolves into separating the teams with
    that strategy and the teams without it.


4. Reasonableness to prototype

    Teams need to be able to prototype their robots in schools. This means
    they need to be able to construct an environment which is a reasonable
    approximation of the one they will be facing at the competition. Some
    behaviours are harder to approximate and some are easier, but they key
    point is not to need complexity or spending to be able to understand
    how robots will behave in the field.

    Game props and components need not be set up to be exactly replicated
    in schools, but should be easily approximated. Cardboard boxes and tin
    cans are very easy for schools to acquire, but if our setup involved a
    rope which robots needed to climb that would be difficult because it's
    hard to construct something stable enough to anchor that in a school.

    Active components in the arena are a problem, but aren't entirely
    ruled out as long as it's possible for schools to approximate them
    (such as by having a person holding something and taking some action
    at the right time).


5. Presenting axes of exploration

    Ideally games should present challenges in all the areas of robotics
    which teams can explore. Adding degrees of mechanical complexity where
    teams can explore building interesting actuators to gain an advantage
    are strongly encouraged, as are degrees of sensing complexity where
    teams can explore building interesting sensors, and tactical
    complexity where teams can explore building interesting software.

    This must not, of course, increase the barrier to entry, but ideally
    the game should involve challenges on all three axes. It is also
    better if there are challenges on these three axes at different skill
    levels: that is, low-performing teams can still gain some advantage by
    exploring options at these three levels as well as high-performing
    teams.


6. Fairness

    Games must be fair. They must also be perceived to be fair, which is
    subtly different but also important. Aspects of this are making sure
    that the arena is symmetric so that no team is advantaged by their
    starting position, and avoiding randomness if it can be seen to have
    given some teams an advantage and disadvantaging other teams.

    A good test of this: if a team described being "robbed" of an award by
    some aspect of the game, would you be able to keep a straight face? If
    one robot has easy access to some McGuffin which gives them lots of
    points and it's harder for the other three, one of the other teams
    could reasonably claim that they had a better robot and should have
    got an award but were "robbed" by their starting position. If,
    however, the team claimed to be "robbed" because they fell at a hurdle
    every other team had deliberately designed to be able to pass, we
    would be pretty scornful.


7. Practicality and robustness

    Given that we need to actually run this competition, making the setup
    practical and robust is very important. Realistically there is limited
    volunteer time ahead of the competition to build things; a workable
    game should have a plan for buying and building everything needed for
    the arena, and should also plan for how we can reasonably reset it
    between matches.

    It must also be robust, in the sense of minimising the chances of
    having to delay or cancel matches due to arena issues. Robustness can
    be simplifying components or building them to be physically stronger,
    it can also mean planning for having spares available, or using
    passive mechanisms instead of active ones.


8. Spectacle

    Student Robotics is a spectator sport. It should be very entertaining
    to watch matches. This has a few implications.

    The scoring system should be easy to understand and it should be easy
    to determine if someone is a long way out in front. Interaction
    between robots (non--destructive of course) should be strongly
    encouraged, because it's always fun to watch–and it also encourages
    intelligence. Robots should be constantly on the move and there should
    be plenty of opportunity for last-minute changes in who wins a match.


    These are the desiderata which I recommend we use to think about game
    ideas. Obviously it's not everything, but I think this is most of what
    we're looking for from a good game.

Reference: https://studentrobotics.org/trac/wiki/Game%20Assessment%20Criteria,
the original criteria used in SR years ago