# 3D-printer
# 3D printer using Klipper firmware
# Youtube video : https://youtube.com/shorts/7HvwOleaxaQ?feature=share

#Config
[include mainsail.cfg]

[mcu xy]
serial: /dev/serial/by-id/usb-Arduino__www.arduino.cc__0043_95530343335351601011-if00

[mcu]
serial: /dev/serial/by-id/usb-1a86_USB2.0-Serial-if00-port0

[printer]
kinematics: cartesian
max_velocity: 200
max_accel: 1000

[tmc2209 stepper_x]
uart_pin: xy:PC0
tx_pin: xy:PC3
run_current: 0.5
hold_current: 0.5
sense_resistor: 0.110
stealthchop_threshold: 0
driver_SGTHRS: 95
diag_pin: ^xy:PB4

[stepper_x]
step_pin: xy:PD2
dir_pin: !xy:PD5
enable_pin: !xy:PB0
rotation_distance: 40
homing_speed: 40
microsteps: 16
full_steps_per_rotation: 200
endstop_pin: tmc2209_stepper_x:virtual_endstop
homing_retract_dist: 0
position_endstop: 0
position_max: 270

[tmc2209 stepper_y]
uart_pin: xy:PC1
tx_pin: xy:PC2
run_current: 0.5
hold_current: 0.5
sense_resistor: 0.110
stealthchop_threshold: 0
driver_SGTHRS: 150
diag_pin: ^xy:PB5


[stepper_y]
step_pin: xy:PD3
dir_pin: xy:PD6
enable_pin: !xy:PB0
rotation_distance: 20
homing_speed: 40
microsteps: 16
full_steps_per_rotation: 200
endstop_pin: tmc2209_stepper_y:virtual_endstop
homing_retract_dist: 0
position_endstop: 0
position_max: 350



[stepper_z]
step_pin: PF0
dir_pin: PF1
enable_pin: !PD7
microsteps: 16
rotation_distance: 10
full_steps_per_rotation: 200
homing_speed: 5
endstop_pin: probe:z_virtual_endstop
position_max: 240
position_min: -10

[stepper_z1]
step_pin: PF6
dir_pin: PF7
enable_pin: !PF2
microsteps: 16
rotation_distance: 10
full_steps_per_rotation: 200
#position_endstop: 0
#position_max: 250
#position_min: -3

[stepper_z2]
step_pin: PL3
dir_pin: PL1
enable_pin: !PK0
microsteps: 16
rotation_distance: 10
full_steps_per_rotation: 200
#position_endstop: 0
#position_max: 250
#position_min: -3



[heater_bed]
heater_pin: PH5
sensor_type: EPCOS 100K B57560G104F
sensor_pin: PK6
control: pid
pid_Kp: 26.285
pid_Ki: 0.796
pid_Kd: 216.943
min_temp: -273
max_temp: 273

[board_pins]
aliases :
    # EXP1 header
    EXP1_1=PC0, EXP1_3=PH0, EXP1_5=PA1, EXP1_7=PA5, EXP1_9=<GND>,
    EXP1_2=PC2, EXP1_4=PH1, EXP1_6=PA3, EXP1_8=PA7, EXP1_10=<5V>,
    # EXP2 header
    EXP2_1=PB3, EXP2_3=PC6, EXP2_5=PC4, EXP2_7=PL0,  EXP2_9=<GND>,
    EXP2_2=PB1, EXP2_4=PB0, EXP2_6=PB2, EXP2_8=PG0, EXP2_10=<NC>


[display]
lcd_type: st7920
cs_pin: EXP1_4
sclk_pin: EXP1_5
sid_pin: EXP1_3
encoder_pins: ^EXP2_3, ^EXP2_5
click_pin: ^!EXP1_2
#kill_pin: ^!EXP2_8

[force_move]
enable_force_move: True

[z_tilt]
z_positions: 0, 0
             265, 190
             0, 350     
points: 0, 0
        265, 190
        0, 350
speed: 100
horizontal_move_z: 15
retries: 20
retry_tolerance: 0.05

[probe]
pin: ^!PD3
x_offset: 0.0
y_offset: 0.0
#z_offset: -2


[fan]
pin: PH6

[extruder]
step_pin: PA4
dir_pin: PA6
enable_pin: !PA2
microsteps: 16
full_steps_per_rotation: 200
gear_ratio: 50:17
rotation_distance: 5.355
nozzle_diameter: 0.400
filament_diameter: 1.750
max_extrude_only_distance: 100
heater_pin: PB4
sensor_type: EPCOS 100K B57560G104F
sensor_pin: PK5
#control: watermark
#pid_Kp: 
#pid_Ki:
#pid_Kd:
min_temp: 0
max_temp: 250
max_power: 0.3

[gcode_macro END_PRINT]
variable_machine_depth: 150
gcode:
    # Turn off bed, extruder, and fan
    M140 S0
    M104 S0
    M106 S0
    # Relative positionning
    G91
    # Retract and raise Z
    G1 Z+25 F1500
    G90
    # Disable steppers
    M84
    # Print message on LCD
    M117 That's All Folks

#*# <---------------------- SAVE_CONFIG ---------------------->
#*# DO NOT EDIT THIS BLOCK OR BELOW. The contents are auto-generated.
#*#
#*# [extruder]
#*# control = pid
#*# pid_kp = 8.483
#*# pid_ki = 0.643
#*# pid_kd = 27.994
#*#
#*# [probe]
#*# z_offset = 0.722
