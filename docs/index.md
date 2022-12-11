# Abstract

In this project, we attempt to implement and run a comparison study on different methods for Maximum Power Point Tracking (MPPT) in solar panels, namely the accuracy and speed of widely used conventional algorithms such as ‘Perturb & Observe, compared to more novel methods that employ the use of approaches based on artificial intelligence (such as ‘Artificial Neural Networks’ and ‘Fuzzy Logic Inference’) in tracking a panel’s maximum power point.

Maximum Power Point Trackers, no matter the methodology that they implement, operate on the principle of dynamic impedance matching. Effectively, for any given load impedance on a solar panel given by (V_load / I_load) where V_load is the voltage across the load and I_load is the current across the load, there is a corresponding source impedance of the panel (V_panel / I_panel) that would maximize power transfer to the load according to the theory of maximum power transfer. Maximum Power Point Tracking is the process of adding a DC-DC converter in between the solar panels and the load, which is meant to dynamically adjust the operating characteristics of the solar panel in order to force the delivery of maximum power to the load, even in the face of deviations in incident irradiance and temperature.

In this study, we implemented 3 MPPT control methods (Perturb & Observe as a conventional method, as well as an Artificial Neural Network and Fuzzy Logic Inference System as AI driven methods), however due to lack of promising sunny weather conditions as well as hardware/software pitfalls we were not able to adequately test all of these control methods in a closed-loop environment. In this report, we will talk through our designs, results, and the promising future of the project given what we learned along the way.

# Team

* Basheer Ammar
* Morgan Williams
* Selasi Etchey

# Required Submissions

* [Final Presentation Slides](https://docs.google.com/presentation/d/1IBYgcV8_e2lx5zYscwHHeMJKVIinyxMxd2ZOYi4wM5s/edit#slide=id.p)
* [Final Report](report.md)
