# Na'an

This challenge is located on *Film Noir Island* in *Chiaroscuro City*. In this challenge, we will be playing against *Shifty McShuffles*.

## The Rules of the Game

Once we click on the terminal, we are greeted with a screen explaining the rules of the game.

![Figure 1: Shifty's Card Shuffle Prompt](/img/shuffle-prompt.png)

Here are the takeaways:
* We pick five cards numbering from 0-9, and can't pick two of the same number.
* At the end of each round, our cards are compared to the opponent's hand.
* Whichever player picks the lowest and highest number wins a point for each card.
* If both players picked the same lowest/highest number, then nobody wins a point.
* The first player to win 10 points wins.

At face value, this game should be fairly straightforward. However, it sounds like Shifty is not afraid to "cheat". It is not immediately clear how the game is rigged, so let's run a test game. 

## Test Round

Start a game with Shifty.

![Figure 2: Starting a Game with Shifty](/img/nan-start.png)

During the first round, I picked a simple hand: `1`, `2`, `3`, `4`, `5`

![Figure 3: Losing Hand](/img/nan-lose.png)

Because Shifty chose the numbers 0 and 9, he won both points this round.

At the next round, I chose a hand that will be guaranteed to contain the lowest and highest number: `0`, `1`, `2`, `8`, `9`

!![Figure 4: A Tied Hand](/img/nan-tie.png)

Shifty also picked the lowest and highest numbers. If we continue to play this hand in perpetuity, Shifty will also choose the same numbers and the hand will always be tied. It now becomes clear how Shifty is cheating: he is looking at our cards. If we choose a 0 or a 9, he will also choose those numbers and the round will be tied. The game can only realistically end with us choosing losing hands and Shifty picking winning ones.

![Figure 5: Game Lost](/img/nan-game-lost.png)

## Beating Shifty

To better understand how we intend to beat Shifty, we should ask ChatGPT to educate us on Python NaN injection attacks[^1].

![Figure 6: ChatGPT](/img/nan-chatgpt.png)

NaN is a floating-point value in Python typically used to represent values like infinite or infinitesimally-close-to-zero. If passed to a Python application that does not sufficiently sanitize inputs or use NaN-aware functions like `math.isnan(x)`[^2], then it can lead to application logic flaws and unexpected results.

Choose a hand with a `nan` string as the value of one of the hands: `0`, `1`, `nan`, `8`, `9`

![Figure 6: Winning a Hand](/img/nan-win.png)

We have found a way to win a hand. Continue with this hand until the game is won.

![Figure 7: Winning the Game](/img/nan-game-won.png)

[^1]: https://www.tenable.com/blog/python-nan-injection
[^2]: https://docs.python.org/3/library/math.html#math.isnan
