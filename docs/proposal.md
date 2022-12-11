# Project Proposal

## 1. Motivation & Objective

In this study we are trying to evaluate and compare the convergence time and maximum power point tracking accuracy of newer artificial intelligence based MPPT (maximum power point tracking) approaches to classical approaches such as Perturb & Observe. Classicial methods are simple to implement but they run into issues in evaluating MPP (maximum power point) when environmental conditions vary due to irradiance and temperature. AI Based methods to MPPT implemented with ANNs and Fuzzy Logic Controllers reportedly fix these issues and provided a faster response time; which is something that we would like to investigate and evaluate.

## 2. State of the Art & Its Limitations

Currently, the most efficient MPPT systems are those that employ a hybrid model to merge artificial intelligence with optimization techniques; with a key example being ANFIS (Adaptive Neuro Fuzzy Inference System) which is essentially takes the key benefits of existing Fuzzy Inference Systems (FIS) (the ability to work with uncertain inputs and without complex mathematical models) and combines that with the accelerated learning capability of artificial neural networks (ANN) to (in real-time) optimize and detemine the fuzzy rules that drive the output of the system. The limits of the ANFIS approach are mainly due to how they gather their inputs. For ANFIS MPPT systems that rely on irradiance and temperature sensing, the cost of irradiance sensors can be costly; and in all cases the key tradeoff is design complexity.

## 3. Novelty & Rationale

What is new in your approach and why do you think it will be successful?

Rather than coming up with a new approach for MPPT, we decided to spend time assessing the feasibility of existing approaches (namely ANN and FIS when compared to classical MPPT methods) so that we can better understand their benefits and limitations. This venture should be successful, as there is a lot of existing literature that we can pull design ideas from.

## 4. Potential Impact

If the project is successful, what difference will it make, both technically and broadly?

If the project is successful, we will have generated added justification as to the use of artifical intelligence in MPPT use-cases. With the design of our neural network scheme, we will have also created a low-cost embedded irradiance sensor that can be used as a way to coordinate MPPT across large solar farms where conditions might not be entirely uniform due to environmental conditions (cloud-cover, etc).

## 5. Challenges

What are the challenges and risks?

There are a lot of challenges that we can see in the project. Being a hardware-heavy project, there are a lot of risks that stem from hardware failure (part shortages and lead-times) as well as time lost due to needed to constantly be around lab instrumentation for testing. In addition, maximum-power-point is a hard thing to quantify in solar panels without exact measurements of irradiance and temperature. Used as a control, a classical MPPT algorithm (namely Perturb & Observe) could give us accurate MPP estimation in ideal conditions, however in partially shaded environments P&O would not be a good control and our results would lose confidence (i.e. are our AI methods accurately judging MPP would no concrete reference to compare to).

## 6. Requirements for Success

What skills and resources are necessary to perform the project?
In order to successfully perform this project, each team member will need to have basic hardware prototyping skills, basic knowledge of power electronics,knowledge of implementing AI methods on embedded devices (namely FIS and ANN), and knowledge of require programmining languages (C++, Matlab).

In terms of resources, we require embedded host devices (Arduino Nano 33 BLE Sense), dc-dc power converter hardware, sensors (voltage,current,and temperature), PV Panels, and access to lab instrumentation for testing both indoors and outdoors.

## 7. Metrics of Success

What are metrics by which you would check for success?

