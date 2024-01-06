# Luggage Lock

Visit *Garland Candlesticks* in the *Squarewheel Yard* on the *Island of Misfit Toys* to begin the challenge.

## Challenge Prompt

![Figure 1: Luggage Lock Decoder Challenge Prompt](/img/luggage-prompt.png)

We are challenged to open a luggage bag with a rotary combination lock[^1] by decoding the 1-4 wheel combination. We have the option of choosing how many wheels the lock has, but to complete the challenge we must decode a 4-wheel lock. 

## Test Round

To understand the mechanics of the game, let's choose the *One wheel* option and try a test round.

![Figure 2: Starting a One Wheel Game](/img/luggage-challenge-1.png)

There is a *?* button in the top-right corner, let's click on it.

![Figure 3: Help Button](/img/luggage-help.png)

We can apply cascading degrees of pressure to the keyhole by clicking on it. There are 5 pressure levels, starting at 0 clicks (no pressure at all) and ending at 5 clicks (high pressure). If the keyhole is clicked a 6th time (maximum pressure), the pressure resets to level 0.

![Figure 4: Applying Pressure to the Keyhole](/gif/luggage-keyhole.gif)

We can rotate the wheels by either clicking on them manually or by pressing their respective key bindings. In the case of a one wheel lock, the key binding to increase the first wheel is <kbd>R</kbd>, and the key binding for the second wheel is <kbd>F</kbd>.

![Figure 5: Rotating the Wheels on Wheel 1](/gif/luggage-dialing.gif)

If we apply pressure **and** dial a wheel, eventually the wheel will apply resistance.

![Figure 6: Rotating the Wheels While Applying Keyhole Pressure](/gif/luggage-resistance.gif)

## Our Attack Methodology

The following YouTube video is especially helpful in maturing our attack methodology:

[YouTube: KringleCon Lock Talk by Chirs Elgee](https://www.youtube.com/watch?v=ycM1hBSEyog)

In Elgee's demonstration, when he applies pressure to the keyhole button and spins one of the wheels, eventually that wheel will become momentarily "stuck" on a single digit. The more "stuck" a digit becomes, the more likely that it is one of the key digits in the combination. Elgee starts at wheel 1, and proceeds sequentially until the lock is opened.

Our attack methodology will look like this:
1. Apply moderate pressure to the keyhole.
2. Turn wheel *N* continuously, where *N* is the index of the wheels in ascending order, starting at wheel *1*.
3. Once we have encountered pressure on a given digit a significant number of times (let's say *5* times), leave the wheel turned to that digit.
4. Repeat steps 2-3 for the next wheels.
5. Apply maximum pressure to the keyhole once we have determined the most likely key digit candidates for all wheels.
6. If our estimate was incorrect, repeat the steps starting at step 1 until successful.

To test our attack methodology, let us return to our one wheel combination lock. 

We will determine the most likely candidate for a key digit by applying moderate pressure (3 clicks), rotating the wheel, tallying how many times we encounter resistance on each digit, and stopping once we have reached a digit that has applied resistance to our wheel 5 times.

![Figure 7: Determining the Key Digit on a One Wheel Combination Lock](/gif/luggage-test-dialing.gif)

The digit *9* was the first to apply resistance to our wheel 5 times during the attack. This is our *most likely* candidate for the key digit, so let us apply maximum pressure to the keyhole to test whether this is the legitimate key digit.

![Figure 8: Unlocking a One Wheel Rotary Combination Lock](/gif/luggage-test-success.gif)

We have successfully decoded the combination of a one wheel rotary combination lock without prior knowledge of the code.

## Decoding a Four Wheel Rotary Combination Lock

With our attack methodology matured, let us now attempt decoding a combination lock with 4 wheels.

![Figure 8: Starting a Four Wheel Game](/img/luggage-challenge-2.png)

Our first step is to determine the most likely candidate for our first wheel key digit. Apply moderate pressure (3 clicks), and begin turning the wheel, taking note of how many times each digit applies resistance while doing so.

![Figure 9: Determining the First Key Digit on a Four Wheel Lock](/gif/luggage-game-lock1.gif)

We have determined our most likely candidate for wheel one: *5*

Keeping the first wheel in the same position at digit *5*, continue applying moderate pressure and turning the wheel to determine the next key digit.

![Figure 10: Determining the Second Key Digit on a Four Wheel Lock](/gif/luggage-game-lock2.gif)

We have determined our most likely candidate for wheel two: *7*

Keep wheels one and two at their respective positions, and determine the most likely key digit on wheel three.

![Figure 11: Determining the Third Key Digit on a Four Wheel Lock](/gif/luggage-game-lock3.gif)

We have determined our most likely candidate for wheel three: *8*

The last key digit can now be determined using the same method as before.

![Figure 12: Determining the Fourth Key Digit on a Four Wheel Lock](/gif/luggage-game-lock4.gif)

We have determined our most likely candidate for wheel four: *6*

The most likely combination for the luggage lock is therefore *6*-*8*-*7*-*5*. Apply maximum pressure (6 clicks) to the keyhole with this code set on the lock to determine if our estimate was correct.

![Figure 13: Unlocking a Four Wheel Rotary Combination Lock](/gif/luggage-game-success.gif)

We have successfully decoded the combination of a four wheel rotary combination lock without prior knowledge of the code.

[^1]: https://en.wikipedia.org/wiki/Luggage_lock
