# Faster Lock

```
Hey there! I'm Bow Ninecandle, and I've got a bit of a... 'pressing' situation.

You see, I need to get into the lavatory, but here's the twist: it's secured with a combination padlock.

Talk about bad timing, right? I could really use your help to figure this out before things get... well, urgent.

I'm sure there are some clever tricks and tips floating around the web that can help us crack this code without too much of a flush... I mean fuss.

Remember, we're aiming for quick and easy solutions here - nothing too complex.

Once we've gathered a few possible combinations, let's team up and try them out.

I'm crossing my legs - I mean fingers - hoping we can unlock this door soon.

After all, everyone knows that the key to holiday happiness is an accessible lavatory!

Let's dive into this challenge and hopefully, we won't have to 'hold it' for too long! Ready to help me out?
```

Start the lock challenge.

![Faster Lock Figure 1](/img/faster-lock-1.png)

The first thing to note is that when we move the face of the lock counter-clockwise (the <kbd>-></kbd> arrow key), the *Reset Status* icon turns red. We can deduce that this icon indicates whether we have selected the wrong number for the combination.

![Figure 2: *Reset Status* Button Turns Red](/gif/faster-reset-red.gif)

If we want to reset the lock, all we have to do is double-click the dial.

![Figure 3: Resetting the Dial](/gif/reset-dial.gif)

When we pull on the lever, the *Tension Status* button changes from green to red respective to how far we pull the shackle.

![Figure 4: *Tension Status* Button Turning Red](/gif/faster-tension.gif)

If we attempt to move the face of the lock right or left while the shackle is partially pulled (tension status is dark green to maroon), we can still move the face of the lock.

![Figure 5: Light-Mediume Tension Effects](/gif/mid-tension.gif)

However, if we attempt to move the face of the lock while the shackle is completely taught (color is back to red), then we are only able to move the face of the lock a little bit.

![Figure 6: Complete Tension Effects](/gif/complete-tension.gif)

Our first objective is to find the *First Locked Position* parameter value. This is accomplished by pulling the shackle as hard as we can and iterating over the values 0 - 11 until we are locked into a small groove. For all grooves, take note of which digits the notch is between. If the notch is between two whole digits (e.g. 5 and 6), then the groove is not indicative of one of our locked positions. However, if the notch is between two half digits (e.g. 5.5 and 6.5), then that groove is one of our locked positions.

![Figure 7: Determining our First Locked Position](/gif/first-position.gif)

We identified the first locked position as *3*, since the notch was in a groove between *2.5* and *3.5*. Our next step is to identify the second groove. 

![Figure 8: Determining our Second Locked Position](/gif/second-position.gif)

Our second lock position is *8*. The next objective is to identify the *Resistant Location*. 

![Figure 9: Determining our Resistant Position](/gif/resistant-position.gif)

The resistant position is 16, we can now plug these values into the calculator, which should provide us the two candidates for the actual third digit position.

![Figure 10: Lock Calculator Third Digit Candidates Identified](/img/lock-calculator-1.png)

To determine which of the two third digit position candidates are the legitimate option, we have to set the dial to 0, and manually compare the "give" of both candidates when we pull the shackle as hard as possible. The candidate with the most "give" is the likely legitimate option.

![Figure 11: Comparing the "Give" of Both Third Position Candidates](/gif/third-position-candidates.gif)

We are going to assume that position *33* is the likelier candidate because it was visibly looser than position *13*.

Next, we must determine the legitimate second position. We observe that when we turn the face of the lock clockwise to position *21*, make one full 360 degree rotation in the counter-clockwise direction, stop at a non-legitimate second position possibility (like *22*, which is not a second digit candidate), the *Reset Status* icon turns red, which indicates that the second position digit was incorrect.

![Figure 12: Trial and Error Second Position Candidates](/gif/second-position-candidates.gif)

After multiple trial-and-error attempts, we observe that when we turn the face of the lock clockwise to position *19*, make one full 360 degree rotation in the counter-clockwise direction, stop at **, and begin moving the face of the lock in the clockwise direction, the *Reset Status* icon no longer turns red, indicating that we have found the correct 2nd digit position.

![Figure 13: Second Position Confirmed](/gif/second-position-confirmed.gif)

We have our combination: 21 - 31 - 33

![Figure 14: Lock Picked](/gif/lock-picked.gif)
