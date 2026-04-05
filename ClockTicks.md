Every processor is accompanied by a physical clock (usually quartz crystal clock), which oscillates at certain frequency (vibrations/sec).

The processor keeps track of time by the help of interrupts generated from the physical clock, which interrupts the processor at every time period `T.

On most modern system, `T` valued to be a microsecond.

This interrupt is called a **clock tick**.

Clock ticks refer to the main system clock.
It is the smallest unit of time recognized by the device.

CPU counts the number of interrupts it has seen since the system has started, and returns that value when you call clock().

So, the physical clock interrupts at every 1 microsecond.

By taking a difference between two clock ticks values (obtained from clock()), you would get how many interrupts that were seen between those two time points.

Si le temps renvoyé par clock est de 13000 ClockTicks, cela représente 13 000 microsecondes.
Donc 0.013000 seconde.


