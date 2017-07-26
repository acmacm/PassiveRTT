# PassiveRTT
Description of one tool chain to evaluate Passive Round-Trip-Time measurement

The paper:
Passive Online RTT Estimation
for Flow-Aware Routers Using One-Way Traffic
Damiano Carra1,, Konstantin Avrachenkov2, Sara Alouf2,
Alberto Blanc2, Philippe Nain2, and Georg Post3
http://www-sop.inria.fr/members/Philippe.Nain/PAPERS/PASSIVE-ONLINE-ESTIMATION/Passive-online-RTT-estimation.pdf

provides a method to estimate RTT from passive observations of a 
single direction of a flow's transmission.  The methods operate on
"the signal is the packet inter-arrival time of the flow at hand."
and compute the Lomb-Sparkle Periodogram on a sliding window of 
the packet flow, stepping by one as new flows arrive.
