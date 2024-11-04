# TypeRacer Game

## Task Description
In this project, I created a game similar to TypeRacer, where users can test their typing speed. The project utilizes an Arduino UNO to control an RGB LED that indicates the game state and buttons to manage the game round and difficulty.

## Requirements
- The game will start with a 3-second countdown.
- The RGB LED will change color based on the accuracy of the entered text.
- The game difficulty can be set using a button, which will alter the speed at which words appear.
- At the end of each round, the score will be displayed in the terminal.

## Components Used
- **Arduino UNO** (ATmega328P microcontroller)
- **1x RGB LED** (to indicate text accuracy)
- **2x Buttons** (for start/stop round and for selecting difficulty)
- **5x Resistors** (3x 220/330 ohm, 2x 1000 ohm)
- **Breadboard**
- **Jumper wires**

## Hardware Setup

1. **RGB LED Pins**
   - Red: Connected to `LED_PIN_RED` (Pin 6 on Arduino)
   - Green: Connected to `LED_PIN_GREEN` (Pin 5 on Arduino)
   - Blue: Connected to `LED_PIN_BLUE` (Pin 4 on Arduino)

2. **Buttons**
   - Start Button: Connected to `BUTTON_PIN_START` (Pin 2 on Arduino) - starts and stops the game round.
   - Mode Button: Connected to `BUTTON_PIN_MODE` (Pin 3 on Arduino) - toggles the difficulty level.

## Wiring Diagram
![Wiring Diagram](./imagini/schema_circuit_trg.PNG)

## Physical Setup
![Physical Setup 1](./imagini/poza1_trg.jpeg)
![Physical Setup 2](./imagini/poza2_trg.jpeg)
![Physical Setup 3](./imagini/poza3_trg.jpeg)
![Physical Setup 4](./imagini/poza4_trg.jpeg)
![Physical Setup 4](./imagini/poza5_trg.jpeg)

## Video Demonstration of the Physical Setup
[Video Demonstration](https://youtube.com/shorts/4CTRUkjRXb0?feature=share)

## Code Functions Overview

[This is the code.](/code)


### `void setColor(int red, int green, int blue)`

Sets the RGB LED color based on the values for red, green, and blue brightness levels (parameters `red`, `green`, `blue` range from 0 to 255).

**Usage**: Used throughout the game to indicate different states, such as game start, correct input, and incorrect input.

### `String pickRandomWord()`

Picks a random word from the `sneakerWords` list, used to generate the words the player needs to type.

**Usage**: Called at the beginning of each new word to provide a random word for the player.

### `void initiateRound()`

Initializes a new game round, including:
   - Setting game state variables to begin the game (`gameActive` set to `true`)
   - Displaying a countdown on the Serial Monitor and flashing the LED
   - Setting a new word and starting its countdown timer

**Usage**: Triggered when the game starts (start button is pressed).

### `void concludeRound()`

Stops the game, displaying the final score on the Serial Monitor and showing the number of correctly typed words.

**Usage**: Triggered when the round ends, either by time expiration or pressing the start button again.

### `void toggleDifficultyLevel()`

Cycles the difficulty level between `EASY`, `MEDIUM`, and `HARD`. Each level has a different word typing time limit:
   - **Easy**: 7 seconds
   - **Medium**: 5 seconds
   - **Hard**: 2 seconds

This function is only called if the game is inactive and the debounce delay has passed to avoid rapid toggling.

**Usage**: The player can press the mode button to change difficulty before the game starts.

### `bool isCorrectInput(const String& input)`

Checks if the player's typed input (`input`) matches the current word (`targetWord`).

**Usage**: Called whenever the player enters a word to verify if it matches the target word.

### `void setup()`

Configures pin modes, initializes Serial communication, and sets the RGB LED to white to indicate the game is ready. Displays an initial message and selected difficulty level on the Serial Monitor.

**Usage**: Runs once when the Arduino program starts.

### `void loop()`

The main game loop, which:
   - Checks `start` and `mode` button states to start/stop the game and toggle difficulty.
   - Ends the round when the time limit expires and updates the word according to the difficulty level.
   - Reads player input, validating if the input matches the current word and updating the score.

**Usage**: Controls the game flow, handles game state changes, and manages user interaction.


## How to Play
1. **Setup**: Assemble the circuit according to the wiring diagram and upload the provided Arduino code to your Arduino UNO.

2. **Starting the Game**:
   - Press the difficulty button to select your preferred difficulty level (Easy, Medium, Hard). Each time you press it, a message will be displayed in the terminal indicating the current difficulty.
   - Press the start/stop button to begin the game. A countdown will be displayed, and the RGB LED will blink for 3 seconds.

3. **Typing the Words**:
   - After the countdown, the RGB LED will turn green, and a word will be displayed in the terminal.
   - You have a limited time to type the displayed word based on the selected difficulty:
     - **Easy**: 5 seconds
     - **Medium**: 3 seconds
     - **Hard**: 2 seconds
   - If you type the word correctly, the LED will stay green, and a new word will appear immediately.
   - If you type the word incorrectly, the LED will turn red. You can correct your input by using the Backspace key to delete characters and retype the word.

4. **Ending the Game**:
   - The game will continue for a total of 30 seconds, with new words appearing at intervals determined by the difficulty level.
   - At the end of the round, your score (the number of correctly typed words) will be displayed in the terminal.
   - You can stop the game at any time by pressing the start/stop button.

5. **Enjoy the Challenge**: Test your typing speed and accuracy against the clock and see how many words you can type correctly!
