# ReactionTimeTutorial

## Step 1

In order for **Reaction Time** to track the speed of a a player's reaction, we need to add variables to keep some data. We assign and set the variables to some starting values. The variables needed are: `start`, `end`, `false_start`, and `running`. Set the values of variables `start` and `end` to `0`, which means no time elapsed. Then set the value of the variables `false_start` and `running` to `false` to say we haven't started yet.

The tracking variables do the following:
- the reaction time experiment starts and ends at specific times based on the player's reaction.
- the code tracks when the experiment is running as well as when the player has a false start.

Add these variables to your code:

```blocks
basic.forever(function(){
let start = 0
let end = 0
let false_start = false
let running = false
running = false
false_start = false
end = 0
start = 0)}
```

### Step 2

We need to register event handlers that will execute whenever the user presses down on the **GND** pin with one hand, and presses pin **P0** or **P1** with the other hand, which completes the circuit. Our event handlers are two ``||input:on pin pressed||`` blocks, one for **P0** and the other for **P1**.

Add the  ``||input:on pin pressed||`` blocks to your code:

```blocks
let start = 0
let end = 0
let false_start = false
let running = false
input.onPinPressed(TouchPin.P0, () => {

})
input.onPinPressed(TouchPin.P1, () => {

})
running = false
false_start = false
end = 0
start = 0
```

## Step 3

We need a countdown timer that shows the seconds counting down when pin **P0** is pressed. Let's insert three ``||basic:show number||`` blocks to visually display the countdown

```blocks
let start = 0
let end = 0
let false_start = false
let running = false
input.onPinPressed(TouchPin.P0, () => {
    basic.showNumber(3)
    basic.showNumber(2)
    basic.showNumber(1)
    basic.clearScreen()
})
input.onPinPressed(TouchPin.P1, () => {

})
running = false
false_start = false
end = 0
start = 0
```
## Step 4

Now we'll set the variables `running` and `false_start` to `false` in the **P0** event.

Add the ``||variables:set to||`` blocks for `running` and `false_start` like like this

```blocks
let start = 0
let end = 0
let false_start = false
let running = false
input.onPinPressed(TouchPin.P0, () => {
    basic.showNumber(3)
    basic.showNumber(2)
    basic.showNumber(1)
    basic.clearScreen()
    running = false
    false_start = false
})
input.onPinPressed(TouchPin.P1, () => {

})
running = false
false_start = false
end = 0
start = 0
```

## Step 5

Let's add a random starting time after pin **p0** is pressed. Include the ``||math:random||`` block in a ``||basic:pause||`` at the bottom of the event block like this:

```blocks
let start = 0
let end = 0
let false_start = false
let running = false
input.onPinPressed(TouchPin.P0, () => {
    basic.showNumber(3)
    basic.showNumber(2)
    basic.showNumber(1)
    basic.clearScreen()
    running = false
    false_start = false
    basic.pause(1000 + randint(0, 2000))
})
input.onPinPressed(TouchPin.P1, () => {

})
running = false
false_start = false
end = 0
start = 0
```

## Step 6

The reaction time will begin if no false start is detected (pin **P0** pressed at the wrong time). When the reaction time starts, a LED is randomly plotted at some the x and y coordinate on the display. Add in the blocks contained in the ``||logic:if then||`` that show the reaction time:

```blocks
let start = 0
let end = 0
let false_start = false
let running = false
input.onPinPressed(TouchPin.P1, () => {

})
input.onPinPressed(TouchPin.P0, () => {
    basic.showNumber(3)
    basic.showNumber(2)
    basic.showNumber(1)
    basic.clearScreen()
    running = false
    false_start = false
    basic.pause(1000 + randint(0, 2000))
    if (!(false_start)) {
        start = input.runningTime()
        running = true
        led.stopAnimation()
        basic.clearScreen()
        led.plot(randint(0, 4), randint(0, 4))
    }
})
running = false
false_start = false
end = 0
start = 0
```

## Step 7

Add some code to detect when the player presses the **GND** foil with one hand and the **P1** pin with the other. This code detects the circuit connection and shuts off the timer. Also, add code to have the @boardname@ read the time in milliseconds from when the timer starts and the circuit is completed. This code also detects if there is a correct reaction or false start if pin **P1** is pressed.

Let's display one of two images if pin **P1** is pressed. The first image displays if the player correctly completes the circuit between **GND** and **P1**. This means that a correct reaction occurred to complete the circuit with pin **P1** pressed after the randomly generated LED appears.

The second image displays if the player completes a circuit between **GND** and **P1** but on a false start. A false start is detected if the player completes a circuit if pin **P1** is pressed before the LED randomly appears at its random x, y coordinate. Modify the code to include the actions for the pin **P1** event:

```blocks
let start = 0
let end = 0
let false_start = false
let running = false
input.onPinPressed(TouchPin.P1, () => {
    if (running) {
        running = false
        end = input.runningTime()
        basic.showLeds(`
            # # . . .
            # # . . .
            # # . . .
            # # . . .
            # # . . .
            `)
        basic.pause(1000)
        basic.showNumber(end - start)
    } else {
        false_start = true
        basic.showLeds(`
            . . . . .
            # . # . .
            . # . . .
            # . # . .
            . . . . .
            `)
    }
})
input.onPinPressed(TouchPin.P0, () => {
    basic.showNumber(3)
    basic.showNumber(2)
    basic.showNumber(1)
    basic.clearScreen()
    running = false
    false_start = false
    basic.pause(1000 + randint(0, 2000))
    if (!(false_start)) {
        start = input.runningTime()
        running = true
        led.stopAnimation()
        basic.clearScreen()
        led.plot(randint(0, 4), randint(0, 4))
    }
})
running = false
false_start = false
end = 0
start = 0
```

## Extension

After the students have finished their experiments. Have them play the game with a friend (using the **P2** pin) and have some contests to see who is the quickest on the draw.

You can find the code for this below:

```blocks
let start = 0
let end = 0
let false_start = false
let running = false
input.onPinPressed(TouchPin.P0, () => {
    basic.showNumber(3)
    basic.showNumber(2)
    basic.showNumber(1)
    basic.clearScreen()
    running = false
    false_start = false
    basic.pause(1000 + randint(0, 2000))
    if (!(false_start)) {
        start = input.runningTime()
        running = true
        led.stopAnimation()
        basic.clearScreen()
        led.plot(randint(0, 4), randint(0, 4))
    }
})
input.onPinPressed(TouchPin.P1, () => {
    if (running) {
        running = false
        end = input.runningTime()
        basic.showLeds(`
            # # . . .
            # # . . .
            # # . . .
            # # . . .
            # # . . .
            `)
        basic.pause(1000)
        basic.showNumber(end - start)
    } else {
        false_start = true
        basic.showLeds(`
            . . . . .
            # . # . .
            . # . . .
            # . # . .
            . . . . .
            `)
    }
})
input.onPinPressed(TouchPin.P2, () => {
    if (running) {
        running = false
        end = input.runningTime()
        basic.showLeds(`
            . . . # #
            . . . # #
            . . . # #
            . . . # #
            . . . # #
            `)
        basic.pause(1000)
        basic.showNumber(end - start)
    } else {
        false_start = true
        basic.showLeds(`
            . . . . .
            . . # . #
            . . . # .
            . . # . #
            . . . . .
            `)
    }
})
```
<script src="https://makecode.com/gh-pages-embed.js"></script><script>makeCodeRender("{{ site.makecode.home_url }}", "{{ site.github.owner_name }}/{{ site.github.repository_name }}");</script>
