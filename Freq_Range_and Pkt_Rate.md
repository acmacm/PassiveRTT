## The Range of Detected Frequencies is Constrained by the Packet Rate

The Cara paper gives limits on detectable frequencies: 

```
f_min = 1/time (time interval for N packets)
f_max = N/2 * f_min

We have N/2 * (1/time) = f_max
or       N / time = 2 * f_max

If f_max = 200 Hz (to detect a  2x multiple of 100 Hz or 10 ms), 
then     N / time = 400  or 400 packets per second (at least)
This implies a Throughput of 579kB/s or 4.633 Mbit/sec (1448 MSS)

If f_max = 300 Hz (to detect a 3x multiple of 100 Hz or 10 ms), 
then     N / time = 600  or 600 packets per second (at least)
This implies a Throughput of 6.950 Mbit/sec (1448 MSS)

```
