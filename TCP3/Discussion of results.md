## Analysis of a HD Stream using Flash, steady rate is ~1Mbit/sec 
Chose single direction for analysis and processed with tshark:
```
tshark -Y "tcp && ip.dst == 156.106.205.1" -r StreamFlashHDCapture.pcap -o "gui.column.format:\"Time\",\"%t\"" > DstTimeTCP3.txt
```
At this point, I've begun to use a source script to automate the R processing, 
anticipating that this will be useful when the need to perform window processing
and analysis on a list of peak frequencies which could represent the fundamental freq.
that stems from the RTT.

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
