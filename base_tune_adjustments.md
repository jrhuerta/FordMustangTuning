Base Tune Adjustments
---

* FIC660 injector characterization

### CX2391 MAP Sensor
```
Airflow -> General -> Throttle Inlet Pressure -> Characteristics -> Slope =  9.555 psi 

Airflow -> General -> Throttle Inlet Pressure -> Characteristics -> Offset = -0.921 psi 
```

### Torque model
```
Torque Model -> Monitoring -> IPC -> Torque monitors -> Wheel Tq Error Max = 200K-500K
```
This is a cummulative error for when calculated torque doesn't match the expected one.

Questions: 
* Torque Maximun and Torque Minium tables?

```
Torque Model -> General -> Torque Calculation -> Engine Torque X
```
Torque x Engine Load x RPM for Mapped Point X

```
Torque model -> General -> Torque Calculation -> Inverse X
```

Engine Load x Torque x RPM for Mapped Point X

* The `Engine Torque` tables need to be adjusted
* Once the Engine Torque Table X is adjusted we need to update the corresponding `Inverse`
* This tables need to be re-normalized on the load axis when adding forced induction because due to boost the engine will be seen loads greater than 1.0

### WOT pedal position
```
Airflow -> Electronic Throttle -> Pedal -> Pedal Pos WOT Start = 80%
```

### Torque management
```
Torque management -> General -> Maximun torque -> Max gross 
```
All cells are already maxed
```
Torque management -> General -> Maximun torque -> 2A, 3A, B, OP 2A, OP 3A, OP B
```
Multiply table values by 2x

```
Torque management -> Driver demand -> Desired Torque -> Normal -> PRN1, 2, 3, 4, 5, 6
```
If the calculated torque exceeds the values in this table the ECU might close the throttle body. In these tables we are going to want to focus on the lower end of the tables particulary if we are coming from an NA to a force induction calibration.

Questions:
* Scheduled torque max = 2A, 3A, B, OP 2A, OP 3A, OP B?
* Torque max vs RPM = Max gross?

### Power Enrichment

```
Fuel -> Power Enrich -> Throttle -> Fuel Enrichment Pedal
```
This able defines what percentage of throttle we need to exceed to operate on power enrichment mode.

For a forced induction application we whould modify this so that as at higher RPMs where we are producing boost less pedal is required to maintain power enrichment mode.

```
Fuel -> Power Enrich -> Power Enrichment -> WOT Lambda
```
This table dictates the target lambda while running on power enrichment mode.
To start tuning this should be set to a safe value. 0.8 lambda (20% rich) is a good starting point for a boosted application
This table will be dialed during the tunning process.

```
Fuel -> Power Enrich -> Power Enrichment -> Enrichment Rate = 0.5 lambda/sec
```
This parameter determines how fast can he ECU increase the fuel rate to reach the desired lambda

### Spark

```
Spark -> Advance -> Borderline
```

```
Spark -> Advance -> MBT
```