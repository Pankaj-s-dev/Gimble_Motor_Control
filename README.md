# Gimble_Motor_Control

# Motor Control API Reference (P-NUCLEO-IHM03)

## Overview

This document maps GUI features (STM32 Motor Control Workbench /
Monitor) to MCSDK APIs.

Includes: - Function description - Parameters with units - Return
values - Practical notes

------------------------------------------------------------------------

## 1. START / STOP

### MC_StartMotor1

**Prototype:** `bool MC_StartMotor1(void);`

**Parameters:** None\
**Returns:** bool (true = success)

**Description:** Starts motor state machine (alignment → ramp-up → run).

------------------------------------------------------------------------

### MC_StopMotor1

`bool MC_StopMotor1(void);`

**Returns:** bool\
**Description:** Immediate stop (PWM disabled)

------------------------------------------------------------------------

### MC_ProgramSpeedRampMotor1

`void MC_ProgramSpeedRampMotor1(int16_t speed, uint16_t duration);`

  Parameter   Unit           Description
  ----------- -------------- --------------
  speed       dHz (0.1 Hz)   Target speed
  duration    ms             Ramp time

------------------------------------------------------------------------

## 2. SPEED FEEDBACK

### MC_GetMecSpeedAverageMotor1

`int16_t MC_GetMecSpeedAverageMotor1(void);`

**Unit:** dHz\
**Conversion:** RPM = (value × 60) / 10

------------------------------------------------------------------------

## 3. TORQUE CONTROL

### MC_SetCurrentReferenceMotor1

`void MC_SetCurrentReferenceMotor1(qd_t Iqd);`

  Field   Unit         Description
  ------- ------------ -------------
  Iq      A (scaled)   Torque
  Id      A (scaled)   Flux

------------------------------------------------------------------------

## 4. MODE CONTROL

### MC_SetControlModeMotor1

`bool MC_SetControlModeMotor1(MC_ControlMode_t mode);`

Modes: - MCM_SPEED_MODE - MCM_TORQUE_MODE

------------------------------------------------------------------------

## 5. VOLTAGE / TEMP / POWER

### MC_GetBusVoltage_V

`uint16_t MC_GetBusVoltage_V(void);` Unit: Volt

### MC_GetTemperatureMotor1

`int16_t MC_GetTemperatureMotor1(void);` Unit: °C

### MC_GetAveragePowerMotor1

`int16_t MC_GetAveragePowerMotor1(void);` Unit: Watt

------------------------------------------------------------------------

## 6. FAULTS

### MC_GetOccurredFaultsMotor1

`uint16_t MC_GetOccurredFaultsMotor1(void);`

### MC_GetCurrentFaultsMotor1

`uint16_t MC_GetCurrentFaultsMotor1(void);`

### MC_AcknowledgeFaultMotor1

`bool MC_AcknowledgeFaultMotor1(void);`

------------------------------------------------------------------------

## Notes

-   Speed unit is NOT RPM → it is dHz
-   Motor runs continuously unless stopped
-   Always call Start before control
