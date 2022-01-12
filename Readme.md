# Calibrate BLTouch with KP3S Official Firmware

Follow the instruction doc of the BLTouch wire connections in Kingroon official from
![Official Kingroon KP3S with BLTouch leveling sensor modification firmware](https://drive.google.com/file/d/1mSXZBLzWFwz71TwLO893RK2lJLcrCqDr/view?usp=sharing%C2%A0). 

Make sure do a manual bed leveling before copy the robin_nano_cfg.txt into sdcard to enable auto bed leveling in KP3S.

## Calibrating the BLTouch
For next steps, you will need prointerface or Octoprint to send few GCode to KP3S. The commands starts with:
1. Home Z axis by sending Home Z commands: G28 Z 
1. Make sure Z_PROBE_OFFSET_FROM_EXTRUDE is set to 0 and the bed leveling is done manually.
1. Probe the bed by sending G30. Please make BLTouch is properly triggered. If it is too close, send G30 Z10 instead. Write down the reported Z offset.
1. Edit the robin_nano_cfg.txt in sdcard, change the value of Z_PROBE_OFFSET_FROM_EXTRUDER to the negative value of the Z offset + the nozzle distance from bed (typically 0.1 with manual leveling process). 
1. Update X_PROBE_OFFSET_FROM_EXTRUDER and Y_PROBE_OFFSET_FROM_EXTRUDER according to BLTouch mount you used.
1. Load the updated robin_nano_cfg.txt to KP3S after that.


For example, if the G30 reported value of 4.1, the final offset will be as below:
```
>Z_PROBE_OFFSET_FROM_EXTRUDER	-3.61	# Z Æ«ÒÆ: -below +above  [the nozzle]		
>X_PROBE_OFFSET_FROM_EXTRUDER	31.0	# X Æ«ÒÆ: -left  +right  [of the nozzle]
>Y_PROBE_OFFSET_FROM_EXTRUDER	-1.0	# Y Æ«ÒÆ: -front +behind [the nozzle]
```

**Warning**: Too much Z Offset will collide the nozzle into the bed.

