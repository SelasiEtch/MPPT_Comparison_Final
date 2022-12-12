# Table of Contents
* Abstract
* [Introduction](#1-introduction)
* [Related Work](#2-related-work)
* [Technical Approach](#3-technical-approach)
* [Evaluation and Results](#4-evaluation-and-results)
* [Discussion and Conclusions](#5-discussion-and-conclusions)
* [References](#6-references)

# Abstract

In this project, we attempt to implement and run a comparison study on different methods for Maximum Power Point Tracking (MPPT) in solar panels, namely the accuracy and speed of widely used conventional algorithms such as ‘Perturb & Observe, compared to more novel methods that employ the use of approaches based on artificial intelligence (such as ‘Artificial Neural Networks’ and ‘Fuzzy Logic Inference’) in tracking a panel’s maximum power point.

Maximum Power Point Trackers, no matter the methodology that they implement, operate on the principle of dynamic impedance matching. Effectively, for any given load impedance on a solar panel given by (V_load / I_load) where V_load is the voltage across the load and I_load is the current across the load, there is a corresponding source impedance of the panel (V_panel / I_panel) that would maximize power transfer to the load according to the theory of maximum power transfer. Maximum Power Point Tracking is the process of adding a DC-DC converter in between the solar panels and the load, which is meant to dynamically adjust the operating characteristics of the solar panel in order to force the delivery of maximum power to the load, even in the face of deviations in incident irradiance and temperature.

In this study, we implemented 3 MPPT control methods (Perturb & Observe as a conventional method, as well as an Artificial Neural Network and Fuzzy Logic Inference System as AI driven methods), however due to lack of promising sunny weather conditions as well as hardware/software pitfalls we were not able to adequately test all of these control methods in a closed-loop environment. In this report, we will talk through our designs, results, and the promising future of the project given what we learned along the way.

# 1. Introduction

## 1. Motivation & Objective

In this study we are trying to evaluate and compare the convergence time and maximum power point tracking accuracy of newer artificial intelligence based MPPT (maximum power point tracking) approaches to classical approaches such as Perturb & Observe. Classicial methods are simple to implement but they run into issues in evaluating MPP (maximum power point) when environmental conditions vary due to irradiance and temperature. AI Based methods to MPPT implemented with ANNs and Fuzzy Logic Controllers reportedly fix these issues and provided a faster response time; which is something that we would like to investigate and evaluate.

## 2. State of the Art & Its Limitations

Currently, the most efficient MPPT systems are those that employ a hybrid model to merge artificial intelligence with optimization techniques; with a key example being ANFIS (Adaptive Neuro Fuzzy Inference System) which is essentially takes the key benefits of existing Fuzzy Inference Systems (FIS) (the ability to work with uncertain inputs and without complex mathematical models) and combines that with the accelerated learning capability of artificial neural networks (ANN) to (in real-time) optimize and detemine the fuzzy rules that drive the output of the system. The limits of the ANFIS approach are mainly due to how they gather their inputs. For ANFIS MPPT systems that rely on irradiance and temperature sensing, the cost of irradiance sensors can be costly; and in all cases the key tradeoff is design complexity.

## 3. Novelty & Rationale

Rather than coming up with a new approach for MPPT, we decided to spend time assessing the feasibility of existing approaches (namely ANN and FIS when compared to classical MPPT methods) so that we can better understand their benefits and limitations. This venture should be successful, as there is a lot of existing literature that we can pull design ideas from.

## 4. Potential Impact

If the project is successful, we will have generated added justification as to the use of artifical intelligence in MPPT use-cases. With the design of our neural network scheme, we will have also created a low-cost embedded irradiance sensor that can be used as a way to coordinate MPPT across large solar farms where conditions might not be entirely uniform due to environmental conditions (cloud-cover, etc).

## 5. Challenges

There are a lot of challenges that we can see in the project. Being a hardware-heavy project, there are a lot of risks that stem from hardware failure (part shortages and lead-times) as well as time lost due to needed to constantly be around lab instrumentation for testing. In addition, maximum-power-point is a hard thing to quantify in solar panels without exact measurements of irradiance and temperature. Used as a control, a classical MPPT algorithm (namely Perturb & Observe) could give us accurate MPP estimation in ideal conditions, however in partially shaded environments P&O would not be a good control and our results would lose confidence (i.e. are our AI methods accurately judging MPP would no concrete reference to compare to).

## 6. Requirements for Success

In order to successfully perform this project, each team member will need to have basic hardware prototyping skills, basic knowledge of power electronics,knowledge of implementing AI methods on embedded devices (namely FIS and ANN), and knowledge of require programmining languages (C++, Matlab).

In terms of resources, we require embedded host devices (Arduino Nano 33 BLE Sense), dc-dc power converter hardware, sensors (voltage,current,and temperature), PV Panels, and access to lab instrumentation for testing both indoors and outdoors.

## 7. Metrics of Success

Given the nature of our comparison study, metrics that we would analyze for success include 
1. MPP Convergence Speed (how fast does the system converge on it's maximum power point
2. MPP Convergence Accuracy (how much error exists in the system's interpretation of MPP, and the actual MPP of the solar panel) 

# 2. Related Work

### 2.a. Papers

List the key papers that you have identified relating to your project idea, and describe how they related to your project. Provide references (with full citation in the References section below).

1. Yilmaz, Unal, et al. “PV System Fuzzy Logic MPPT Method and Pi Control as a Charge Controller.” Renewable and Sustainable Energy Reviews, vol. 81, 2018, pp. 994–1001., https://doi.org/10.1016/j.rser.2017.08.048. The inspiration for the setup of our fuzzy logic controller, and a previous attempt at using such a controller for the purpose of MPPT. Takes in error and change of error as an input, and returns a duty cycle output. Overall system explained also employs photovoltaic panels and a Proportional Integral (PI) controller operating a buck converter. 

2. “Fuzzy Logic Toolbox Documentation.” MathWorks, https://www.mathworks.com/help/fuzzy/index.html?s_tid=CRUX_topnav. 
Details the operation of the Fuzzy Logic Toolbox within MATLAB that was used to set up the environment used to conduct the fuzzy logic approach experiments.

3. A. Laudani, F. R. Fulginei, A. Salvini, G. M. Lozito and F. Mancilla-David, "Implementation of a neural MPPT algorithm on a low-cost 8-bit microcontroller," 2014 International Symposium on Power Electronics, Electrical Drives, Automation and Motion, 2014, pp. 977-981, doi: 10.1109/SPEEDAM.2014.6872101.
Implementation of a Neural Network based MPPT Algorithm on an 8-bit microcontroller. Method uses sensor data (Voltage,Temperature, and Current) in order to estimate incident irradiance on a solar panel as well as predicting optimal operating voltage of the panel. This paper was helpful in understanding how a neural network could aid in MPPT, as well as in providing some brief commentary on sizing neural networks for embedded applications.

4. F. Mancilla-David, F. Riganti-Fulginei, A. Laudani and A. Salvini, "A Neural Network-Based Low-Cost Solar Irradiance Sensor," in IEEE Transactions on Instrumentation and Measurement, vol. 63, no. 3, pp. 583-591, March 2014, doi: 10.1109/TIM.2013.2282005.
Implementation of a neural network as a low-cost solar array irradiance estimator, bypassing the need for expensive pyranometers.This Irradiance sensor can be used to for more efficient control of large solar plants, where shading effects are unpredictable and widespread. This paper was useful in helping to build the PV model that we used to train our neural network, as well as understanding its potential use-case as an open-loop irradiance sensor

10. Abdullah M. Noman, Khaled E. Addoweesh, Abdulrahman I. Alolah, "Simulation and Practical Implementation of ANFIS-Based MPPT Method for PV Applications Using Isolated Ćuk Converter", International Journal of Photoenergy, vol. 2017, Article ID 3106734, 15 pages, 2017. https://doi.org/10.1155/2017/3106734. This article better helped us understand the current state of the art when it comes to MPPT (ANFIS).


### 2.b. Software

5. MATLAB (Fuzzy Logic Toolbox)
6. MATLAB (Deep Learning Toolbox)
7. Simulink
8. Arduino PID_v1 library
9. Arduino MBED OS library

# 3. Technical Approach

Hardware

DC-DC Converter
At the very core of this project is a DC-DC converter which bridges the gap between our software control algorithms, and the act of adjusting the operating point of our solar panel. Buck converters work well for this purpose as they are able to regulate a lower DC output voltage from a higher DC input voltage as well as a PWM signal input, which can easily be generated by modern microcontrollers. 


Figure 1: Standard Buck Converter Design 
![Figure 1](MPPT_Comparison_Final/docs/media/Figure_1.png)

Initially, our buck converter was made out of discrete parts, as is seen in Figure 1, however a lack of a gate driver IC to switch the transistor ‘S’ at high frequencies led us to search for more integrated options that would allow us to adjust the buck converter setpoint dynamically. Eventually we settled on using the Arduino Motor Driver Shield Rev3 and operating it as an adjustable PWM digital-to-analog converter that we could operate with a PWM signal and low-pass filter the output in order to achieve the same results.


Figure 2: High Level Schematic of Arduino Motor Driver Shield and Project Implementation 
![Figure 2a](MPPT_Comparison_Final/docs/media/Figure_2_a.jpg)
![Figure 2b](MPPT_Comparison_Final/docs/media/Figure_2_b.jpg)

As you can see in Figure 2, by adjusting the motor driver to only operate in the forward position (meaning the top-right and top-left transistors will always be off) and shorting ‘Vout-’ to ground, we essentially reach that same buck converter design as in Figure 1 by attaching our low-pass filter between ‘Vout+’ and ground, and utilizing the motor protection diode of the bottom-left transistor as the freewheeling diode in our converter. Through testing, we found our that this design is not very useful to our cause as the input voltage (Vin) which is connected to the output of our solar panel requires a minimum of 6V for the motor driver to operate, leading us to connect a 9V battery in series to ensure that that the converter is able to operate even when the solar panels are shaded and their voltage drops. Here we have a video showcasing the buck converter’s operation with an input PWM signal (https://www.youtube.com/shorts/_8I-USZ9iXU PWM Signal - Yellow, Buck Output - Green).


Sensors

1.Voltage Sensor - A simple resistive divider was used as a voltage sensor in order to sense the input solar panel voltage
Output of the voltage sensor was 0.16V/V

2.Temperature Sensor - The temperature sensor was realized by a Adafruit AMG 8833 IR Thermal Camera
The sensor communicates temperature values for its 8x8 optical grid via I2C. For this project, pixel temperatures were averaged so as to provide average panel temperature when pointed at a solar panel

3.Current Sensor - The Sparkfun ACS723 Current Sensor Breakout Board was used for the project as it gave us a ‘high-sensitivity’ current sensor, allowing us to between distinguish our measurements from the noise floor (switching converters produce a good amount of sensor noise). Output of the current sensor was adjusted to 0.8V/A

4. Solar Panel - SunnyTech 2 Watt, 6V, 330mA Solar Panel Module (ZW-136110-3). Project Configuration was 2 Series, 2 Parallel

Software

1. Perturb & Observe
Overview:

This classic algorithm perturbs the operating voltage to ensure maximum power. The P&O method is widely employed in practice, due to its low-cost, simplicity and ease of implementation. It operates periodically by perturbing the operating voltage point and observing the power variation in order to deduct the direction of change to give to the DC Converter. It is typically a slow algorithm as perturbation steps are typically fixed, and as such it is not well adjusted to large setpoint variations.
Implementation:

In this technique, our first step is to sample the PV voltage and current, and multiply to get instantaneous power. Instantaneous power is compared to and subtracted from the previous power sampled (difference is P). Similarly, V is found by subtracting the previous voltage sample from the current voltage sample. To check if we are moving closer to the system maximum power point we compare P and V. If both quantities are positive, then the slope (PV) is positive, indicating that we are on the left side and approaching MPP with an increase in PV voltage. Essentially, maximum power is achieved when PV=0 , and we perturb PV voltage in the opposite direction when PV< 0. 
Results

Closed Loop Perturb & Observe Test Video: (https://www.youtube.com/watch?v=P4zq_pb_fxU)

2. Artificial Neural Network
System Diagram: 
![NN System Diagram](MPPT_Comparison_Final/docs/media/NN_Diagram.jpg)

Overview:

The goal of the ANN approach was to train a Neural Network to estimate the maximum power point of a solar panel using measurements of its output voltage, output current, and temperature. In our implementation, we trained a neural network to act as a low cost irradiance sensor, estimating incident irradiance on the panel, which then could aid in calculating maximum power point. This approach was chosen because MPPT is still at the core of the system, however many large solar farms could also benefit from a low-cost irradiance sensor ‘dummy panel’ that could work to coordinate MPPT as well providing practical irradiance information that could be used in understanding panel degradation/wear.

Implementation:

The Neural Network was provided with 2000 datapoints of Voltage, Current, and Temperature that came from a MATLAB script working to solve the expanded form of the single diode solar cell IV model for Irradiance (‘G’) with random combinations of voltage, current, and temperature (IA,VA, and T)
(Discussion of this model can be found in [3]). A 2 layer feedforward network with 3 hidden layers was determined to be sufficient for our use-case, as we can see the in the neural network multivariate fitting results with 1 hidden layer, 2 hidden layers,and 3 hidden layers 

![NN 1 Hidden Layer](MPPT_Comparison_Final/docs/media/NN_1_Hidden_Layer.png)
![NN 2 Hidden Layer](MPPT_Comparison_Final/docs/media/NN_2_Hidden_Layer.png)
![NN 1 Hidden Layer](MPPT_Comparison_Final/docs/media/NN_3_Hidden_Layer.png)

The network employs regression tactics in order to learn its own mapping of the input data to the desired irradiance output

Results:

Seen in Figure 3, we test the accuracy of the neural network irradiance estimates on I-V curves that we were able to generate from datasheet values of our panel modules through Simulink’s SimScape PV Array Block. While not exact (we see about a 14% error), the irradiance estimates are in proximity to the actual values of irradiance for each I-V curve.
Irradiance Estimator Test Video: (https://www.youtube.com/shorts/F8F-q0dnJ0A)


Figure 3: Neural Network Irradiance Estimation Testing 
![Figure 3](MPPT_Comparison_Final/docs/media/Figure_3.png)

3. Fuzzy Logic Inference System
System Diagram: 
![Fuzzy System Diagram](MPPT_Comparison_Final/docs/media/Fuzzy_Inference_Diagram.png)

Overview:

Fuzzy logic is a simpler artificial intelligence system that aims to emulate the way humans are able to describe certain observations using arguably “vague” statements and then translate said observations into actionable information. More specifically, a fuzzy logic controller will take in “crisp” numerical inputs and, through a membership function, convert them into “fuzzy” inputs described by the appropriate descriptors. Then, using a set of rules defined by the experiential knowledge of the operators, the appropriate output given the inputs is provided, and is converted to a “crisp” output. This feature allows for a precise and continuous spectrum of estimations, especially in applications where we have substantial knowledge on the correlation between fuzzy inputs and outputs.

Implementation:

We constructed our FLC using MATLAB’s Fuzzy Logic toolbox, modeling our controller design, which consisted essentially of our rules and membership functions, after the controller designed in Yilmaz et al.’s paper. This controller takes an error value, consisting of the change in power divided by the change in voltage, as well as the difference between the current and previous error measurement and outputs a duty cycle value. Differences between our FLC and the one designed in the paper include tighter bounds for the “zero” fuzzy inputs both for error and change in error, in the interest of ensuring the highest quality result, and the duty cycle output being between zero and one in order to match traditional representations of duty cycle and allow it to be represented as a “percent” value.


Figure 4: Rules for the Fuzzy Logic Controller 
![Fuzzy Rules](MPPT_Comparison_Final/docs/media/Figure_4.png)


Figure 5: Membership Functions for the Fuzzy Logic Controller
![Fuzzy Membership 1](MPPT_Comparison_Final/docs/media/Figure_5_a.png)
![Fuzzy Membership 2](MPPT_Comparison_Final/docs/media/Figure_5_b.png)
![Fuzzy Membership 3](MPPT_Comparison_Final/docs/media/Figure_5_c.png)

The voltage and current measurements that are used to generate the inputs to the FLC are collected by our sensors and are sent from the Arduino to MATLAB to be used in a Simulink model which employs our Fuzzy Logic controller. The FLC then gives us our duty cycle value and sends it back to the Arduino before the next iteration. The updates to our duty cycle assist us in moving towards the maximum power point. As a higher change in power corresponds to a higher error, we aim to observe the eventual reduction of that change in power to zero, as that occurs at the maximum value of the change in power over change in voltage.

Results:
In tests that used simulated values, the transmission between the Arduino and MATLAB were successful. The Fuzzy Logic Controller itself also worked as expected, with realistic outputs being displayed for the inputs provided.

4. MBED OS 
Overview:

In control systems theory it is typically good practice to have sensing working in parallel to actuation. Our goal was to use Mbed OS to help in task scheduling and the allocation of shared resources (sensor data) among tasks, so that we could better control the flow of data for efficient real-time control. Our three MPPP algorithms operated with the same three high level tasks: Sensing data, data transmission for remote monitoring, and updating the system operating point.

Results:
Unfortunately, we were not able to get MBED task scheduling working with our existing codebase. That aspect of the project is deemed to be a work in progress.

5. Wifi Data Transmission for Remote Monitoring
Overview:

Experiments involving Wi-Fi data transmission to a web browser were conducted while we were still using the Arduino Nano RP2040, which had compatibility with Arduino’s WiFiNINA library. Our proof of concept allowed for timely and automatic updates and were tested with sensor data 


# 4. Evaluation and Results

Although we were able to get most our our hardware and software working in an open-loop environment, we were not able to get things working in a closed-loop setting for the comparison study due to multiple setbacks and pitfalls that we encountered during the implementation process.

Hardware: 
Multiple current sensor failures and hardware failures plagued the beginning parts of the project, setting us back in our timeline as we waited for parts and adjusted our implementation strategy

Software:
Trouble implementing a neural network and fuzzy logic inference system natively on and embedded device
We were limited to sending data through our Simulink models for these control systems, adding unnecessary delay to the control response. In addition, issues with the serial connection on the BLE Sense boards automatically disconnecting after code was flashed was an issue we encountered  late in the quarter. This prevented us from being able to view serial sensor data, and adequately test the AI control algorithms which depended on a serial data stream to Simulink

Miscellaneous:
Numerous cloudy and cold weather conditions in December/November limited our already short time windows for testing, and we found it hard to test our system adequately without the aid of lab instrumentation (oscilliscopes and power supplies) that we could move outside.


# 5. Discussion and Conclusions

We’ve been able to verify that the AI Control Algorithms we undertook work as expected in an open-loop setting (not actively doing MPPT) but setbacks in hardware and software prevented (described above) prevented us being able to perform the comparison study that we initially set out to test; however we’ve learned valuable lessons that pave a path forward with improvements to the system 

Hardware Improvements: 
Switching to a standard buck converter design with an adequate gate driver would be a key change. Our Motor Driver PWM DAC was a solution that we had laying around without the need to buy more parts, however the 6V minimum input voltage forced us to attach a battery in series with our panel,and necessitates substracting out the current/voltage error in the sensor data. In addition,an integrated PCB Design for hardware would improve usability and reduce efficiency reductions from breadboard parasitics and noise

Software Improvements:
Implementation of AI control methods on native embedded hardware would allow for a design more robust to latency and negates the serial link issues that we encountered towards the end of the quarter. Developing adequate simulation models of our control algorithms and hardware would would help us ensure that our approaches are conceptually sound before attemping to debug issues that might be the cause of a flawed approach.


# 6. References

1. Yilmaz, Unal, et al. “PV System Fuzzy Logic MPPT Method and Pi Control as a Charge Controller.” Renewable and Sustainable Energy Reviews, vol. 81, 2018, pp. 994–1001., https://doi.org/10.1016/j.rser.2017.08.048.

2. “Fuzzy Logic Toolbox Documentation.” MathWorks, https://www.mathworks.com/help/fuzzy/index.html?s_tid=CRUX_topnav. 

3. A. Laudani, F. R. Fulginei, A. Salvini, G. M. Lozito and F. Mancilla-David, "Implementation of a neural MPPT algorithm on a low-cost 8-bit microcontroller," 2014 International Symposium on Power Electronics, Electrical Drives, Automation and Motion, 2014, pp. 977-981, doi: 10.1109/SPEEDAM.2014.6872101.

4. F. Mancilla-David, F. Riganti-Fulginei, A. Laudani and A. Salvini, "A Neural Network-Based Low-Cost Solar Irradiance Sensor," in IEEE Transactions on Instrumentation and Measurement, vol. 63, no. 3, pp. 583-591, March 2014, doi: 10.1109/TIM.2013.2282005.

5. Matlab Fuzzy Logic Toolbox (https://www.mathworks.com/products/fuzzy-logic.html)

6. Matlab Deep Learning Toolbox (https://www.mathworks.com/products/deep-learning.html)

7. Simulink (https://www.mathworks.com/products/simulink.html)

8. Arduino PID_v1 library (https://github.com/br3ttb/Arduino-PID-Library)

9. Arduino MBED OS Library (https://github.com/arduino/ArduinoCore-mbed)

10. Abdullah M. Noman, Khaled E. Addoweesh, Abdulrahman I. Alolah, "Simulation and Practical Implementation of ANFIS-Based MPPT Method for PV Applications Using Isolated Ćuk Converter", International Journal of Photoenergy, vol. 2017, Article ID 3106734, 15 pages, 2017. https://doi.org/10.1155/2017/3106734
