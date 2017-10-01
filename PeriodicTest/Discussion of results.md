## A Test using a Periodic Sample of Constant Rate Packet Stream (synthesised)

After seeing a good and simple TCP stream fail to produce a viable estimate of RTT, 
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



indicates that the periodicity was observed, but the value at 100 Hz is a prominant minimum.
