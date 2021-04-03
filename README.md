# FlatCAM_automation
FlatCAM process TCL automation script 

1. KICAD project preparation & conventions

- default PCB layers stack 
- *F-Cu* holds front copper layer
- *B-Cu* holds back copper layer
- *Eco1.User" holds front engraving layer (for engraved texts, etc...)
- *Eco2.User" holds back engraving layer
- *Edge.Cuts" holds cutout shape 
- Drills conventions : 
- 0.30mm drills - make shallow (0.5mm depth, typically 0.6mm dia) holes on front layer 
- 0.35mm drills - make shallow holes on back layer
- any other are drilled on front, when single sided board detected or back when double-sided board given to process

2. Import script to empty project in FlatCAM (File->Scripting->Open script)

3. Adjust variables to your needs 

4. Push "RUN"

5. Check results

6. Don't forget to save your script with modified variables for future use 
