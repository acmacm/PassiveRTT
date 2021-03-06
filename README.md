# PassiveRTT
**Description of a tool chain to evaluate Unidirectional Passive RTT measurement**

The paper:
"Passive Online RTT Estimation
for Flow-Aware Routers Using One-Way Traffic",  
Damiano Carra, Konstantin Avrachenkov, Sara Alouf,
Alberto Blanc, Philippe Nain, and Georg Post

http://www-sop.inria.fr/members/Philippe.Nain/PAPERS/PASSIVE-ONLINE-ESTIMATION/Passive-online-RTT-estimation.pdf

provides a method to estimate RTT from passive observations of a 
**single direction of a flow's transmission**.  Overview the method:
"the signal is the packet inter-arrival times of the flow at hand."
and computes the Lomb-Scargle Periodogram on a sliding window of 
the inter-arrival times of the flow, stepping by one as new packets arrive.

**Tools.md** contains an example of putting the various tools to work
on a Google QUIC stream. This is a partial tool-chain at present:
the sliding window and processing of the list of peak frequencies is not yet implemented.

Other results will be added as they become available, focusing on TCP since this was the original focus of passive measurements.
Analysis of each stream has been placed in a sub-directory (e.g., TCP1 is the first attempt with a TCP stream).
Also tried several Synthesised Periodic Streams with **Periodic** sampling and analyzed with Lomb-Scargle.
(Since Lomb-Scargle works with non-periodic sampling, analysis of an ideal stream should be a easier?)

**Latest Update:** An old pcap of a Flash HD stream produced a very strong peak
in the L-S Periodogram; this is the first case where a frequency component was
non-random/did not occur by chance. See the **TCP3** Directory.

