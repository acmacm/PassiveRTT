## Analysis of a HD Stream using Flash, steady rate is ~1Mbit/sec 
Chose single direction for analysis and processed with tshark:
```
tshark -Y "tcp && ip.dst == 156.106.205.1" -r StreamFlashHDCapture.pcap -o "gui.column.format:\"Time\",\"%t\"" > DstTimeTCP3.txt
```
The Wireshark TCP analysis indicates many RTT ~60ms, but also many very low RTT (<5ms). 

https://github.com/acmacm/PassiveRTT/blob/master/TCP3/StreamFlashHD_RTT.pdf

The Wireshark Throughput and Stevens plots are also available:

https://github.com/acmacm/PassiveRTT/blob/master/TCP3/StreamFlashHD_Tput.pdf

https://github.com/acmacm/PassiveRTT/blob/master/TCP3/StreamFlashHD_Stevens.pdf

At this point, I've begun to use a source script to automate the R processing, 
anticipating that this will be useful when the need to perform window processing
and analysis (on a list of peak frequencies which could represent the fundamental freq.
considerable averaging to obtain the RTT.

```
> source(file = "LSP_script.txt")
Read 4818 items
(script preps and runs lsp)
> lombData = lsp(x, times = times, from = 1, to = 1000, type = "frequency", alpha = 0.1, plot = TRUE)
lombData$peak.at
[1] 64.00682700  0.01562333
lombData$p.value
[1] 0.6300621
```
The Lomb-Scargle Periodogram indicates a single strong peak frequency:

https://github.com/acmacm/PassiveRTT/blob/master/TCP3/TCP3_LP_freq1000_a0.1.pdf

but this peak at 64 Hz or 15.6 ms is not easliy related to the measured RTTs,
maybe one fourth of 60 ms, or a multiple of one of the very small RTTs (< 5 ms).

At least the p-value is only leaning toward a chance outcome.
