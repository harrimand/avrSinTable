# avrSinTable
Python source to generate AVR assembly directives that create a table of values to be added to a 
Pulse Width Modulation register.  The values will create a sinusoidal motion on a servo motor attached 
to the output compare pins OC1A or OC1B.  The servo should be positioned to it's center position before
reading the table values and updating the Pulse Width Register.  The values in the table are signed 8 bit 
Hex values.  The high byte of the 16 bit value being added to the Pulse Width register should be set to all 
ones if the most significant bit of the value read from the table is a one.  Otherwise the high byte should 
be cleared.  You can clear the high byte, then test the most significant bit of the value read using sbrc 
command (skip if bit in register cleared) followed by a ser command (set bits in register) that will set 
the high byte to all ones.

Example:<br>
```
lpm   TEMPL, Z+
clr   TEMPH
sbrc  TEMPL, 7
ser   TEMPH
add   pwL, TEMPL
adc   pwH, TEMPH
```
