# HP45-standalone-controller-V4.02
HP45 standalone controller V4.02

This github repository is a direct upload of the HP45 Standalone controller V4.02.

This version uses a Teensy 3.5, has all the extra circuits to use DMA for inkjet, and has self testing capabilities. 
A more detailed set of information can be found here: https://ytec3d.com/hp45-controller-v4/

The firmware to run on this board is found here: https://github.com/yvodehaas/HP45-standalone-V4
And the software to control it is found here: https://github.com/yvodehaas/Inkjet-commander
Oasis controller also works on this controller, though it will only work in an Oasis based machine: https://hackaday.io/project/86954-oasis-3dp

This project has been discontinued on my side and is uploaded in the hope that someone else can use it as a template or as is. It is provided without warranty.

The board has a few known issues to keep in mind:
- The reset pulse circuit that resets the TLC59213 using the 74HC123 NEEDS to work. Without this the TLC59213 stays powered. Best case this destroys the HP45 nozzles on the HP45, works case it first destroys the TLC59213, then the Teensy 3.5
- The TLC59213 has a direct connection to the Teensy 3.5. The TLC59213 breaking usually applies the 12V supply to the Teensy 3.5 pins, destroying it.
- The Address testing circuit sometimes gives false negatives. The controller will still print, but while throwing errors.
- The resistor accross the 4017 and 4081 circuit (address circuit) is there to raise the voltage for the nozzle check circuit. The HP45 has pulldown resistors that lowered the voltage on the test circuit sufficiently to stop being able to test.
- Temperature is an indication. The formula was based on 2 printheads while it is known that the HP45 has no accurate temperature sensor. 80C at startup is possible.
- The controller needs 3 pulses to fire all nozzles in an address. This is done 5 primitives, 5 primitives and 4 primitives on each address. This seems to be an issue in the HP45, where too much heat builds up, leading to misfirings. Varying the voltage on the VHD should make this better, but this needs to be calibrated for each printhead.

This list will get appended when more issues are found.
