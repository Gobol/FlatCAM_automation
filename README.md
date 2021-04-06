# FlatCAM_automation

FlatCAM process TCL automation script - automate KiCAD gerber processing into GCODE files for CNC PCB milling.

# Structural convention - using default KiCAD naming setup : 

- default PCB layers stack 
- *F-Cu* holds front copper layer
- *B-Cu* holds back copper layer
- *Eco1.User" holds front engraving layer (for engraved texts, etc...)
- *Eco2.User" holds back engraving layer
- *Edge.Cuts" holds cutout shape 

# Script conventions & parameters : 

Script tries to detect automatically when processing one-sided or two-sided boards (two sided if \*B-Cu file loaded correctly into FlatCAM).
KiCAD's output plots must be present in **<project_dir>/gerber/** directory.

Parameters: 

- kicad_name "rflink_shield" - KiCAD project name (also directory holding the project)

- kicad_path "/mnt/code/kicad/" - kicad projects path (base), resolving to kicad_path+kicad_name (eg. /mnt/code/kicad/rflink_shield/)

- output_path "/mnt/gcodes" - output path for resulting gcodes, resolving to output_path+kicad_name (eg. /mnt/gcodes/rflink_shield/)

- track_z_cut -0.07   - track isolation engraving depth
- isolation_overlap 0.5   - track isolation multipass (2 passes) overlap
- annot_z_cut -0.05   - annotations engraving depth
- track_xy_feed 300   - engraving speed in mm/s
- z_feedrate 100	    - z_plunge speed in mm/s when engraving
- mirror_axis "Y"     - two-sided board mirror axis (X=up/down or Y=left/right)
set shallow_hole_diam_front 0.3
set shallow_hole_diam_back 0.35
set shallow_hole_depth -0.5
set thruhole_z -1.8
set cutout_z_cut -1.8
set cutout_cut_per_pass 0.9
set cutout_feedrate_xy 120
set cutout_feedrate_z 80
set align_holes_depth -6
set align_holes_dia 1.5
- spindle_rpm 1000    - spindle rotational speed
- spindle_dwell 2     - spindle spin-up wait time before job


Drilling diameter conventions : 
- 0.30mm drills - make shallow (0.5mm depth, typically 0.6mm dia) holes on front layer 
- 0.35mm drills - make shallow holes on back layer

# Results files naming convention : 

**[No][M?]_[TOOL]_[DESC].nc **

[No] - files are numbered - they should be processed in following order on CNC machine
[M?] - if M present - denotes mirrored layer (back side process)
[TOOL] - 3 character tool code, eg. 45V - 45 degree V-bit engraver, 1D5 - drill 1.5mm, 1F0 - Flat bit 1.0mm
[DESC] - file description

## USAGE:

1. Import script to **empty project** in FlatCAM (File->Scripting->Open script)

2. Adjust variables/parameters/paths according your needs 

3. Push "RUN"

4. Check results

5. Don't forget to save your script with modified variables for future use 