Given the nature of our comparison study, metrics that we would analyze for success include 
1. MPP Convergence Speed (how fast does the system converge on it's maximum power point
2. MPP Convergence Accuracy (how much error exists in the system's interpretation of MPP, and the actual MPP of the solar panel) 

## 8. Execution Plan

Describe the key tasks in executing your project, and in case of team project describe how will you partition the tasks.

The key tasks include:

1. Sampling and conditioning sensor data for our control algorithms (Morgan Williams will head this task)

3. Wirelessly transmission of sensor data. This involves utilizing the Wifi capabilities of the Arduino RP2040's Wifi to allow for remote monitoring of PV characteristics (Basheer Ammar will head this task)

5. Design of required MPPT hardware. This includes wiring of the solar panels, as well as design of the DC-DC converter that adjusts the PV operating point (Selasi Etchey will head this task)

7. Design of Neural Network MPPT Implementation. This includes training a neural network to act as an irradiance sensor, and closing an MPPT loop around that estimate (Selasi Etchey will head this task)

8. Design of PID Control. This aspect of the project is neccesary to close the loop around the Neural Network algorithm by adjusting our sensed PV current in the direction of our setpoint PV current (calculated as a result of Neural Network irradiance estimate) (Morgan Williams will head this task)

9. Design of Fuzzy Inference MPPT System. This includes design of the Fuzzy Logic Controller which acts as the 2nd AI control method that we plan to analyze in this comparison study. (Basheer Ammar will head this task)

10. Integration of Mbed OS to help with task scheduling and improving the real-time performance of the system (Morgan Williams will head this task)

## 9. Related Work

### 9.a. Papers

List the key papers that you have identified relating to your project idea, and describe how they related to your project. Provide references (with full citation in the References section below).

1. Yilmaz, Unal, et al. “PV System Fuzzy Logic MPPT Method and Pi Control as a Charge Controller.” Renewable and Sustainable Energy Reviews, vol. 81, 2018, pp. 994–1001., https://doi.org/10.1016/j.rser.2017.08.048. The inspiration for the setup of our fuzzy logic controller, and a previous attempt at using such a controller for the purpose of MPPT. Takes in error and change of error as an input, and returns a duty cycle output. Overall system explained also employs photovoltaic panels and a Proportional Integral (PI) controller operating a buck converter. 

2. “Fuzzy Logic Toolbox Documentation.” MathWorks, https://www.mathworks.com/help/fuzzy/index.html?s_tid=CRUX_topnav. 
Details the operation of the Fuzzy Logic Toolbox within MATLAB that was used to set up the environment used to conduct the fuzzy logic approach experiments.

3. A. Laudani, F. R. Fulginei, A. Salvini, G. M. Lozito and F. Mancilla-David, "Implementation of a neural MPPT algorithm on a low-cost 8-bit microcontroller," 2014 International Symposium on Power Electronics, Electrical Drives, Automation and Motion, 2014, pp. 977-981, doi: 10.1109/SPEEDAM.2014.6872101.
Implementation of a Neural Network based MPPT Algorithm on an 8-bit microcontroller. Method uses sensor data (Voltage,Temperature, and Current) in order to estimate incident irradiance on a solar panel as well as predicting optimal operating voltage of the panel. This paper was helpful in understanding how a neural network could aid in MPPT, as well as in providing some brief commentary on sizing neural networks for embedded applications.

4. F. Mancilla-David, F. Riganti-Fulginei, A. Laudani and A. Salvini, "A Neural Network-Based Low-Cost Solar Irradiance Sensor," in IEEE Transactions on Instrumentation and Measurement, vol. 63, no. 3, pp. 583-591, March 2014, doi: 10.1109/TIM.2013.2282005.
Implementation of a neural network as a low-cost solar array irradiance estimator, bypassing the need for expensive pyranometers.This Irradiance sensor can be used to for more efficient control of large solar plants, where shading effects are unpredictable and widespread. This paper was useful in helping to build the PV model that we used to train our neural network, as well as understanding its potential use-case as an open-loop irradiance sensor

10. Abdullah M. Noman, Khaled E. Addoweesh, Abdulrahman I. Alolah, "Simulation and Practical Implementation of ANFIS-Based MPPT Method for PV Applications Using Isolated Ćuk Converter", International Journal of Photoenergy, vol. 2017, Article ID 3106734, 15 pages, 2017. https://doi.org/10.1155/2017/3106734. This article better helped us understand the current state of the art when it comes to MPPT (ANFIS).


### 9.c. Software

5. MATLAB (Fuzzy Logic Toolbox)
6. MATLAB (Deep Learning Toolbox)
7. Simulink
8. Arduino PID_v1 library
9. Arduino MBED OS library


## 10. References

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


