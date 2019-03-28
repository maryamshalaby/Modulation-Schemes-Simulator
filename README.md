# Modulation Schemes Simulator
This repo contains the model files of multiple digital modulation schemes simulated using Simulink, as well as instructions to replicate the models, Scatter plots and BER performance figures.
The channel used in simulation is an Additive White Gaussian Noise Channel (AWGN). Input to the channel is simulated both in unfiltered form, and Raised Cosine (RC) shaped form. 
## Initial Set up
1. Open Matlab
2. Through Matlab commapnd prompt run *Simulink*
3. Add a new blank model
4. Proceed to add needed blocks as will be shown below
## Modulation Schemes
* Binary Phase-shift Keying (**BPSK**)
* Quadrature Phase-Shift Keying (**QPSK**)
* Frequecny-Shift Keying (**FSK**) 
* Quadrature Amplitude Modulation (**QAM**)
### BPSK Modulation
In BPSK Modulation, the binary signal is modulated by changing the *phase* of a fixed frequency carrier signal. Two symbols are modulated in the following diagram, thus two phases exist in the system, 0 and 180, as will be shown in the *Constellation Diagram*.
#### Function Blocks
The following figure shows the function blocks used. 
![BPSK Model](https://github.com/maryamshalaby/Modulation-Schemes-Simulator/blob/master/BPSK/BPSK%20Figures/BPSKmodel.PNG)
#### Function Blocks Parameter Set up
##### Random Integer Generator:
![Integer Generator](https://github.com/maryamshalaby/Modulation-Schemes-Simulator/blob/master/BPSK/BPSK%20Figures/Int-Gen.PNG)
* M-ary Number: set to 2, as in binary input
* Initial Seed: program default used for randomness
* Sample time: 1 second per sample
* Samples per frame: number of samples tested per frame is set to 100
##### BPSK Modulator Baseband:
Default paramters used.
##### AWGN Channel:
![AWGN Channel](https://github.com/maryamshalaby/Modulation-Schemes-Simulator/blob/master/BPSK/BPSK%20Figures/channel.PNG)
* Initial Seed: program default used for randomness
* Mode: set to SNR as it will be the basis of BER analysis
--**Note**: EbNo is a workspace variable, will be used for BER analysis, intially set to 10 db, and would need to be defined prior to         running.--
* Number of Bits per symbol: 1, again, Binary
* Signal power: program default used
* Symbol period: set to match random integer generator
##### BPSK Demodulator Baseband:
Default paramters used.
##### Error Rate Calculation:
Default paramters used.
#### Raised Cosine Set up
![BPSKRC Model](https://github.com/maryamshalaby/Modulation-Schemes-Simulator/blob/master/BPSK/BPSK%20Figures/BPSKRCmodel.PNG)
##### Raised Cosine Transmit Filter:
Default parameters used, Filter span in symbols is double the group delay, will be used in error rate calculation block.
##### Raised Cosine Recieve Filter:
Default parameters used, Decimation factor must march input samples correctly to downsample the signal to match number of samples generate from modulator.
#### Constellation Diagarams:
**Note**: EbNo set in the plotting of constellation diagrams is 10 db.
##### Without RC

<p align="center"> <img src="/BPSK/BPSK Figures/Channel in.PNG" height="400" width="400"> <img src="/BPSK/BPSK Figures/Channel out.PNG" height="400" width="400"></p>

As seen in the *channel in* constellation diagram, the input symbols are modulated into two phases, 0 and 180, thus  the two yellow dots. As for the *channel out* diagram, the effect of noise is apparant as it distorted the modulated carrier phases.
##### With RC

<p align="center"><img src="/BPSK/BPSK Figures/RC in.PNG" height="400" width="400"> <img src="/BPSK/BPSK Figures/RC out.PNG"height="400" width="400"></p>

#### BER Analysis:
#### Set up:
1. Run BER tool by typing *bertool* into matlab command prompt
2. Under Theoretical tab, choose range (our case is -10:10), choose modulation technique and plot
3. Under Monte Carlo tab, choose range, load file and state variable name. (Variable is added through simout block as shown, could also just output error rate calculation to workspace) 
4. Run
#### Result:
Figure shows BER analysis of both without RC and with RC models shown above
![BER analysis](https://github.com/maryamshalaby/Modulation-Schemes-Simulator/blob/master/BPSK/BPSK%20Figures/BER.PNG)
It is apparent, that the RC transmitter and reciever introduced a higher error rate, that is because, intitally the model ha no ISI (inter symbol interference) to begin with, which is what the RC was designed to tackle. Its intro duction into the system introduced higher error due to the approximate nature of the RC filter in frequency domain.

--------------------------------------------------------------------------------
### QPSK Modulation
In BPSK Modulation, the binary signal is modulated by changing the *phase* of a fixed frequency carrier signal. Two symbols are modulated in the following diagram, thus two phases exist in the system, 0 and 180, as will be shown in the *Constellation Diagram*.
#### Function Blocks
The following figure shows the function blocks used. 
![BPSK Model](https://github.com/maryamshalaby/Modulation-Schemes-Simulator/blob/master/BPSK/BPSK%20Figures/BPSKmodel.PNG)
#### Function Blocks Parameter Set up
##### Random Integer Generator:
![Integer Generator](https://github.com/maryamshalaby/Modulation-Schemes-Simulator/blob/master/BPSK/BPSK%20Figures/Int-Gen.PNG)
* M-ary Number: set to 2, as in binary input
* Initial Seed: program default used for randomness
* Sample time: 1 second per sample
* Samples per frame: number of samples tested per frame is set to 100
##### BPSK Modulator Baseband:
Default paramters used.
##### AWGN Channel:
![AWGN Channel](https://github.com/maryamshalaby/Modulation-Schemes-Simulator/blob/master/BPSK/BPSK%20Figures/channel.PNG)
* Initial Seed: program default used for randomness
* Mode: set to SNR as it will be the basis of BER analysis
--**Note**: EbNo is a workspace variable, will be used for BER analysis, intially set to 10 db, and would need to be defined prior to         running.--
* Number of Bits per symbol: 1, again, Binary
* Signal power: program default used
* Symbol period: set to match random integer generator
##### BPSK Demodulator Baseband:
Default paramters used.
##### Error Rate Calculation:
Default paramters used.
#### Raised Cosine Set up
![BPSKRC Model](https://github.com/maryamshalaby/Modulation-Schemes-Simulator/blob/master/BPSK/BPSK%20Figures/BPSKRCmodel.PNG)
##### Raised Cosine Transmit Filter:
Default parameters used, Filter span in symbols is double the group delay, will be used in error rate calculation block.
##### Raised Cosine Recieve Filter:
Default parameters used, Decimation factor must march input samples correctly to downsample the signal to match number of samples generate from modulator.
#### Constellation Diagarams:
**Note**: EbNo set in the plotting of constellation diagrams is 10 db.
##### Without RC

<p align="center"> <img src="/BPSK/BPSK Figures/Channel in.PNG" height="400" width="400"> <img src="/BPSK/BPSK Figures/Channel out.PNG" height="400" width="400"></p>

As seen in the *channel in* constellation diagram, the input symbols are modulated into two phases, 0 and 180, thus  the two yellow dots. As for the *channel out* diagram, the effect of noise is apparant as it distorted the modulated carrier phases.
##### With RC

<p align="center"><img src="/BPSK/BPSK Figures/RC in.PNG" height="400" width="400"> <img src="/BPSK/BPSK Figures/RC out.PNG"height="400" width="400"></p>

#### BER Analysis:
#### Set up:
1. Run BER tool by typing *bertool* into matlab command prompt
2. Under Theoretical tab, choose range (our case is -10:10), choose modulation technique and plot
3. Under Monte Carlo tab, choose range, load file and state variable name. (Variable is added through simout block as shown, could also just output error rate calculation to workspace) 
4. Run
#### Result:
Figure shows BER analysis of both without RC and with RC models shown above
![BER analysis](https://github.com/maryamshalaby/Modulation-Schemes-Simulator/blob/master/BPSK/BPSK%20Figures/BER.PNG)
It is apparent, that the RC transmitter and reciever introduced a higher error rate, that is because, intitally the model ha no ISI (inter symbol interference) to begin with, which is what the RC was designed to tackle. Its intro duction into the system introduced higher error due to the approximate nature of the RC filter in frequency domain.
