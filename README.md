# DIGITAL CLOCK WITH ALARM - VERILOG DESIGN
This Verilog module implements a digital clock with an alarm functionality. It includes seven output signals, notably Hour, Minute, Second, and Alarm. The system operates in 24-hour format, and the time and alarm values can be manually set.

A 10 Hz input clock is used to generate a 1-second clock internally. This 1-second clock then drives the counter logic for seconds, minutes, and hours.

# Functional Overview
The clock provides initialization through a reset or by enabling LD_time. Alarm configuration is done using LD_alarm, and it can be toggled ON/OFF using AL_ON. Once active, the alarm signal (Alarm) will go HIGH when the real-time matches the alarm time and will stay HIGH until STOP_al is triggered.

# Input Ports
reset: Active-high reset that initializes the clock to the values on H_in1, H_in0, M_in1, and M_in0 while setting seconds to 00. Also resets the alarm to 00:00:00 and ensures the alarm signal is LOW. During normal operation, this must be LOW.

clk: A 10 Hz external clock source. Used to generate a 1-second tick internally.

H_in1: 2-bit input for the most significant digit of the hour (0–2), used when loading time or alarm.

H_in0: 4-bit input for the least significant digit of the hour (0–9).

M_in1: 4-bit input for the most significant digit of the minute (0–5).

M_in0: 4-bit input for the least significant digit of the minute (0–9).

LD_time: When HIGH, sets the current time to the input hour and minute values and resets seconds to 0.

LD_alarm: When HIGH, sets the alarm time using the values on H_in1, H_in0, M_in1, and M_in0.

STOP_al: If the alarm signal is HIGH, setting this input HIGH will deactivate the alarm.

AL_ON: Enables or disables the alarm function. The alarm will only trigger when this input is HIGH.

# Output Ports
Alarm: This output goes HIGH when the current time matches the set alarm time and AL_ON is HIGH. It remains HIGH until STOP_al is triggered.

H_out1: Most significant digit of the current hour (0–2).

H_out0: Least significant digit of the current hour (0–9).

M_out1: Most significant digit of the current minute (0–5).

M_out0: Least significant digit of the current minute (0–9).

S_out1: Most significant digit of the current second (0–5).

S_out0: Least significant digit of the current second (0–9).

# Internal Registers and Signals
clk_1s: Generated 1-second clock derived from the 10 Hz input clock.

tmp_1s: Counter used to divide 10 Hz clock into 1 Hz clock.

tmp_hour, tmp_minute, tmp_second: Registers holding current hour, minute, and second values respectively.

# Clock Time Internal Registers

c_hour1, c_hour0: Hour digits (MSB and LSB).

c_min1, c_min0: Minute digits (MSB and LSB).

c_sec1, c_sec0: Second digits (MSB and LSB).

# Alarm Time Internal Registers

a_hour1, a_hour0: Hour digits of alarm.

a_min1, a_min0: Minute digits of alarm.

a_sec1, a_sec0: Second digits of alarm (set to zero by default).
