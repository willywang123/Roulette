# 🎰 FPGA Roulette Game

## 📌 Overview
This project implements a fully interactive **Roulette game** on an FPGA platform (**DE1-SoC**) and can also be run on **CPUlator**. The game features real-time graphics rendering, keyboard-based input, animated physics for the spinning wheel and ball, and dynamic betting logic.

The system integrates low-level hardware control with game logic to simulate a realistic casino roulette experience.

## 🚀 Features

- 🎮 **Interactive Gameplay**
  - Place bets using a PS/2 keyboard
  - Select bet types such as exact number, color, and range
  - Track balance in real time

- 🎡 **Animated Roulette Wheel**
  - Smooth wheel rotation using trigonometric transformations
  - Ball motion simulation with friction and deceleration

- 🖥️ **Graphics Rendering**
  - Double buffering for flicker-free animation
  - Custom drawing functions for circles, lines, and rectangles
  - Background and UI rendering from image buffers

- ⌨️ **Keyboard Input**
  - PS/2 scan code decoding
  - Support for numeric input and betting controls

- 💰 **Betting System**
  - Multiple chip denominations: $1, $2, $5, $10
  - Different betting categories including exact number, ranges, color, and parity
  - Automatic payout calculation

- 🔢 **Hardware Integration**
  - 7-segment display for balance
  - LEDs for timer and game feedback
  - Memory-mapped I/O for peripherals

## 🧠 System Architecture

The program is organized into several main components:

### 1. Graphics Engine
- Uses pixel buffer memory with double buffering
- Implements:
  - Bresenham circle drawing
  - Line drawing
  - Image rendering
- Core functions:
  - `plot_pixel()`
  - `drawFilledCircle()`
  - `draw_line()`

### 2. Game Logic
- Handles:
  - Betting
  - Balance updates
  - Game state transitions
- Key variables:
  - `balance`
  - `bet[]`
  - `betChoice`
  - `gameNum`

### 3. Physics Simulation
- Ball motion:
  - Circular motion using `cos()` and `sin()`
  - Gradual slowdown through friction
- Wheel rotation:
  - Rotational transformation of pixels

### 4. Input Handling
- PS/2 keyboard interface:
  - `readKeyboard()`
  - `ps2Decoder()`
- Key mappings:
  - `A/S/D/F` → betting chips
  - `0–9` → number selection

### 5. Hardware Interface
- Memory-mapped addresses for:
  - Timer
  - LEDs
  - HEX displays
  - Pixel buffer controller

## 🎮 How to Play

1. **Start the Game**
   - Press `KEY0` to start immediately
   - Or use `KEY1` to navigate through the instruction screens

2. **Place Bets**
   - Use:
     - `A` → $1
     - `S` → $2
     - `D` → $5
     - `F` → $10
   - Enter a roulette number (`0–37`) using the keyboard
   - Use function keys (`F1–F9`) to choose other bet types

3. **Wait for the Spin**
   - A countdown timer runs before the wheel starts spinning

4. **View the Result**
   - The ball lands on a number
   - The balance updates automatically based on the result

5. **Restart**
   - When the balance reaches 0, press `Space` to restart the game

## 🛠️ Build & Run

### Requirements
- **Option 1:** DE1-SoC FPGA board
- **Option 2:** CPUlator simulator
- ARM-compatible C toolchain
- VGA display and PS/2 keyboard for FPGA execution

### Running on FPGA
1. Compile the C source file
2. Load the program onto the DE1-SoC board
3. Connect the VGA display and PS/2 keyboard
4. Run the program and interact with the game in real time

### Running on CPUlator
1. Open the **CPUlator ARMv7 DE1-SoC simulator**
2. Load the compiled program or source file
3. Run the simulation
4. Interact using the simulator’s supported I/O devices

## 📂 File Structure

- `Roulette_FINAL.c` — main game logic
- Image assets:
  - `background`
  - `start_screen`
  - `instruction_screen`
  - `keyboard_screen`
  - `endingPage`
- Chip sprites:
  - `$1`
  - `$2`
  - `$5`
  - `$10`

## ⚙️ Key Implementation Details

### Double Buffering
Two pixel buffers are used to prevent flickering and screen tearing during animation:
- `Buffer1`
- `Buffer2`

### Wheel Outcome Calculation
The program computes the final roulette result using angular offsets and maps the stopping position to a roulette number through a lookup table.

### Timing System
A hardware timer controls the countdown and pacing of gameplay.

## 🧩 Challenges & Learnings

- Synchronizing graphics updates using vertical sync
- Implementing smooth animation on limited hardware
- Decoding low-level PS/2 keyboard scan codes
- Designing efficient pixel-level rendering functions
- Combining embedded hardware control with interactive game logic

## 📈 Future Improvements

- Add sound effects
- Improve the user interface and animations
- Support more betting options
- Make the physics simulation more realistic
- Add a multiplayer mode

## 👨‍💻 Authors

- **Zhengyang (Willy) Wang**
- **Zhuoyang (Jack) Li**
