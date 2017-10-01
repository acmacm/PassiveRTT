# PassiveRTT
Description of a tool chain to evaluate Passive Round-Trip-Time measurement

The paper:
"Passive Online RTT Estimation
for Flow-Aware Routers Using One-Way Traffic",  
Damiano Carra, Konstantin Avrachenkov, Sara Alouf,
Alberto Blanc, Philippe Nain, and Georg Post

http://www-sop.inria.fr/members/Philippe.Nain/PAPERS/PASSIVE-ONLINE-ESTIMATION/Passive-online-RTT-estimation.pdf

provides a method to estimate RTT from passive observations of a 
single direction of a flow's transmission.  The methods use
"the signal is the packet inter-arrival time of the flow at hand."
and compute the Lomb-Scargle Periodogram on a sliding window of 
the inter-arrival times of the flow, stepping by one as new packets arrive.

**Tools.md** contains an example of putting the various tools to work
on a Google QUIC stream.

Other results will be added as they become available, focusing on TCP since this was the original focus of passive measurements.

Latest Update: Synthesised a Periodic Stream with periodic sampling and analyzed with Lomb-Scargle.
