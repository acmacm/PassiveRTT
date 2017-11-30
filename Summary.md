## This page summarizes observations and findings ##
(work-in-progress)
* It seems that Carra et al. took the noisy and low-confidence results of 
a statistical process (as seen here, no RTT-related frquency has been detected
even after using very low alpha confidence) and added hueristics and sliding-window averaging to
infer the fundamental frequency and RTT present in a unidirectional stream.

* There appear to be several limitations on the streams that are applicable.
Streams with long RTT (~50ms) are more likely to be suitable (having a 
better match between packet rate and relatively low frequencies to detect).

* (so far) None of the TCP streams analysed have a sufficient packet rate
such that the measured fundamental frequency or the multiples of the fundamental
are in the detectable range. See https://github.com/acmacm/PassiveRTT/blob/master/Freq_Range_and%20Pkt_Rate.md

* "Ideal" interarrival time streams were simulated with uniform sampling
and period. The Lomb-Scargle Periodogram is surprisingly unable to detect
the fundamental frequency at 100 Hz, from the constant 10 ms packet spacing.

* The Carra et al. analysis of minimum and maximum frquecies that can be detected 
may not be applicable when the inter-arrival times are the signal 
being detected. Pulses with period T should result in a Dirac comb
in the frquency domain with spacing 1/T (the fundamental frequency
and multiples thereof).
