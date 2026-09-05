# Model implementation and verification

Source: `AFIT-IP-Over-Link16.pdf`, PDF pages 48-59.

Navigation: previous [Research methodology](02-research-methodology-pages-035-047.md) | [coverage index](README.md) | next [Results and analysis](04-results-and-analysis-pages-060-073.md)

> Transcription is normalized for search and reading order. Source-page anchors are authoritative locators; graphical fidelity is audited separately in `TABLES-AND-FIGURES.md`.

<a id="source-pdf-page-48"></a>

## Source PDF page 48

3-5

2. End-to-End (ETE) delay – ETE is measured in seconds and is defined to be the elapsed time from when a packet arrives at the source node’s routing layer to when the packet is received by the routing layer of the destination node. 3. Data transfer – In Link-16, either 3, 6, or 12 Link-16 words can be transmitted in a

### 7.8125 msec time slot depending on whether the Standard, Packed-2, or Packed-4 data

packing structure is used.  For instance if the Packed-2 packing structure is used, then

### 420 (six 70-bit words) data bits are transferred in 1/128 second to give an instantaneous

rate of 52.5 kbps.

### 3.5 Parameters.

Within the system boundaries, the system and workload parameters that affect performance are defined below.

### 3.5.1 System Parameters.

1. JTIDS Transmission/Reception Equipment – This equipment is the communications component of Link-16.   It encompasses the Class 2 terminal software, hardware, RF equipment, and the high-capacity, secure anti-jam waveform that they generate [Nor01]. 2. JBI Applications – These include the JBI server, browser, and collaboration server. 3. JBI Data Resources – These include Air Tasking Orders, Imagery, etc. 4. Network Layers – TCP, IP, physical layer. 5. RT CORBA Middleware – Intermediary for passing objects between TCP layer and JBI applications.

<a id="source-pdf-page-49"></a>

## Source PDF page 49

3-6

### 3.5.2 Workload Parameters.

1. Data rate – The tactical data rate range for Link-16 is 28.80 kbps to 115.20 kbps. 2. Voice and data workload – A trace of traffic measured on a real-time system will be used to compare against simulated results.  Data includes tactical data information such as navigation waypoints, target assignment, target tracking, release points, munitions inventory, and sensor data. 3. IPv6 versus IPSec – IPv6 provides the channel for transferring IP packets. IPSec provides the additional security measures required for multi-level security within the F-15E notional architecture. 4. Operating System (OS) – Proprietary real-time OS versus COTS. 5. Packing structure – Either Standard, Packed-2, or Packed-4 data packing structure is used.

### 3.6 Factors.

The following factors and their corresponding levels were chosen as the most significant for this research.

### 3.6.1 Data rate.

1. Standard Tactical Rate (with parity) – 28.8 kbps 2. Packed-2 Tactical Rate (with parity) – 57.6 kbps 3. Packed-4 Tactical Rate (with parity) – 115.2 kbps

### 3.6.2 Internet Protocol.

1. IPv6 – This provides a baseline performance analysis of IP packets over Link-16.

<a id="source-pdf-page-50"></a>

## Source PDF page 50

3-7

2. IPSec – Additional overhead from IPSec is considered to determine if the Link-16 network can handle the increased workload.  The two protocols of concern are the Authentication Header protocol and the Encapsulated Security Payload protocol

### 3.7 Evaluation Technique.

An OPNET  Link-16 model developed by the Navy Space and Naval Warfare (SPAWAR) Systems Command office is used to evaluate this performance analysis.  Some modifications to the model were made by the Air Force Research Lab (AFRL) Sensors Directorate.  An external mission model was used with the OPNET Link-16 model to input mission data such as message type, message ID, message size, source, and destination.

### 3.8 Workload.

Workload parameters are based on the Link-16 OPNET  model as listed in Table 3.1:

### Table 3.1:  Workload Parameters

- `Workload Parameter Setting`
- `Data Rate 57.6 kbps`
- `Offered Load 30, 60, 90 %`
- `Message Length 450 bits`
- `Type of Message J-series type`
- `Packing Structure Packed-2 (six words per time slot)`
- `Security Level AH, ESP, or both`
- `Network Participation Group (NPG) Va ries according to mission function`

<a id="source-pdf-page-51"></a>

## Source PDF page 51

3-8

### 3.9 Experimental Design.

This experimental design consists of specify ing the number of experiments, the factor level combinations for each experiment, and the number of replications of each experiment.  Since this experiment included one factor with three levels and another factor with three levels, there were

### 3 × 3 = 9 experiments.  Five replications were conducted for a total of 5 × 9 = 45 simulations.

The 30%, 60%, and 90% offered load levels were chosen to show the effects these loads have on the Link-16 network when its lightly loaded, moderately loaded, and heavily loaded.  Although three different security levels were chosen (AH, ESP, and a combination of AH and ESP), it was not necessary to repeat a full set of simulations for the ESP level since it only adds two more bytes of overhead to the IP packet and the difference in the simulation results was negligible. Therefore, a few simulations were run to verify that the difference was negligible when adding

