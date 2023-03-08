# Trust mechanism consists of:
- Truth (competence)
- Eagerness (willingness
- (ability > does the robot already know?)
- Potentially: confidence in these


| Action                                                                             | Influence on truth | Influence on eagerness |
|------------------------------------------------------------------------------------|--------------------|------------------------|
| search                                                                             | /                  | +                      |
| found                                                                              | /                  | +                      |
| collect                                                                            | /                  | +                      |
| Remove: continue (line 321)                                                        | +                  | -                      |
| Remove: remove (line 328)                                                          | /                  | +                      |
| Rescued                                                                            | +                  | +                      |
| (line 222) all areas searched, task not finished (not everyone is rescued)         | - -                | - -                    |
| Time out: reacting to message (multiple instance, s.a. Line 525)                   | /                  | -                      |
| Time out: showing up   (long enough time out that it is very doable to be on time) | -                  | -                      |-
| Line 504: if no victim is in area that human pointed to                            | -                  | /                      |
| Line 473: if victim is in area that human pointed to                               | +                  | +                      |

**We would like to add a time out to the waiting that the bot will do for the human**. 
Time out based on:
- Ticks? There is a duration_in_ticks in line 191, so the method already makes use of it.

Actions that the bot will do on its own/have a low time out for if the trust is low:
- Remove small rocks on its own
- Remove tree on its own
- Carry mildly injured victims on its own

 maybe play with how many ticks the bot waits depending on how good/bad the trust value is.
the bot will do this if the human does not react to its messages or does not show up after the time out

For all other actions, have it send another message when:
- Ticks have run out
- When trust is low, have a lower amount of ticks to wait
- When trust is high, have a higher amount of ticks to wait.

**Trust values between [-1, 1]**

| Action                                                | Possibly change: no trust                       | Possibly change: trust                |
|-------------------------------------------------------|-------------------------------------------------|---------------------------------------|
| Remove rocks (small)                                  | Do it yourself (t<=0 or e<= 0)                  | Do it together (t>0 and e>0)          |
| Remove stone (big)                                    | New message                                     | Wait                                  |
| Remove tree                                           | No response? Do it yourself (e<= 0)             | No response? Message again (e>0)      |
| Decide to save mildly injured victim                  | No response? Decide it yourself (do it) (e<= 0) | No response? Message again (e>0)      |
| Carry mildly injured victim                           | Does not show up? Do it yourself (e<= 0)        | Does not show up? Message again (e>0) |
| Add area to searched list (human said it searched it) | Do not add area to searched list (t<=-0.5)      | Add area to searched list (t>-0.5)    |

Especially actions that the agent can do by its own, we want to change the codes so that it allows for it. For example, when the agent knows the human is lazy, it is more likely to remove the rock on its own than to wait or wait less long.

It seems collectedVictims is a hard truth in the program, only victims which were rescued are put in there.
It can be used to check if the human has been lying or not.

Line 473 > add else statement that if in the searched area that the human pointed out there is no victim, they were lying. The trust should decrease.

When coding the values like 0.5, make variables at the top of the code, so that it can be changed easily when fine tuning these parameters.
(optional: mae two lists of searched rooms, one from the human and one from the bot, that way, you only need to search the human rooms if victims still remain)

Another thing the human can lie about is its location. The robot bases the distance between them on the last communicated location of the human. It is however only used in the code to communicate to the human whether they are close or far away from the robot. The human can know this themselves if they know where the robot is and where they are. We decided not to change anything regarding this.

To do:
- Make concrete bins based on the above
- Make list of where in the code we want to change things






