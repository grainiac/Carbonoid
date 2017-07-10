**NOTE**

This is my tool change gcode I use in Simplify3D:

{{{
; ====================== Tool Change BEGIN =======================
; all settings optimized for a 60 mm PTFE tube used on hotend side
;
G91                  ; Relative Coordinates
G1 Z+1 E-30 F3000    ; Lift Z 1mm for Tool Change @33mm/s and fast Retract 30mm @50mm/s
G90                  ; Absolute Coordinates
G1 X0 Y140 F4800     ; Move X Y for tool change
;
; select current tool
T[old_tool]     ; Select Old Tool
G92 E0          ; Zero Extruder
;
; perform extraction & reshaping
G1 E10 F3000    ; Fast Reinsert 10mm @50mm/s
G1 E-10 F1800   ; Reshape 10mm @30mm/s
G4 P3000        ; 3s cooling period
G1 E-90 F1800   ; Long retract 90mm @30mm/s
G90             ; Absolute Coordinates
G92 E0          ; Zero Extruder
;
; select new tool
T[new_tool]     ; Select New tool
G92 E0          ; Zero Extruder
G91             ; Relative Coordinates
;
; perform fast reinsert of new filament and initial short feed
G1 E110 F1800   ; Fast insert 110mm @30mm/s
G1 E5 F300      ; Feed 5 mm @5mm/s
G92 E0          ; Zero Extruders
;
G1 Z-1 F2000    ; Return Z to resume printing
G90             ; Absolute Coordinates
;
; ====================== Tool Change END =========================
}}}