# Luggage Lock

Visit *Garland Candlesticks* in the *Squarewheel Yard* on the *Island of Misfit Toys* to begin the challenge.

## Challenge Prompt

![Figure 1: Luggage Lock Decoder Challenge Prompt](/img/luggage-prompt.png)

We are challenged to open a luggage bag with a rotary combination lock by decoding the 1-4 wheel combination. We have the option of choosing how many wheels the lock has, but to complete the challenge we must decode a 4-wheel lock. 

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

To test our attack methodology, let us return to our one wheel combination lock. 

We will determine the most likely candidate for a key digit by applying moderate pressure (3 clicks), rotating the wheel, tallying how many times we encounter resistance on each digit, and stopping once we have reached a digit that has applied resistance to our wheel 5 times.

![Figure 7: Determining the Key Digit on a One Wheel Combination Lock](/gif/luggage-test-dialing.gif)

The digit *9* was the first to apply resistance to our wheel 5 times during the attack. This is our *most likely* candidate for the key digit, so let us apply maximum pressure to the keyhole to test whether this is the legitimate key digit.

![Figure 8: Unlocking a One Wheel Rotary Combination Lock](/gif/luggage-test-success.gif)

## Decoding a Four Wheel Rotary Combination Lock

With our attack methodology matured, let us now attempt decoding a combination lock with 4 wheels.

![Figure 8: Starting a Four Wheel Game](/img/luggage-challenge-2.png)

