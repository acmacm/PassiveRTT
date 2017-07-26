In this first attempt to calculate some Periodograms,
I captured packets with Wireshark and operated on the
.pcapng files to produce a vector of the packet arrival times
that met filter criteria.

For example, the command:

tshark -Y "quic && ip.dst==192.168.1.120" -r chrome_wlan_Cumberland.pcapng -o "gui.column.format:\"Time\",\"%t\"" > DstTime.txt

will filter the Google QUIC packets travelling in a single direction
from an existing .pcapng file, and produce a text file with the 
"time since capture started" as configured in Wireshark (View -> Time Display Format).

Next, we turn to the R-tool for Statistical Analysis, which has 
a Package to calculate the Lomb-Scargle Periodogram
