# Results and analysis

Source: `AFIT-IP-Over-Link16.pdf`, PDF pages 60-73.

Navigation: previous [Model implementation and verification](03-model-implementation-and-verification-pages-048-059.md) | [coverage index](README.md) | next [Conclusions and appendices](05-conclusions-and-appendices-pages-074-087.md)

> Transcription is normalized for search and reading order. Source-page anchors are authoritative locators; graphical fidelity is audited separately in `TABLES-AND-FIGURES.md`.

<a id="source-pdf-page-60"></a>

## Source PDF page 60

4-9 Link-16 network.  The IPSec areas of interest are Authentication Header (AH) and Encapsulating Security Payload (ESP) protocols and are explained in the next section.

### 4.3.1 Baseline Implementation.   The implementation of the Link-16 model used as a

baseline includes the parameter settings outlined in Table 4.2.  An external model was used to communicate with the OPNET model in order to simulate IP traffic downloaded to a JTIDS host terminal.

### Table 4.2:  Implementation Workload Parameters

- `Workload Parameter Setting`
- `Offered Load 30, 60, or 90 %`
- `IP Message Length 2160, 4320, 6480 bytes`
- `plus 28 bytes for AH`
- `and 54 bytes for AH and ESP`
- `JTIDS Message Length 450 bits`
- `Type of Message J-series type`
- `Packing Structure Packed-2 (six words per time slot)`
- `Security Level AH, ESP, or Both`
- `Network Participation Group (NPG) NPG-29`


### 4.3.2 Baseline Results (ETE Delay).   The ETE is measured in seconds and is defined to

be the elapsed time from when a packet arrives at the source node’s routing layer to when the packet is received by the routing layer of the destination node.  Figure 4.5 shows the ETE mean delay for offered loads of 30, 60, and 90 %.  For the 30 % load, 2,160 bytes (17,280 bits) were

<a id="source-pdf-page-61"></a>

## Source PDF page 61

4-10 generated every second for an average ETE delay of 0.256 seconds.  The ideal ETE mean delay should be 17,280 bits/57,600 bps = 0.300 seconds. The 60 % offered load (4320 bytes) resulted in an average ETE of 0.652 seconds.  The 90 % workload (6,480 bytes) resulted in an average ETE of 1.354 seconds.  Additional simulations were run using 8,000 byte IP packets at which point the ETE average was 2.506.  As expected, an increase in the number of bytes per second beyond the 90 % offered load caused the buffer to backup, and required several hours for the OPNET simulations to reach completion.

End-To-End Delay (Baseline) 30 60 90 0.000 0.200 0.400 0.600 0.800 1.000 1.200 1.400 1.600 Offered Load (% ) ETE Delay (seconds)

### Figure 4.5:  Baseline End-To-End Delay

### 4.3.3  Baseline Results (Effective Throughput).  Figure 4.6 shows the effective throughput for

nominally offered loads of 30, 60, and 90 %.  Effective throughput was calculated by using the total number of bits offered at the host terminal divided by the total simulation time.  The total

<a id="source-pdf-page-62"></a>

## Source PDF page 62

4-11 number of bits only includes the data bits, and does not include any overhead bits.  The actual offered load varied slightly from the nominally offered load.  For instance, the 30 % offered load should present 17,280 bits per second (bps) (57,600 × 0.30) to the host terminal.  However, as mentioned above, the exponential distribution is used to calculate the time each IP packet is presented to the host terminal, but the actual calculated value for how often packets are presented may differ from the nominal valued by as much as several milliseconds.  As was the case in the

### 30 % offered load, the actual distribution time was 17,280 bits per 1.02 seconds.  Therefore the

actual offered load was 16,941 (17,280/1.02).  The measured effective throughput of 16,949 bps is slightly different due to rounding errors in the Link-16 model.

Effective Throughput (Baseline) 30 60 90 0 10000 20000 30000 40000 50000 60000 Offered Load (% ) Throughput (bps)

### Figure 4.6:  Effective Throughput – Baseline

<a id="source-pdf-page-63"></a>

## Source PDF page 63

4-12 At the 60 % nominally offered load level the Link-16 network is only receiving 34,491 bps and is not fully utilized and there is less chance of messages backing up in the buffer.  However, at the 90 % workload level, the host terminal is receiving 51,798 bps, which is near its maximum capacity and messages back up in the buffer more frequently, thereby negatively impacting the effective throughput and thus explains the super-linear growth.

### 4.4 JTIDS Security Feature Additions (IPSec)

Security and privacy in IPSec is integrated into IPv6 and provided through the AH and ESP protocols.

