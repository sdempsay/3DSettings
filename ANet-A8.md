Start settings
--------------
```
G28 ; Do a basic homing calibration
G29 ; Do a mesh Z calibration with my Z sensor
M140 S[bed0_temperature] ; bed temp (before moving)
G1 X0 Y0 ; Move the the front of the printer
M104 S[extruder0_temperature] T0 ; Nozzle temp
M190 S[bed0_temperature] ; wait for bed temp
M109 S[extruder0_temperature] T0 ; wait for nozzle temp
G1 X10 Y5 Z0.2 F3000 ; get ready to prime
G92 E0 ; reset extrusion distance
G1 X180 E20 F600 ; prime nozzle
```

Finish settings
---------------
```
M104 S0 ; turn off extruder heater
M140 S0 ; turn off bed heater
G1 X0 Y200 F1000 ; prepare for part removal
M84 ; disable motors
M107 ; turn off fan
```

Multi-color layer stop
----------------------
```
G1 X10 Y10 ; move away from the print (hopefully)
G91 ; Relative mode for the Z axis so we can change out filament
G1 Z20 ; Lift off the bed so that filament can be extruded
```

Multi-color layer start
-----------------------
```
G1 Z0 ; back to the relative 0
G90 ; Back to absolute
G92 E0 ; Reset extrusion
G1 E20 F600; Prime out a bit of filament
G92 E0 ; Reset extrusion
G1 X12 Y5 Z0.2 F3000 ; Move to draw
G1 X180 E20 F600; Draw a quick line, then ready to print
```
