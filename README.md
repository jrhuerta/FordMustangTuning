# FordMustangTuning

* The 3.7 comes fitted with O2 sensors for both banks.
* The ECU runs in closed loop all the time

## Oven vs Close loop tuning
There are 2 main ways in which you can start tuning the vechicle.

* Disabling closed loop mode
* You can do so by going to `Fuel -> Oxygen Sensors -> Closed Loop Enable` and setting value high enough `2259C` so that the ECU never goes into closed loop.
* With this configuration you would be using the EQ err = Commanded/Measured AFR to make adjustments.

* Using short term fuel values to correct the calibration
* Disable LTFT by going to `Fuel -> Oxygen Sensors -> Long Term Fuel Trims` and set it to `Disabled`
* Use the short term fuel trims histogram to make adjustments.


## Torque model

[HPTuners thread explaining Ford's late model torque model](https://forum.hptuners.com/showthread.php?69606-Late-model-Ford-s-Torque-Control-ETC-System&highlight=Wheel+Error+Max)

### Wheel Tq Error Max
When the calculated torque does not match the expected range defined by the `Torque Model -> Monitoring -> IPC -> Torque Monitors -> Torque Maximun` and the `Torque Model -> Monitoring -> IPC -> Torque Monitors -> Torque Minimun` this error accumulates and it can cause the engine to go into limp mode.

Adjusting this value prevents this from happening
`Torque Model -> Monitoring -> IPC -> Torque Monitors -> Wheel Tq Error Max -> 500,000.00-200,000.00`

    