### 4.4.1 Authentication Header (AH) Protocol – End-To-End Delay.   The addition of the

AH to the IPv6 baseline involves using the keyed MD-5 hash function, or any one way hashing algorithm to compute a 128-bit digest of the message to be transmitted [CDK01].  In this effort, the MD-5 has function is considered for calculating additional overhead bits.  The 128 bits returned from the hash function is appended to the authentication data contained in the AH.  As mentioned in Chapter Two, the AH adds on 12 bytes from the first five fields of the AH and another 16 bytes (128 bits) of authentication data for a total of 28 additional bytes added to the IP packet.  Therefore, even though this process requires extensive computer preprocessing, it only adds 28 bytes of overhead to the baseline IP packet, thus effecting network latency and ETE delay very minimally as shown in Figure 4.7 [Kae99].

### 4.4.2 Authentication Header (AH) Protocol -- Effective Throughput.  Figure 4.8 shows

the effective throughput for offered loads of 30, 60, and 90 %.  Similar to the ETE delay, the effective throughput is minimally impacted due to the addition of the AH protocol.

<a id="source-pdf-page-64"></a>

## Source PDF page 64

4-13 End-To-End Delay (Baseline & AH) 0.000 0.200 0.400 0.600 0.800 1.000 1.200 1.400 1.600 Offered Load (%) ETE Delay (seconds) Baseline 0.256 0.652 1.354

### AH 0.257 0.658 1.369

### 30 60 90

### Figure 4.7:  Baseline and Authentication Header -- End-To-End Delay

Effective Throughput (Baseline & AH) 0 10000 20000 30000 40000 50000 60000 Offered Load (%) Throughput (bps) Baseline 16949 34491 51798

### AH 17372 34906 51981

### 30 60 90

### Figure 4.8:  Baseline and Authentication Header -- Effective Throughput

<a id="source-pdf-page-65"></a>

## Source PDF page 65

4-14

### 4.4.3 Encapsulating Security Payload (ESP) Protocol – Effective Throughput.  The

addition of the ESP header to the IPv6 baseline uses an encryption algorithm to secure the payload.  A common encryption algorithm used is triple DES.  Triple DES uses a 112-bit key to encrypt the payload data, therefore adding 14 bytes onto the payload data.  As described in Chapter Two, the ESP protocol adds a minimum of 12 bytes and up to an additional 255 bytes (if required by the encryption algorithm).  A total of 26 bytes will be used as additional overhead data for the ESP protocol. Since the additional 28 bytes of overhead from the AH had such a small effect on the overall ETE delay, it is reasonable that simulations ran using 26 bytes of overhead would be statistically equivalent and therefore, in the economy of time, a full set of simulations was not conducted for the ESP extension, but instead a few simulations were run to verify that results were not significantly different from the simulations run for the AH extension.  The overall effect on throughput was also minimal.

### 4.4.4 Baseline, Authentication Header, and Encapsulating Security Payload -- ETE

Delay.  ESP and AH headers can be combined in a variety of modes.  For these simulations, an average for the combination of the ESP and AH headers was used which added an additional 54 (28 + 26) bytes of overhead.  As can be seen in Figure 4.9, the increase in overhead has a minimal effect on the average ETE delay.  The 30 % offered load increases from 0.256 for the baseline, to 0.470 for the 60 % offered load, and 1.060 for the 90 % offered load.

<a id="source-pdf-page-66"></a>

## Source PDF page 66

