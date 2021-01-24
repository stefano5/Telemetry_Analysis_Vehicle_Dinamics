# Telemetry_Analysis_Vehicle_Dinamics

These notebooks was written in the Vehicle Dynamics course (Università di Pisa).

**The telemetry data cannot be provided and i cannot (than i will not) show here any plot or result.**

The format file is a .xls (with multiple sheets) file with following syntax:

| time (s) | distance (m) | speed (km/s) | acc X (g) | acc Y (g) | yaw rate (deg/s) | steer angle (deg) | body sleep angle (deg)|
|----------|:------------:|:------------:|:---------:|:---------:|:----------------:|:-----------------:|:---------------------:|
| value    |   value      |   value      |   value   |  value    |    value         |    value          |     value             |



The acceleration should be expressed in g, the notebooks itself convert it in m/s^2 (multiplying by 9.81)
The sign expected to read by the notebook are:
 + Acc X -> acceleration backwards 
 - Acc X -> acceleration forward
 + Acc Y -> turn left
 - Acc Y -> turn right
 + yaw rate -> turn left
 - yaw rate -> turn right
 + steer angle -> turn left
 - steer angle -> turn right
 
The data may be raw, notebooks will filter them. This is a crucial step, based on how rough the signals are you will have a parameter to use to filter them.

The software is divided into four notebooks.
  1) load_data_NB1.nb
  2) filtering_NB2.nb
  3) telemetry_NB3.nb
  4) function_declatarions_NB0.nb

# load_data_NB1.nb
Load the raw data from the directory in which the notebooks are located.
If there are more than one xls file in the directory the notebooks ask you which xls file you want to load.
If the xls file has more than one sheets the notebooks ask you which sheet you want to analyze.

**The load file can fail if the format file is wrong**

After the loading the notebooks will say: "Would you run all notebooks?"
  If you press "no" the other notebooks will not be evaluated.
  If you press "yes" the "filtering_NB2.nb" notebook and "telemetry_NB3.nb" notebook will be opened than evaluated.
In any case will be evaluated the "function_declatarions_NB0.nb" notebook (it is mandatory).

These are the sections. Again, i cannot show any result.
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
This (sub)section have not output. Computes the trajectory of the vehicle center of mass.

## Angular Acceleration
Computes the angular acceleration. This was a request from the course project, and we need of this signal for other computations.

## Plot Telemetry
Show the telemetry in order to check them. 

## Plot Circuit
If the signals have been written correctly in the file now the circuit (trajectory of the vehicle center of mass) will be shown.

## Curves Identification
This is a trial and error tool to identify the curves. 
Is based on the lateral acceleration.
This tool take the square of lateral acceleration and allow you to choose a threshold above which it is assumed to be cornering.

![](https://i.imgur.com/RoIwlW3.png)

You have to fit two empirical parameters (depend on the noise of the data):
  1) omega -> other filtering, if reuired (personal advice, shoul be little)
  2) threshold -> choose the threshold above which you assumed to be cornering (personal advice, this is the main parameter)

For every circuit you know the real number of corner. Fit this two parameters keeping that in mind.
However the effect of the parameters is immediately seen on the circuit very clearly.

## Moving Centrodes, Fixed Centrodes & Moving and Fixed Centrodes
Compute the moving and fixed centrodes of the vehicle. the theory of this procedure is explained [here](http://www.dimnp.unipi.it/guiggiani-m/fig_centrodes_guiggiani.html).

## Plot all Centrodes & Circuit  
Show all centrodes when the car entering the curve. Therefore the car is shown going into the circuit and, when facing a curve, the relative polars are shown.

## Lateral Force
This is an example of a useful tool. Shown the lateral acceleration and the circuit in two different plot. 
It also shows the position of the vehicle in the circuit and, in the acceleration graph, shows the value of the vehicle acceleration at that point in the circuit

![](https://i.imgur.com/A92Ekus.png)

## Inflection Circle
It shown all the centrodes and the inflection circle, see the theory [here](http://www.dimnp.unipi.it/guiggiani-m/fig_centrodes_guiggiani.html).
![](https://i.imgur.com/1Fy4t5t.png)

## gg Plot
Show the gg, plot that is the acceleration (X e Y) expressed in g.

## Slip Angle, Compare Circuit with Graph
The compute of the sleep angle from other signals was a request from the course project. The "Compare Circuit with Graph" section was made for write the final report of the project.

# function_declatarions_NB0.nb
Here there are the complex functions declarations of the previus functions.



 