### 26 bytes of overhead from the AH extension versus adding 28 bytes of overhead from the ESP

extension.

### 3.10 Summary.

This chapter described the methodology to be used for the performance analysis of implementing IP packets over the Link-16 network.  It discussed the thesis goal, approach to be used, system boundaries and services, performance metrics, parameters, factors, and workload.

<a id="source-pdf-page-52"></a>

## Source PDF page 52

4-1

### IV.  IMPLEMENTATION AND ANALYSIS

### 4.1 Overview

This chapter provides research results and analysis.  The verification and validation of the OPNET implementation of the Link-16 model is described and a description of the baseline IPv6 over Link-16 model is presented.  For comparison to the baseline, security features are added to IPv6 to further test the Link-16 network’s capacity to handle increased demand.  Finally, this chapter provides an overview of results and overall analysis.

### 4.2  Link-16 Verification and Validation

OPNET is a Commercial Off-The-Shelf (COTS) program that provides an environment for network simulations.  It is widely used throughout the DoD for network modeling and provides support for detailed radio modeling, which is a key requirement for JTIDS.  OPNET’s network traffic is generated stochastically, using probability density functions.  Therefore, generated data packets do not contain information, but are just tokens that represent data of a given size that transverse a given network.  This is sufficient for this study, since we are only interested in how overhead and data load affect overall performance, the particular information contained in packets is irrelevant.  The model need is based on a model provided by the AFRL Sensors Directorate and uses OPNET’s radio propagation model, referred to as the Radio Transceiver Pipeline, and simulates the protocol message packet and models a JTIDS terminal’s transmissions on a time slot basis.  Figure 4.1 shows the communications system consisting of an external mission model, and the JTIDS hosts and JTIDS terminals used in the Link-16 model.  The mission model is used to communicate with the Link-16 model and provides the offered load and mission data to the Link-

### 16 network.

<a id="source-pdf-page-53"></a>

## Source PDF page 53

4-2

### Figure 4.1:  Mission Model – Link-16 Communication System

This OPNET model was configured using the Link-16, Packed-2 packet format, which contains two 3-word blocks of 225 bits each for a total of 450 bits.  For example, one particular test sent 2160 bytes (17,280 bits) from a Narrow Area Search Munitions (NASM) terminal to the Airborne Command and Control Center (ABCCC) terminal.  The 17,280 bits were divided up and inserted into 39 (17,280/450 = 38.4) JTIDS packets. The JTIDS transmitter terminal adds 35 bits of overhead to the 6-word JTIDS packet for a total of 485 bits.  Average data rate is calculated based on 450 bits transmitted every 1/128 th of a second, therefore 450 × 128 = 57,600 bps.  The terminal model supports transmission and reception of free-text format messages, the format used to transmit IP packet data through the Link-16 network.  The terminal model is a simplified representation of a JTIDS terminal that enqueues incoming TADIL-J messages from the host into available buffers, and sends them out in the correct timeslot.  The terminal model uses the OPNET Radio Transceiver Pipeline to calculate the effects of Radio Frequency (RF) propagation.  The pipeline stages used are modified versions of the default radio pipeline stages provided by OPNET.  The modifications allow for Mission Model

<a id="source-pdf-page-54"></a>

## Source PDF page 54

4-3

improved bit error rate calculation and add support for animation of the radio links.  The host-toterminal interface is represented as a duplex point-to-point link with zero delay.  Although it is not representative of the 1553 bus, the latency is factored into the Link-16 model. JTIDS scenarios require the terminal nodes and host computer pairs to be co-located in subnets for proper spatial movement.  This organization is imposed by OPNET because node models connected by physical links (as the terminal and host are by the dls_serial link) cannot be mobile. Figure 4.2 shows the OPNET  host node model used to generate J-series messages, which are sent to the JTIDS terminal shown in Figure 4.3.

### Figure 4.2: dls_JTIDS_host  Node Model

<a id="source-pdf-page-55"></a>

## Source PDF page 55

4-4

### Figure 4.3:  dls_radio_JTIDS Node Model

This J-series message packet format represents a single TADIL-J message consisting of six 75-bit words.  The JTIDS terminal accepts these packets through the point-to-point serial interface connecting it to the host computer.  The JTIDS terminal encapsulates one or more TADIL-J messages that are sent in the time slot, along with the message headers.  The number of messages encapsulated is dependent on the packing type and the length of each TADIL-J message, which in the case of this model uses the Packed-2 format with a message length of 450 bits. Validation was not accomplished on this model because no real-time data could be obtained to validate the results against.

<a id="source-pdf-page-56"></a>

## Source PDF page 56

4-5

### 4.2.1  Verification Implementation.   The basic implementation of the JTIDS model used for

