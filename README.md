# Tuning a 2017 Ford Mustang 3.7L V6

This a compilation fo the steps to tune my personal car after installing a Procharger on it.

The list of the modifications are as follow:

* FIC660 fuel injectors
* Motorcraft CX2391 MAP Sensor
* P1SC Procharger with a 3.625" Griptec pulley
* DW400 fuel pump
* AEM v3 water meth injection system

I'm new to tuning so I decided to take a step approach to doing this modifications in order to understand changes and iterate from a working state to a working state. At each step I will link the calibration file with the corresponding modifications so you can compare and understand the changes. For some steps I will add links relevant articles from the HPTuners forum. 

I started from the [stock calibration](./calibrations/1%20-%202017%20Ford%20Mustang%20V6%20Coupe%20-%203.7L%20-%20Stock.hpt) downloaded from the car before any modifications.

## MAP sensor:

This model uses a MAP sensor instead of a MAF. The factory MAP sensor is a 1 bar and as I'm adding boost I will need to replace the factory sensor with one that is able to measure above atmosferic pressure. To make things simpler I decided to use the sensor from an Ford Mustang I4 2.4L Ecoboost. These can be easily purchased and more importantly you can find out the required parameters to make it work from an [ecoboost stock calibration]() that you cand download from the HPTuners tune repository.



## Injector characterization

I purchased FIC660 injectors as they have good reputation for having realiable injector characterization data. You can download your data for the Ford ECU from their site for your specific injectors and adjust your calibration 

## Open vs Close loop tuning

This car comes with wideband O2 sensors fitted which enables the engine to run in closed loop mode.

There are 2 main ways in which you can start tuning the vechicle.

### Closed loop mode

This is the default operation mode for this car. In this mode the ECU uses the wideband O2 sensors to achieve the command AFR. The ECU applies corrections to the AFR using fuel trims.

 `Short Term Fuel Trims (STFT)`: Instant corrections. The ECU uses this to correct differences between the commanded and the measured AFR.
 `Long Term Fuel Trims (LTFT)`: Accumulative corrections. Over time the ECU will accumulate STFT to LTFT so that corrections that are constantly required are moved here and the STFT go back or close to 0.

 Important: While tunning it might be desirable to disable `LTFT`. You can do so by going to:
 ```
Fuel -> Oxygen Sensors -> Long Term Fuel Trims -> LTFT = Disabled
```
With this configuration you would be using the short term fuel trims histogram to make adjustments.
### Open loop mode

You can disable close loop mode by setting the parameter that controls at which temperature the ECU will enable close looped mode to it's max value:
```
Fuel -> Oxygen Sensors -> Closed Loop Enable -> CL O2 Sensor Temp = 2259C
```

With this configuration you would be using the measured EQ err historgram to make adjustments.

```
EQerr = Commanded Lambda / Measured Lambda
```

## Torque model

[HPTuners thread explaining Ford's late model torque model](https://forum.hptuners.com/showthread.php?69606-Late-model-Ford-s-Torque-Control-ETC-System&highlight=Wheel+Error+Max)

### Wheel Tq Error Max

IPC stands for independent plausibility check. It's a built in check that verifies calculated torque from the airflow agaisnt our torque tables. When the calculated torque does not match the expected range.
  
This error accumulates and it can cause the engine to go into limp mode.

We should adjust this parameter to a large enough value that prevents this from happening, given our torque tables are correct.

`Torque Model -> Monitoring -> IPC -> Torque Monitors -> Wheel Tq Error Max -> 500,000.00-200,000.00`

### Pedal WOT

 `Airflow -> Electronic Throttle -> Pedal -> Peda Pos WOT Start`: control the transition from the Driver Demand Table to WOT
 
 `Airflow -> Electronic Throttle -> Pedal -> Peda Pos WOT Start`: this is the position at which the throttle body is at WOT


    
