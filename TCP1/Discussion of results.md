## First Try with TCP

As a logical step beyond getting the tool-chain working, 
applied the tools to a classic FTP/TCP file transfer.

The Wireshark version of the RTT plot shows mostly 
RTTs less than 30ms:
https://github.com/acmacm/PassiveRTT/blob/master/TCP1/TCP1_WS_RTT.pdf

```
tshark -Y "ftp-data && ip.dst == 10.255.255.2" -r m2-255-139_Eth_July03-PC-Bband.pcap -o "gui.column.format:\"Time\",\"%t\"" > DstTimeTCP1.txt

> times = scan(file = "DstTimeTCP1.txt")
Read 686 items
> n = length(times)
> x = rep(0,n)
> for (j in 2:n) { x[j] = times[j] - times[j-1] }
> lombData = lsp(x, times = times, from = 1, to = 1000, type = "frequency", alpha = 0.1, plot = TRUE)
> lombData$peak.at
[1] 99.93137995  0.01000687
> lombData$p.value
[1] 0.3842117
```
https://github.com/acmacm/PassiveRTT/blob/master/TCP1/TCP1_LP_freq.pdf
The peak at ~10 ms could be legitimate, but the p value and 
confidence are low.

Changing the frequency range didn't help, in fact, this range excluded the former peak:
```
> lombData = lsp(x, times = times, from = 500, to = 1000, type = "frequency", alpha = 0.1, plot = TRUE)
> lombData$peak.at
[1] 8.999913e+02 1.111122e-03
> lombData$p.value
[1] 0.8147793
```
https://github.com/acmacm/PassiveRTT/blob/master/TCP1/TCP1_LP_freq_500-1000.pdf

Next, I tried a smaller number of packet interarrival times, just 200:
```
> times = scan(file = "DstTimeTCP1_200.txt")
Read 200 items
> n = length(times)
> x = rep(0,n)
> for (j in 2:n) { x[j] = times[j] - times[j-1] }
> lombData = lsp(x, times = times, from = 1, to = 1000, type = "frequency", alpha = 0.1, plot = TRUE)
> lombData$peak.at
[1] 1.419557e+02 7.044449e-03
> lombData$p.value
[1] 1
> 
```
https://github.com/acmacm/PassiveRTT/blob/master/TCP1/TCP1_200_LP_freq.pdf

The result is no better than chance, according to the p-value.

The requirements to detect frequencies correposnding to the measured RTTs are not quite met here:
```
The TCP1 filtered pcap file contains 687 packets
Total time of the filtered capture = 13.139016 Seconds  (~52 pkt/sec)
f_min = 1/time = 0.076 Hz
f_max = 687/2 * f_min =  26.144
==>>> These values don't match the Measured RTT 
      (10 to 20 ms, 100 to 50 Hz)

But, if we look at the first 256 packets (as in the Carras paper)
Time in the capture = 5.908809 Seconds
f_min = 1/time = 0.1692 Hz
f_max = 256/2 * f_min = 21 Hz
So, we still don't have sufficient frequency range to detect 100 Hz,
(or any multiples of the 100Hz fundamental freq.)
```