verification included the parameter settings in Table 4.1.  Performance metrics include the End-to- End (ETE) delay and throughput.

### Table 4.1:  Verification Workload Parameters

- `Workload Parameter Setting`
- `Data Rate 57.6 kbps`
- `Offered Load 30 % (2,160 bytes or 17,280 bits)`
- `Message Length 450 bits`
- `Type of Message J-series type`
- `Packing Structure Packed-2 (six words per time slot)`
- `Security Level None`
- `Network Participation Group (NPG) NPG-29`


### 4.2.2  Sample size for determining mean.   To estimate the system’s mean performance with

an accuracy of ± r % at a confidence level of 100 × (1-α )%, the number of observations n required to achieve this goal is can be determined from Eq. (4-1) [Jai91]: Confidence Interval = n szx ±  (4-1) Where z is the normal variate of the desired confidence level.  The desired accuracy of r % indicates that the confidence interval should be (x (1-r/100), x (1+r/100)).   Using this and Eq. (4-1) and solving for n yields Eq. (4-2):

<a id="source-pdf-page-57"></a>

## Source PDF page 57

4-6

2

### 100 

   = xr zsn (4-2) With an accuracy of 5 % and based on preliminary tests, each set of simulations requires runs.  Refer to Appendix D for calculations used to determine the required number of simulations.

### 4.2.3 Verification Results.   The Link-16 OPNET model was verified by presenting data at

the host terminal and ensuring the data went across the host terminal to the sending JTIDS transmitter terminal, then to the receiving JTIDS terminal, and finally to the receiving host terminal.  During this process, the number of bytes received at the receiving JTIDS terminal was compared against the number of bytes sent at the sending JTIDS terminal to ensure that they were equal. The ETE delay was measured and compared against the ideal ETE delay.  For instance, when sending 17,280 bits through the network with the data rate set at 57,600 bits per second, the ETE delay should be 17,280 bits/57,600 bps = 0.300.  To verify the ETE delay, a MATLAB program (cfi, Appendix E) was used to create exponentially distributed IP messages at a frequency of 17,280 bps (2,160 bytes per second) for the baseline model representing a 30 % offered load. The MATLAB software program was used to create a script file that was input into an external “mission model”.  The mission model and the OPNET Link-16 model make up a distributed system in which the mission model uses the script file to input mission data to the OPNET Link-16 model.  It includes the following types of data:  type of message sent, time message was transmitted, message ID, source ID, destination ID, and message quality. Originally, messages were sent based on a deterministic distribution, or in other words the 5≤n

<a id="source-pdf-page-58"></a>

## Source PDF page 58

4-7

messages were sent every second with exactly one second between transmittals.  However, this method didn’t provide a realistic model of how traffic arrives at a network node and multiple runs generated the same results each time.  Therefore, an exponential distribution was created in order to model the bursty nature of network traffic arriving at a node. Through several simulations it was determined the OPNET model reached steady-state after

### 3000 samples were run, as shown in Figure 4.4.  The average ETE delay was just over 0.250

seconds.  Although the average ETE delay is typically expected to be equal to, or greater than, the ideal ETE delay, the reason it is less can be explained by either one of, or a combination of the following:

### Figure 4.4:  Average ETE Delay (2160 Byte Packet, 3000 Samples)

<a id="source-pdf-page-59"></a>

## Source PDF page 59

4-8 • The Radio Frequency (RF) data rate of the Link-16 model was set at 97.0 kbps, instead of 57.6 kbps to better approximate an effective throughput of 57.6 kbps, because the real terminal sends at a much higher rate to leave time within the time slot for propagation guard and jitter.  The total time required to transmit the header and data portion of the timeslot in the Packed-2 Double-Pulse structure is 5.772 ms.  Because the model is generic in the sense that it can support, Standard Double Pulse, Packed-2 Single Pulse, Packed-2 Double Pulse, or Packed-4 Double Pulse message packing, it uses an average time to model jitter and propagation.  Therefore, depending on which type of data pulse is used, there will be some built in error. • Although the exponential distribution was set up to send an IP packet to the host terminal every second, the actual calculated time between packets sent varies from 0.97 seconds to 1.03 seconds, causing the ETE delay and throughput to be offset by various amounts. The OPNET model was also checked to ensure it was using the proper packing configuration (Packed-2) and if it was adding the additional 35 bits of overhead to each 450-bit word. Messages were traced and verified that a total of 485 bits were being transmitted through the JTIDS terminals.  Through several simulations and debugging methods, the above mentioned verification tests confirmed that the OPNET model was operating correctly.

### 4.3 JTIDS Baseline.

This research is studying the effects of IPv6 packets over the JTIDS network as well as the effect IPSec, with its additional security overhead bits, has on the latency and throughput of the

Navigation: previous [Research methodology](02-research-methodology-pages-035-047.md) | [coverage index](README.md) | next [Results and analysis](04-results-and-analysis-pages-060-073.md)
