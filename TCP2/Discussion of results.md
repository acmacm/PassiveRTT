## Another Try with TCP

I located a fairly simple Lab trace with a short transfer in one direction.
The TCP transfer only contains 45 packets after tshark filtering.
The Stevens plot of Sequence number vs time:

https://github.com/acmacm/PassiveRTT/blob/master/TCP2/HTTP_test_apache2_Stevens.pdf

Wireshark indicates RTTs between 3ms and 6ms, with many less than 4 ms:

https://github.com/acmacm/PassiveRTT/blob/master/TCP2/HTTP_test_apache2_RTT.pdf


```
TCP2
tshark -Y "tcp && ip.dst == 198.228.201.150" -r HTTP_test_apache2.snoop -o "gui.column.format:\"Time\",\"%t\"" > DstTimeTCP2.txt

> times = scan(file = "DstTimeTCP2.txt")
Read 45 items
> n = length(times)
> x = rep(0,n)
> for (j in 2:n) { x[j] = times[j] - times[j-1] }
> lombData = lsp(x, times = times, from = 1, to = 1000, type = "frequency", alpha = 0.1, plot = TRUE)
> lombData$peak.at
[1] 5.857278e+02 1.707278e-03
> lombData$p.value
[1] 0.941433
> 
```
The peak at ~586 Hz corresponds to 1.7 ms, about half the measured RTT. So, this is related to the 
approximate and known fundamental frequency and RTTs between 3 and 4 ms.

The p value is quite high (prob = 0.94 that result occured by chance) and the confidence is below the alpha threshold:

https://github.com/acmacm/PassiveRTT/blob/master/TCP2/TCP2_LP_freq1000_a0.1.pdf

https://github.com/acmacm/PassiveRTT/blob/master/TCP2/TCP2_LP_freq1000_a0.1.jpeg


But, there's a different problem with this trace: There really aren't enough packets to detect the 
fundamental frequency, f ~ 285 Hz, let alone a multiple of the fundamental (2f = 571).

(see the f_min and f_max analysis).
