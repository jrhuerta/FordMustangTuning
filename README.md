# FordMustangTuning

* The 3.7 comes fitted with O2 sensors for both banks.
* The ECU runs in closed loop all the time

## Open vs Close loop tuning
There are 2 main ways in which you can start tuning the vechicle.

### Open loop mode

`Fuel -> Oxygen Sensors -> Closed Loop Enable`: Setting value high enough (Max `2259C`) will prevent the ECU from going into closed loop mode.

With this configuration you would be using the measured EQ err = Commanded/Measured AFR to make adjustments.

### Closed loop mode

`Fuel -> Oxygen Sensors -> Long Term Fuel Trims` and set it to `Disabled`

With this configuration you would be using the short term fuel trims histogram to make adjustments.

## Torque model

[HPTuners thread explaining Ford's late model torque model](https://forum.hptuners.com/showthread.php?69606-Late-model-Ford-s-Torque-Control-ETC-System&highlight=Wheel+Error+Max)

### Wheel Tq Error Max
When the calculated torque does not match the expected range defined by:
- `Torque Model -> Monitoring -> IPC -> Torque Monitors -> Torque Maximun`
- `Torque Model -> Monitoring -> IPC -> Torque Monitors -> Torque Minimun`
  
This error accumulates and it can cause the engine to go into limp mode.

Adjusting this value prevents this from happening
`Torque Model -> Monitoring -> IPC -> Torque Monitors -> Wheel Tq Error Max -> 500,000.00-200,000.00`

### Pedal WOT

 `Airflow -> Electronic Throttle -> Pedal -> Peda Pos WOT Start`: control the transition from the Driver Demand Table to WOT
 
 `Airflow -> Electronic Throttle -> Pedal -> Peda Pos WOT Start`: this is the position at which the throttle body is at WOT


    