4-15 End-To-End Delay (Baseline,

### AH & ESP)

0.000 0.200 0.400 0.600 0.800 1.000 1.200 1.400 1.600 Offered Load (%) ETE Delay (seconds) Baseline 0.256 0.652 1.354

### AH 0.257 0.658 1.369

### AH & ESP 0.259 0.663 1.388

### 30 60 90

### Figure 4.9:  Baseline, Authentication, and Encapsulating Security Payload

End-to-End Delay

### 4.4.5 Baseline, Authentication Header, and Encapsulating Security PayloadProtocols –

Effective Throughput.  Figure 4.10 shows the effective throughput for offered loads of 30, 60, and

### 90 %.  The throughput for the 30 % workload increases slightly from 16,949 bps for the baseline,

to 17,372 bps for AH, and again increases slightly to 17,582 bps for the combination of AH and ESP.  The slight increase from the AH configuration to the AH and ESP combined configuration shows that the difference is statistically insignificant as can be seen in Table 4.3 because the F- Computed values are less then the F-Table values.  The 60 and 90 % workloads follow a similar trend.

<a id="source-pdf-page-67"></a>

## Source PDF page 67

4-16 Effective Throughput (Baseline,

### AH, & ESP)

0 10000 20000 30000 40000 50000 60000 Offered Load (%) Throughput (bps) Baseline 16949 34491 51798

### AH 17372 34906 51981

### AH & ESP 17582 35362 52201

### 30 60 90

### Figure 4.10:  Baseline, Authentication, and Encapsulating Security Payload

Effective Throughput

### 4.5 Result Analysis

The next sections present an analysis comparing the three overhead variations (baseline, AH, AH and ESP combined) to the offered load variations (30, 60, 90 % offered load).  All the ANOVA tables and derivation formulas are also displayed together in Appendices A through C.

### 4.5.1 End-To-End (ETE)Delay Analysis.   As seen in Figure 4-9 above, the ETE delay

increases as packet size (offered load) increases.  The variation shown in Table 4.3 shows that

### 99.94 % of the variation was due to the change in workload.  Only 0.02 % of the variation was due

to increased overhead.  The variation due to overhead-workload interaction was 0.01 % and variation due to error was 0.02 %.  Because the F-Computed value for offered load is significantly larger than the F-Table value, this confirms that offered load has a significant impact in Link-16 network performance.  The F-Computed value for the overhead variation is slightly larger than the

<a id="source-pdf-page-68"></a>

## Source PDF page 68

4-17 F-Table value; therefore, it has a minimal effect on the network performance.  Because the F-Computed value for interaction is less than the F-Table value, the overhead-offered load interaction does not have an effect on the network performance.

### Table 4.3:  End-to-End (ETE) Delay Allocation of Variation (ANOVA)


### 4.5.2 Effective Throughput Analysis.  The effective throughput, as seen in Figure 4.10

above, is 98 % (16949 bps/17280 bps) of the maximum effective throughput at the 30 % offered load level.  At the 60 % offered load level the throughput percentage is 99.8 % (34,491 bps/34,560 bps), and at the 90 % offered load level the throughput percentage is 99.9 % (51,798 bps/51,840 bps).  As previously mentioned, the effective throughput will at times be less than, or even greater than, the ideal throughput due to the error in the exponential distribution of the IP packets not being delivered, on average, exactly one second apart. The variation shown in Table 4-4 shows that 99.83 % of the variation is due to change in the offered load.  The change in overhead effects 0.03 % of variation, and 0.13 % of the variation is due to error.  The F-Computed valued of 13544.72 for the offered load is well above the F-Table value, verifying it has a significant impact on Link-16 network performance.  The overhead and interaction variations have no effect on Link-16 performance as verified by smaller F-Computed values as compared to the F-Table values.

### Table A.6:  End-To-End Delay Allocation of Variation

- `Variation Variation % DOF Mean Square F-Computed F-Table`
### SSY 35.6400   45

### SSO 26.0969   1

SSA (Overhead Var): 0.0019 0.0203 2 0.0010 15.592 6.940 SSB (Offered Load Var): 9.5376 99.9427 2 4.7688 76652.265 6.940 SSAB (Interaction): 0.0013 0.0135 4 0.0003 5.181 6.940 SSE (Error Var): 0.0022 0.0235 36 0.0001

### SST 9.5431   44 0.2169

<a id="source-pdf-page-69"></a>

## Source PDF page 69

4-18

### Table 4.4:  Effective Throughput Allocation of Variation (ANOVA)

### Table B.6:  Effective Throughput Allocation of Variation

- `Variation Variation % DOF Mean Square F-Computed F-Table`
### SSY 63345625271   45

### SSO 54302809601   1

SSA (Overhead Var): 3032934 0.03 2 1516467 4.55 6.94 SSB (Offered Load Var): 9027475902 99.83 2 4513737951 13544.72 6.94 SSAB (Interaction): 309939 0.00 4 77485 0.23 6.94 SSE (Error Var): 11996896 0.13 36 333247

### SST 9042815670   44 205518538

### 4.5.3 Raw Throughput Analysis.  Figure 4.11 shows the raw throughput for the all three

offered loads and all three overhead configurations.  The raw throughput is actually greater than the number of data bits offered at the host terminal because of the overhead bits added to the data load before the JTIDS terminal transmits the JTIDS word. Raw Throughput (Baseline,

### AH, & ESP)

0 10000 20000 30000 40000 50000 60000 Offered Load (%) Throughput (bps) Baseline 18449 37061 55945

### AH 18623 37437 56281

### AH & ESP 18860 37652 56488

### 30 60 90

### Figure 4.11:  Baseline, Authentication Header, and Encapsulating

Security Payload Raw Throughput

<a id="source-pdf-page-70"></a>

## Source PDF page 70

4-19

### 4.6  Confidence Interval(CI) Analysis

CI analysis can be used to determine if a meas ured value is significantly different from zero. The analysis is performed by checking the CI interval to see if it includes the value zero.  If the CI includes zero, then the measured values are not significantly different than zero.   Appendix A (Tables A.7 and A.8) and Appendix B (Tables B.7 and B.8) show the CI for the ETE delay and throughput offered load and overhead effects.  The CI analysis shows that the results from the varied offered loads are significant, but the results from the varied security levels are not significant.

### 4.7 Summary

This chapter described th e verification of the OPNET Link-16 model and the resultant data from that model.  Next, the implementation and results of the IP baseline model used for this research were explained.  Then a performance summary of the overhead and workload variations was described.  Finally an analysis of the results and data variations was explained.

<a id="source-pdf-page-71"></a>

## Source PDF page 71

5-1

V.  Conclusions and Future Work

### 5.1 Overview

The JBI concept is within reach of becoming reality now that information technologies, in particular Internet technologies, are reaching a quality-of-service level that provides sufficient bandwidth for fast-paced war-fighting requirements.  As various communication sub-systems are pieced together to form a network-centric JBI, Information Assurance becomes a chief concern. IPSec provides another security layer in the overall JBI security scheme.  The research goal was to determine the feasibility of passing IP messages and IPSec messages over a Link-16 network. Sub-goals included performance analysis by comparing the effect that additional overhead from the IPSec security protocols has on a Link-16 network.  In addition, various workloads were placed on the network to see how overall ETE delay and throughput are affected.

### 5.2 Conclusions

Since the IPSec security pr otocols add minimal overhead to the IP packet, and even though the Link-16 network is relatively slow (57.6 kbps) compared to most Internet pipelines, it has minimal effect on Link-16 ETE delay and throughput.  Similar to varying the security levels, varying the offered load has a minimal effect on effective throughput.  At the 60 % offered load level, effective throughput is 99.8 % of the maximum capacity.  At the 90 % offered load level, effective throughput is 99.9 % of maximum capacity.  Here we see, that an offered load through the 90 % level does not negatively impact the performance of the Link-16 network.  However, the Link-16 data rates are still not adequate to for transferring large data files that typically traverse the Internet.  Some research has been done, suggesting the Link-16 network can operate up to 1.0 Mbps.  An effective throughput near the 1.0 Mbps level would be adequate to process large imagery files which typically range in size from 2 to 5 megabytes.  At an average effective

<a id="source-pdf-page-72"></a>

## Source PDF page 72

5-2

throughput rate of 1.0 Mbps, a typical imagery file of 3 to 5 megabytes can take 3 to 5 seconds to download.

### 5.3 Contributions

This research demonstrates that although the IPSec security protocols contribute minimal to IP packet overhead, the main problem is that the Link-16 network is a legacy system that is far too slow to transfer large size data files.  The AH and ESP security protocols can be added to the IPv6 packets with minimal effect on ETE delay and effective throughput.  However, as offered load increases beyond 6.5 kbps, throughput begins to degrade rapidly.  Therefore, the Link-16 network can transmit IP packets provided the average bytes per second rate doesn’t exceed 6.5 kbps.  The addition of IPSec protocols has minimal impact on the Link-16 network and does not degrade its performance.

### 5.4 Future Work

Since the USAF Tactical Datalink Roadmap has determined that Link-16 will be around for long term use, future work and research will always be useful to discover methods of improving the Link-16 data rate, such as software modifications or compression techniques.  Further research can be conducted in this area by adjusting the Link-16 data rates to current maximum capacity of 238 kbps to determine effective throughput at that rate.  Hardware modifications can also be made which effect the carrier modulation to increase the number of words in the packing structure. It should be noted that the OPNET  Link-16 model used in this research was one of the early versions of several planned iterations, and some features such as relay and net stacking, are

<a id="source-pdf-page-73"></a>

## Source PDF page 73

5-3

not part of the current model set.  Possible future research may include the use of multiple nets to simultaneously transmit data to increase throughput.  It would be beneficial to validate the OPNET Link-16 model used in this research work.  However, real-time data is needed to validate results obtains from the Link-16 model.

Navigation: previous [Model implementation and verification](03-model-implementation-and-verification-pages-048-059.md) | [coverage index](README.md) | next [Conclusions and appendices](05-conclusions-and-appendices-pages-074-087.md)
