In this first attempt to calculate some Periodograms,
I captured packets with Wireshark and operated on the
.pcapng files to produce a vector of the packet arrival times
that met filter criteria.

For example, the command:
```
tshark -Y "quic && ip.dst==192.168.1.120" -r chrome_wlan_Cumberland.pcapng -o "gui.column.format:\"Time\",\"%t\"" > DstTime.txt
```
will filter the Google QUIC packets travelling in a single direction
from an existing .pcapng file, and produce a text file with the 
"time since capture started" as configured in Wireshark (View -> Time Display Format).

Next, we turn to the (free) R-tool for Statistical Analysis, which has 
a Package to calculate the Lomb-Scargle Periodogram:

https://cran.r-project.org/web/packages/lomb/index.html

The package needs to be Installed and Loaded in R.

Note that this standard package does not implement the 
shifting window of N samples used to build an estimation of
the spectrum. However, this can be managed with an R script
and is for further work.

We next read-in the .txt file (times)
and calculate the Inter-arrival times (x) in R 
(for 500 packet arrivals from a longer capture):
```
> times = scan(file = "DstTime_500.txt")
Read 500 items
> n = length(times)
> x = rep(0,n)
> for (j in 2:n) { x[j] = times[j] - times[j-1] }
> x
  [1] 0.000000 0.001080 0.031642 0.000284 0.002855 0.001319 0.000001 0.000266
  [9] 0.000000 0.000664 0.000001 0.000776 0.000002 0.000445 0.000002 0.000382
 [17] 0.000587 0.000867 0.000001 0.000450 0.000731 0.001362 0.000001 0.000613
...
[481] 0.003177 0.000001 0.000000 0.000721 0.001363 0.000414 0.000473 0.000518
[489] 0.006508 0.001001 0.002047 0.000001 0.000970 0.000001 0.000001 0.001057
[497] 0.000001 0.000903 0.000001 0.001008
```

Next, we submit vectors x and times to the Periodogram calculation
(which can use other parameters, such as the frequency range, false alarm alpha, etc.):

```
> lombData = lsp(x, times = times, from = 1, to = 1000, type = "frequency", alpha = 0.1, plot = TRUE)
> lombData$peak
[1] 5.442109
> lombData$peak.at
[1] 1.660570 0.602203
> lombData$p.value
[1] 0.9946199
```
The calculated peak period seems to be at ~602ms, but the peak power
fails to exceed the false alarm threshold, as shown in the plot that
the lsp() function optionally produces:

https://github.com/acmacm/PassiveRTT/blob/master/chrome_wlan_dst_quic_500_alpha10_Cumberland.pdf

Since the ~600ms RTT seemed on the long side, I pinged the server that 
was sourcing the QUIC stream, and ICMP RTT was quite a bit lower:
```
>ping 172.217.8.14
Pinging 172.217.8.14 with 32 bytes of data:
Reply from 172.217.8.14: bytes=32 time=24ms TTL=54
Reply from 172.217.8.14: bytes=32 time=22ms TTL=54
Reply from 172.217.8.14: bytes=32 time=30ms TTL=54
Reply from 172.217.8.14: bytes=32 time=27ms TTL=54

Ping statistics for 172.217.8.14:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 22ms, Maximum = 30ms, Average = 25ms
```

It's proably a good thing that the first tool-chain run-through
didn't produce great results immediately, because there are many
alternative analysis angles to try, and if this was easy,
they wouldn't pay us the big bucks...

I'm inclined to look at other segments of the capture. The stream was 
from YouTube: https://www.youtube.com/watch?v=tZaeKwgS7wg   
(audio of Jason Isbell's song "Cumberland Gap"), and received
on my chrome browser Version 60.0.3112.78 . 
I also plan to try this method with a few of the many other pcap
files on my hard drive.  The original authors focused on TCP flows.


