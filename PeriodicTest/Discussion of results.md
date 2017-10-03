## A Test using a Periodic Sample of Constant Rate Packet Stream (synthesised)

After seeing a good and simple TCP stream produce only a multiplier-related estimate of fundamental frequency and RTT, 
I prepared a set of times and timestamps that simulate a Preiodic Stream, 
and submitted the timestamps to the Lomb-Scargle analysis.

The time stamps were all 0.01 seconds apart, so we should see 
100 Hz frequency prominantly represented in the results.

```
> times = scan(file = "Periodic//Periodic0.01.txt")
Read 45 items
> n = length(times)
> x = rep(0,n)
> for (j in 2:n) { x[j] = times[j] - times[j-1] }
> lombData = lsp(x, times = times, from = 1, to = 1000, type = "frequency", alpha = 0.1, plot = TRUE)
> lombData$peak.at
[1] 9.500000e+02 1.052632e-03
> lombData$p.value
[1] 1
```
The Periodogram

https://github.com/acmacm/PassiveRTT/blob/master/PeriodicTest/Periiodic0.01_LS_LPa0.1.pdf

indicates that the periodicity was observed, but the value at 100 Hz is a prominant minimum.
There are many related frequency components, and this would be expected from the impulse train.

None of the power levels are close to the alpha = 0.1 threshold, 
and the p value = 1 indicates that this result certainly occured by chance.
At least the periodogram is less noisy.

This analysis suffers from too few packets and insufficient packet rate.

Trying to match the requirements from f_min and f_max, 400pps stream,
by creating a stream with bursts of 4 packets every 10 ms:

```

> times = scan(file = "Periodic//Periodic0.01_400pps.txt")
Read 401 items
> n = length(times)
> x = rep(0,n)
> for (j in 2:n) { x[j] = times[j] - times[j-1] }
> lombData = lsp(x, times = times, from = 1, to = 1000, type = "frequency", alpha = 0.1, plot = TRUE)
> lombData$peak.at
[1] 6.500000e+02 1.538462e-03
> lombData$p.value
[1] 1
> x[1:30]
 [1] 0.00 0.01 0.00 0.00 0.00 0.01 0.00 0.00 0.00 0.01 0.00 0.00 0.00 0.01 0.00
[16] 0.00 0.00 0.01 0.00 0.00 0.00 0.01 0.00 0.00 0.00 0.01 0.00 0.00 0.00 0.01
> times[1:30]
 [1] 0.00 0.01 0.01 0.01 0.01 0.02 0.02 0.02 0.02 0.03 0.03 0.03 0.03 0.04 0.04
[16] 0.04 0.04 0.05 0.05 0.05 0.05 0.06 0.06 0.06 0.06 0.07 0.07 0.07 0.07 0.08
> 
```
https://github.com/acmacm/PassiveRTT/blob/master/PeriodicTest/Periiodic0.01_400pps_LS_LPa0.1.pdf

Trying reduced alpha =0.50
   Didn't help, L-S is still a flat line...
