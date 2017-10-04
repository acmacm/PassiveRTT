## This page summarizes observations and findings ##
(work-in-progress)
* It seems that Carra et al. took the noisy and low-confidence results of 
a statistical process and added hueristics and sliding-window averaging to
infer the fundamental frequency and RTT present in a unidirectional stream.

* (so far) None of the TCP streams analysed have a sufficient packet rate
such that the measured fundamental frequency or the multiples of the fundamental
are in the detectable range. See https://github.com/acmacm/PassiveRTT/blob/master/Freq_Range_and%20Pkt_Rate.md
