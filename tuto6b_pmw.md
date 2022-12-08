## Change PWM period

The PWM period is 1.3 ms by default (about 770 Hz). In order to change the period,
you can just adjust the values in line 138 of [au_plus_top.luc](https://github.com/mufpga/MicroFPGA/blob/f8a2190763355563aa698f6f22a582752207a964/Au%2B/source/au_plus_top.luc#L138) (or corresponding line for the
Cu FPGA):

```verilog
pwm pulsewm[NUM_PWM](#TOP(254),#DIV(9),#WIDTH(8));
```

As specified by Alchitry, the `TOP` and `DIV` are responsible for the
period in the following manner:

```
If you need a specific period (i.e. for servos),
you can use DIV to divide the clock in powers
of 2 and TOP to set the max value.

If TOP is 0, 2^WIDTH is used for TOP.

Note that if WIDTH isn't big enough to store the
TOP value, TOP will never be reached and 2^WIDTH
will be used instead.

The duty cycle is: TOP / value
The period is: TOP / (CLK_FREQ / 2^DIV)

For a servo, you typically want a frequency of
50Hz, or a period of 0.02 seconds. With a
clock frequency of 50MHz, you should use
TOP = 244, DIV = 12, and WIDTH = 8. If you
want more resolution you can use
TOP = 62500, DIV = 4, and WIDTH = 16.
```

Where `CLK_FREQ` is 100 MHz.

For instance with a 8 bits `WIDTH` (see the other PWM tutorial for how to changed
the bit depth):
|  TOP  | DIV |  Period  |
| :---: | :-: | :------: |
|  250  |  2  |  0.01 ms |
|  156  |  6  |  0.1 ms  |
|  254  |  9  |  1.3 ms  |
|  244  | 13  |  20 ms   |

1. Change the `TOP` and `DIV` values.
2. Recompile the code and upload it to the FPGA.
