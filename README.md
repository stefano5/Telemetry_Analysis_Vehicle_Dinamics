# Telemetry_Analysis_Vehicle_Dinamics

These notebooks have been written in the Vehicle Dynamics course at the Università di Pisa.

The final report is provided, see "Stefano_Maugeri_report.pdf".


**The telemetry data cannot be provided.**

The format source file is a .xls file (with multiple sheets) and it must have the following syntax:

| time (s) | distance (m) | speed (km/s) | acc X (g) | acc Y (g) | yaw rate (deg/s) | steer angle (deg) | body sleep angle (deg)|
|----------|:------------:|:------------:|:---------:|:---------:|:----------------:|:-----------------:|:---------------------:|
| value    |   value      |   value      |   value   |  value    |    value         |    value          |     value             |



The acceleration should be expressed in g, the notebooks itself convert it in m/s^2
The sign expected to be read by the notebook are:
 - Positive Acc X -> acceleration backwards 
 - Negative Acc X -> acceleration forward
 - Positive Acc Y -> turn left
 - Negative Acc Y -> turn right
 - Positive Yaw rate -> turn left
 - Negative Yaw rate -> turn right
 - Positive steer angle -> turn left
 - Negative steer angle -> turn right
 
The data may be noisy, notebooks will filter them. This is a crucial step, based on how noisy the signals are you will have a parameter to use to filter them.

Software is divided into four notebooks.
  1) load_data_NB1.nb
  2) filtering_NB2.nb
  3) telemetry_NB3.nb
  4) function_declatarions_NB0.nb

# load_data_NB1.nb
Load the raw data from the directory in which the notebooks are located.
If there are more than one xls file in the directory the notebook will ask you which xls file you want to load.
If the chosen xls file has more than one sheets then the notebooks will ask you which sheet you want to analyze.

**The load file will fail if the format file is wrong**

After the loading the notebooks will say: "Would you run all notebooks?"
  If you press "no" the other notebooks will not be evaluated.
  If you press "yes" the "filtering_NB2.nb" notebook and "telemetry_NB3.nb" notebook will be opened then evaluated.
In any case will be evaluated the "function_declatarions_NB0.nb" notebook.

These are the sections.
![](https://i.imgur.com/yxg6GFM.png)


# filtering_NB2.nb

If the data are raw you need to filter them.
Use "Control Panel" section to fit a satisfactory value of omega, omega is the act of the filter.
![](https://i.imgur.com/W2JOtIh.png)
After found them for every signal, write it here (replace the second parameter of the function "actFilter") shown above.


# telemetry_NB3.nb
This notebook contains the telemetry analysis.

![](https://i.imgur.com/aLdTiF4.png)

## Conversion & Trajectory Building
This (sub)section has not output. Computes the trajectory of the vehicle center of mass.

## Angular Acceleration
Computes the angular acceleration. This was a request from the course project, and we need of this signal for other computations.

## Plot Telemetry
Show the telemetry in order to check them. 

## Plot Circuit
Having the yaw angle, the longitudinal and the lateral velocity, it was possible to calculate the velocity of the center of mass. Now integrating the vector the points of the trajectory performed by the vehicle were obtained. But, as shown bottom, the error grows as the integration progresses. 

![1](https://user-images.githubusercontent.com/40228829/159125678-a4116c17-001f-45f7-953e-51e471920d59.svg)


This phenomenon is due to the sensors quality. If the integration is made in the opposite direction, the result obtained is the same: the error increases with the progression of the integration, but from the opposite direction, as shown bottom.

![2](https://user-images.githubusercontent.com/40228829/159125681-927efa2e-e6cc-4a70-a8e2-df4e731a8325.svg)

By making a weighted average of the two trajectories it is possible to obtain the correct (and closed) trajectory.

![3](https://user-images.githubusercontent.com/40228829/159125689-93f89e65-b041-4343-8b28-b06fff23c5b6.svg)


## Curves Identification
This is a trial and error tool to identify the curves. 
Is based on the lateral acceleration.
This tool take the square of lateral acceleration and allow you to choose a threshold above which it is assumed to be cornering.

![Cattura](https://user-images.githubusercontent.com/40228829/159125785-38972d89-e841-446a-bb50-9d3a25ea15d5.PNG)



You have to fit two empirical parameters (depend on the noise of the data):
  1) omega -> other filtering, if reuired (tip: should be small)
  2) threshold -> choose the threshold above which you assumed to be cornering (tip: this is the main parameter)

For every circuit you know the real number of corners. Fit these two parameters keeping that in mind.
However the effect of the parameters is immediately seen on the circuit very clearly.

## Moving Centrodes, Fixed Centrodes & Moving and Fixed Centrodes
Compute the moving and fixed centrodes of the vehicle. The theory of this procedure is explained [here](http://www.dimnp.unipi.it/guiggiani-m/fig_centrodes_guiggiani.html).

![2222](https://user-images.githubusercontent.com/40228829/159126042-257e4da3-0af6-43f7-8b80-727f8afe2f6a.PNG)


## Plot all Centrodes & Circuit  
Show all centrodes when the car entering the curve. Therefore the car is shown going into the circuit and, when facing a curve, the relative polars are shown.

![aaaaa](https://user-images.githubusercontent.com/40228829/159126133-740d6209-6629-4b52-9b80-cfa9498d7975.PNG)


## Lateral Force
This is an example of a useful tool. It shows the lateral acceleration and the circuit in two different plot. 
It also shows the position of the vehicle in the circuit and, in the acceleration graph, it shows the value of the vehicle acceleration at that point in the circuit (red circle)


![aaaaa](https://user-images.githubusercontent.com/40228829/159126235-c993293f-9ec9-4f6c-9c30-8854a36a52ac.svg)

## Inflection Circle
It shown all the centrodes and the inflection circle, see the theory [here](http://www.dimnp.unipi.it/guiggiani-m/fig_centrodes_guiggiani.html).

![aaaaa](https://user-images.githubusercontent.com/40228829/159126332-b04764ff-ec48-4b09-99ca-3b9a6902c797.PNG)


## gg Plot
Show the gg plot that is the acceleration (X e Y) expressed in g.

![aaaaa](https://user-images.githubusercontent.com/40228829/159126368-2328428e-34f0-4ec6-a8ae-fe7b2f27993e.svg)


## Slip Angle, Compare Circuit with Graph
The compute of the sleep angle from other signals was a request of the course project. The "Compare Circuit with Graph" section was made in order to write the final report of the project.

# function_declatarions_NB0.nb
Here there are the complex functions declarations of the previus functions.



 
