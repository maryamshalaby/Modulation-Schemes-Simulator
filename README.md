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
* Quadrature Amplitude Modulation (**QAM**)  16-64
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
* Number of Bits per symbol: 1
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
##### Error Rate Calculation:
* Recieve Delay: set to 10 , 2 * 2 * group delay , since we have 2 filters, double the delay.
#### Constellation Diagarams:
**Note**: EbNo set in the plotting of constellation diagrams is 10 db.
##### Without RC

<p align="center"> <img src="/BPSK/BPSK Figures/Channel in.PNG" height="400" width="400"> <img src="/BPSK/BPSK Figures/Channel out.PNG" height="400" width="400"></p>

As seen in the *channel in* constellation diagram, the input symbols are modulated into two phases: 0 and 180, thus  the two yellow dots. As for the *channel out* diagram, the effect of noise is apparant as it distorted the modulated carrier phases.
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
In QPSK Modulation, the 4-ary (2 bit) signal is modulated by changing the *phase* of a fixed frequency carrier signal. Four symbols are modulated in the following diagram, thus four phases exist in the system, 45,135,225 and 315 as will be shown in the *Constellation Diagram*. Basically it is the same as previous modulation technique, just a change in number of bits per symbol.
#### Function Blocks
The following figure shows the function blocks used. 
![QPSK Model](https://github.com/maryamshalaby/Modulation-Schemes-Simulator/blob/master/QPSK/QPSK%20Figures/BPSKRCmodel.PNG)
#### Function Blocks Parameter Set up
##### Random Integer Generator:
![Integer Generator](https://github.com/maryamshalaby/Modulation-Schemes-Simulator/blob/master/QPSK/QPSK%20Figures/intgen.PNG)
* M-ary Number: set to 4, as in 4-ary input

Rest of parameters explained above.
##### QPSK Modulator Baseband:
Default paramters used.
##### AWGN Channel:
![AWGN Channel](https://github.com/maryamshalaby/Modulation-Schemes-Simulator/blob/master/QPSK/QPSK%20Figures/awgn.PNG)
* Number of Bits per symbol: 2

Rest of parameters explained above.
##### QPSK Demodulator Baseband:
Default paramters used.
##### Error Rate Calculation:
Default paramters used.
#### Raised Cosine Set up
![QPSKRC Model](https://github.com/maryamshalaby/Modulation-Schemes-Simulator/blob/master/QPSK/QPSK%20Figures/BPSKRCmodel1.PNG)
##### Raised Cosine Transmit Filter:
Same predicament explained above.
##### Raised Cosine Recieve Filter:
Same predicament explained above.
##### Error Rate Calculation:
Same predicament explained above.
#### Constellation Diagarams:
##### Without RC

<p align="center"> <img src="/QPSK/QPSK Figures/Channel in.PNG" height="400" width="400"> <img src="/QPSK/QPSK Figures/Channel out.PNG" height="400" width="400"></p>

As seen in the *channel in* constellation diagram, the input symbols are modulated into four phases: 45,135,225 and 315, thus the four yellow dots.
##### With RC

<p align="center"><img src="/QPSK/QPSK Figures/RC in.PNG" height="400" width="400"> <img src="/QPSK/QPSK Figures/RC out.PNG"height="400" width="400"></p>

#### BER Analysis:
#### Set up:
Explained above.
#### Result:
Figure shows BER analysis of both without RC and with RC models shown above
![BER analysis](https://github.com/maryamshalaby/Modulation-Schemes-Simulator/blob/master/QPSK/QPSK%20Figures/BER.PNG)

--------------------------------------------------------------------------------
### FSK Modulation
In FSK Modulation, input stream is modulated by changing the *frequency* of a carrier signal. Each symbol is modulated to a distinct frequency. Here I chose to modulate a binary input stream, thus only two frequencies exist. (2-FSK)
#### Function Blocks
The following figure shows the function blocks used. 
![FSK Model](https://github.com/maryamshalaby/Modulation-Schemes-Simulator/blob/master/FSK/FSK%20Figures/FSKmodel.PNG)
#### Function Blocks Parameter Set up
##### Random Integer Generator:
![Integer Generator](https://github.com/maryamshalaby/Modulation-Schemes-Simulator/blob/master/FSK/FSK%20Figures/intgen.PNG)
* M-ary Number: set to 2, as in binary input

Rest of parameters same as above.

##### FSK Modulator Baseband:
![FSK Modulator Baseband](https://github.com/maryamshalaby/Modulation-Schemes-Simulator/blob/master/FSK/FSK%20Figures/fsk.PNG)
* Frequency seperation: set to 1 Hz, cause why not?
* Samples per symbol: set to 3. Since sampling rate, which is samples per symbol/sampling time should be more than double M * frequency seperation (Band width), To prevent aliasing-> Nyquist. 

Rest of parameters were left to default.

##### AWGN Channel:
Same as BPSK.
##### FSK Demodulator Baseband:
Parameters set as modulator.
##### Error Rate Calculation:
Default paramters used.
#### Raised Cosine Set up
![FSKRC Model](https://github.com/maryamshalaby/Modulation-Schemes-Simulator/blob/master/FSK/FSK%20Figures/FSKRCmodel.PNG)
##### Raised Cosine Transmit Filter:
Same predicament explained above.
##### Raised Cosine Recieve Filter:
Same predicament explained above.
##### Error Rate Calculation:
Same predicament explained above.
#### Constellation Diagarams:
##### Without RC

<p align="center"> <img src="/FSK/FSK Figures/Channel in.PNG" height="400" width="400"> <img src="/FSK/FSK Figures/Channel out.PNG" height="400" width="400"></p>

As seen in the *channel in* constellation diagram, the points plotted are not indicative of modulated frequency, but change with sampling rate. (phase of sampling)

##### With RC

<p align="center"><img src="/FSK/FSK Figures/RC in.PNG" height="400" width="400"> <img src="/FSK/FSK Figures/RC out.PNG"height="400" width="400"></p>

#### BER Analysis:
#### Set up:
Explained above.
#### Result:
Figure shows BER analysis of both without RC and with RC models shown above

![BER analysis](https://github.com/maryamshalaby/Modulation-Schemes-Simulator/blob/master/FSK/FSK%20Figures/BER.PNG)

**Note:** It seems that the RC filter has greater impact on FSK than other modulation techniques, causes higher BER! And intuitively it could be explained by the fact that th filter distorts frequency of signal and in FSK that is where the information lies.

--------------------------------------------------------------------------------
### QAM Modulation
In QAM Modulation, input stream is modulated by changing the *amplitude* of a carrier signal. Multiple input streams could be sent by changing the *phase* of carrier signal.
#### Function Blocks
The following figure shows the function blocks used. 
##### 16-QAM
![16-QAM Model](https://github.com/maryamshalaby/Modulation-Schemes-Simulator/blob/master/QAM16/QAM16%20Figures/QAM16model.PNG)
##### 64-QAM
![64-QAM Model](https://github.com/maryamshalaby/Modulation-Schemes-Simulator/blob/master/QAM64/QAM64%20Figures/QAM64model.PNG)

#### Function Blocks Parameter Set up
##### Random Integer Generator:
###### 16-QAM
![Integer Generator](https://github.com/maryamshalaby/Modulation-Schemes-Simulator/blob/master/QAM16/QAM16%20Figures/intgen.PNG)
* M-ary Number: set to 16

###### 64-QAM
* M-ary Number: set to 64

Rest of parameters were left to default.

##### QAM Modulator Baseband:
###### 16-QAM
![16-QAM Modulator Baseband](https://github.com/maryamshalaby/Modulation-Schemes-Simulator/blob/master/QAM16/QAM16%20Figures/qam.PNG)
* M-ary Number: set to 16
###### 64-QAM
* M-ary Number: set to 64

Rest of parameters were left to default.

##### AWGN Channel:
###### 16-QAM
* bits per symbol: set to 4 , =log2(16)
###### 64-QAM
* bits per symbol: set to 6 , =log2(64)

Rest of parameters were left to default.

##### QAM Demodulator Baseband:
Parameters set as modulator.
##### Error Rate Calculation:
Default paramters used.
#### Raised Cosine Set up
###### 16-QAM
![16-QAMRC Model](https://github.com/maryamshalaby/Modulation-Schemes-Simulator/blob/master/QAM16/QAM16%20Figures/QAM16RCmodel.PNG)
###### 64-QAM
![64-QAMRC Model](https://github.com/maryamshalaby/Modulation-Schemes-Simulator/blob/master/QAM64/QAM64%20Figures/QAM64RCmodel.PNG)
##### Raised Cosine Recieve Filter:
Same predicament explained above.
##### Error Rate Calculation:
Same predicament explained above.
#### Constellation Diagarams:
##### Without RC
###### 16-QAM
<p align="center"> <img src="/QAM16/QAM16 Figures/Channel in.PNG" height="400" width="400"> <img src="/QAM16/QAM16 Figures/Channel out.PNG" height="400" width="400"></p>

As seen in the *channel in* constellation diagram, input symbols are modulated into 4 different phases each with 4 different amplitudes, thus 16 possible combinations. 
###### 64-QAM
<p align="center"> <img src="/QAM64/QAM64 Figures/Channel in.PNG" height="400" width="400"> <img src="/QAM64/QAM64 Figures/Channel out.PNG" height="400" width="400"></p>

As seen in the *channel in* constellation diagram, input symbols are modulated into 8 different phases each with 8 different amplitudes, thus 64 possible combinations.
Also, A larger input vector (1000) had to be used so we could get points in each combination. ( visual purposes)

##### With RC

###### 16-QAM
<p align="center"> <img src="/QAM16/QAM16 Figures/RC in.PNG" height="400" width="400"> <img src="/QAM16/QAM16 Figures/RC out.PNG" height="400" width="400"></p>

###### 64-QAM
<p align="center"> <img src="/QAM64/QAM64 Figures/RC in.PNG" height="400" width="400"> <img src="/QAM64/QAM64 Figures/RC out.PNG" height="400" width="400"></p>


#### BER Analysis:
#### Set up:
Explained above.
#### Result:
Figure shows BER analysis of both without RC and with RC models shown above
###### 16-QAM
![BER analysis](https://github.com/maryamshalaby/Modulation-Schemes-Simulator/blob/master/QAM16/QAM16%20Figures/ber.PNG)

###### 64-QAM
![BER analysis](https://github.com/maryamshalaby/Modulation-Schemes-Simulator/blob/master/QAM64/QAM64%20Figures/BER.PNG)
