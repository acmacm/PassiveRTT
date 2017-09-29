## Second Try with TCP

I found a fairly simple Lab trace with a short transfer in one direction.
The TCP transfer only contains 45 packets after tshark filtering.

Wireshark indicates RTTs between 3ms and 6ms

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
