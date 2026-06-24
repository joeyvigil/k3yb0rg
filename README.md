# K3YB0RG

v4n4g0n inspired, 3d printable keyboard

![K3YB0RG](images/topView.jpg)
![K3YB0RG](images/sideView.jpg)
![K3YB0RG](images/assem_pic.jpg)
![K3YB0RG](images/assem_pic2.jpg)
![K3YB0RG](images/assem_pic3.jpg)
![K3YB0RG](images/top_diss.jpg)
![K3YB0RG](images/top_diss2.jpg)

## Materials
1. 3D Printer
2. Filament (PLA)
3. 1N4148 diodes (one for each switch)
4. Switches
5. Keycaps
6. Stabilizers (6.25u Cherry style for space bar)
7. Micro-Controller (I used a Pro Micro with USB C, but others with ATmega32U4 will work)
8. Nuts and Bolts (12 M3 x 16mm hex screws and nuts)
9. Wire (I've had the most luck only using 20-28 awg solid core wire. I use the soldering iron to remove insulation.)
10. USB Cable (USB C to USB A in my case)
11. Soldering Iron (A basic soldering iron will do, quality does not matter too much)
12.  Solder (60-40 rosin core solder works best)
13.  Solder Sucker
14.  Zip Ties (for securing micro-controller)

## 3D Printing

1. Download the STL files from the releases section.
2. Slice the files using your preferred slicer settings. I recommend using:
   - a layer height of 0.2mm
   - printing at 90% infill 
   - a brim for better bed adhesion
   - supports for the bottom parts
3. Print the following parts:
    - V4N_bot_left.stl (fits a wide range of micro-controllers)
    - V4N_bot_right.stl
    - V4N_top_left.stl
    - V4N_top_right.stl

## Soldering

### How the wiring works — read this first

The Pro Micro doesn't have one pin per key. The 49 keys are wired as a **grid of 5 rows × 12 columns**, and the controller scans that grid to detect presses — so you only run **5 + 12 = 17** signal wires, not 49.

Every switch has two legs, and you solder **three things** to them:

- **One leg → its COLUMN** — joined by a wire to every other switch in the same vertical column.
- **Other leg → a DIODE → its ROW** — solder a diode to the second leg, then join the diodes along each horizontal row.

The diode prevents *ghosting* (phantom keypresses when several keys are held at once). It only passes current one way, so **every diode must face the same direction** — on this board the **black band points toward the row**. Keep them consistent and the matrix just works.

![How the K3YB0RG matrix is wired](images/matrix_diagram.png)

**Where the wires land on the Pro Micro** (these come straight from `k3yb0rg.json`, so they always match the firmware):

| | Pins (in order) |
|---|---|
| **Rows** 0 → 4 (diode side) | `D3, D2, D1, D0, D4` |
| **Columns** 0 → 11 (other leg) | `C6, D7, E6, B4, B5, B6, B2, B3, B1, F7, F6, F5` |

If a key misreads after flashing, it's almost always one row/column wire on the wrong pin, or a diode soldered in backwards.

The photos below show the same thing on a real board.

### Rows

1. Place all switches into the top case pieces.
2. Put in space key Stabilizer (you'll regret having to de-solder later if you don't do it now)
3. Solder a diode to each switch with the **black band facing the row wire** (it points down in the photo below):
   ![A row of switches with a diode soldered to each, black band facing the row wire](images/rows.jpg)
4. Solder a wire at the end of each row of switches (this will go to the micro-controller).

### Columns
1. Cut pieces of wire long enough to reach from the top of the switch to the micro-controller pins.
2. Solder the wires in the following configuration:
    - **Tip:** I like to burn away the insulation on the wire at the points where I want to solder.
![Column Wiring](images/wiring.jpg)

### Microcontroller
1. Solder wires to the microcontroller in the following configuration:
![kbfirmware pin assignment for the Pro Micro](images/pins.jpg)
![Pro Micro pinout reference](images/pro_micro_pinout.jpg)

## Programming
1. Download and install [QMK Toolbox](https://qmk.fm/toolbox/)
2. Download the hex file k3yb0rg.hex.
3. Connect the micro-controller to your computer.
4. Open QMK Toolbox and flash the k3yb0rg.hex file to the micro-controller.
   - open hex file
   - check "Auto-flash"
   - make sure the correct micro-controller is selected (ATmega32U4 for Pro Micro)
   - press reset button on micro-controller (if available) or short RST to GND
   - wait for "Flash complete!" message
5. Your keyboard should now be functional. Open a [keyboard tester](https://www.keyboardtester.com/) to verify all keys work.
6. If you want to customize the keymap or Wiring, you can use [keyboard firmware builder](https://kbfirmware.com/), click upload and open the k3yb0rg.json file.

## Assembly
1. Place the micro-controller into the bottom left case piece and secure it with a zip tie.
2. assemble the top and bottom case pieces together using the 3M x 16mm screws and nuts.
3. Place keycaps on switches.
4. Enjoy your new keyboard!


## V4N4G0N inspired design

![K3YB0RG](images/FeZixgI.jpg)

![K3YB0RG](images/v4n4g0n-r1.png)

## Layers
you can edit the layers using keyboard firmware builder or QMK Configurator. (Using the k3yb0rg.json file)
![Layers](images/layer1.jpg)
![Layers](images/layer2.jpg)
![Layers](images/layer3.jpg)


## Video Guide
Here is an old video guide I made for a previous keyboard:
[![K3YB0RG Build Guide](https://img.youtube.com/vi/XAc28t4e77w/0.jpg)](https://www.youtube.com/watch?v=XAc28t4e77w)

## Timelapse

[![K3YB0RG Timelapse](https://img.youtube.com/vi/-jxHc12UWSU/0.jpg)](https://youtu.be/-jxHc12UWSU)

## Thanks
