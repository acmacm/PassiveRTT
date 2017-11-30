## The Range of Detectable Frequencies is Constrained by the Packet Rate

The Carra paper gives limits on detectable frequencies: 

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
For the set of impulse periods, T, that we are evaluating, I'm beginning to 
wonder if the Nyquist sample limit applied here (N/2) is applicable.
The sample times and the interarrival times (signal to detect) are directly related,
and this is not the case for many applications of Lomb-Scargle.

The limits as formulated above are a tight restriction on applicable
streams, especially when considering that Carra et al. indicate that
a multiple of the fundamental frequency is expected to have peak power
(and the fundamental is only determined after evaluating lists of 
candidates). In the TCP3 analysis, the detected peak frequency was ~ 4 times the expected
fundamental frequency (from Wireshark RTT measurements).
