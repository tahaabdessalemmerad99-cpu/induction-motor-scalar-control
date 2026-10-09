# induction-motor-scalar-control
MATLAB/Simulink simulation of a three-phase induction motor using scalar control, PI regulation, PWM, and a MOSFET-based voltage-source inverter.


## Overview

This project presents the modeling and simulation of a **three-phase squirrel-cage induction motor drive** using **MATLAB/Simulink and Simscape Power Systems**.

The motor is supplied through a **MOSFET-based voltage-source inverter** fed by a **450 V DC voltage source**. The drive is controlled using a **scalar control strategy (V/f-based control)** combined with a **PI controller** and PWM-based switching.

The model was developed to study the dynamic behavior of the induction motor under changes in the speed reference and to analyze key electrical and mechanical variables such as rotor speed, stator current, stator flux, electromagnetic torque, and stator voltage.

---

## Project Objectives

The main objectives of this project are:

- Model a three-phase squirrel-cage induction motor.
- Implement a scalar control strategy for induction motor speed control.
- Generate the inverter switching signals using PWM.
- Control the drive using a PI controller.
- Study the dynamic response of the motor to speed-reference changes.
- Monitor electrical and mechanical quantities during simulation.
- Analyze the behavior of stator current, stator flux, electromagnetic torque, and rotor speed.

---

## System Architecture

The simulated drive consists of the following main stages:

```text
                    Speed Reference
                          │
                          ▼
                 ┌─────────────────┐
                 │ Scalar Control  │
                 │     + PI        │
                 └────────┬────────┘
                          │
                          ▼
                    PWM Generation
                          │
                          ▼
                ┌──────────────────┐
                │ MOSFET Inverter  │
                │    3-Phase       │
                └────────┬─────────┘
                         │
                         ▼
              ┌──────────────────────┐
              │ Induction Motor      │
              │  Squirrel-Cage       │
              └──────────┬───────────┘
                         │
                         ▼
              Electrical & Mechanical
                    Measurements
```

---

## Main Components

### Induction Motor

The model uses the **Asynchronous Machine – SI Units** block from the Simscape/Power Systems library.

Main motor characteristics configured in the model include:

| Parameter | Value |
|---|---:|
| Motor type | Squirrel-cage induction motor |
| Rated power | 1 kW |
| Rated voltage | 380 V |
| Frequency | 50 Hz |

---

### DC Voltage Source

The inverter is supplied by a:

**450 V DC voltage source**

which provides the DC-link voltage required by the power converter.

---

### MOSFET Inverter

A three-phase voltage-source inverter is implemented using **six MOSFET switching devices**.

The inverter converts the DC-link voltage into a controlled three-phase voltage supply for the induction motor.

The switching signals are generated using PWM.

---

## Scalar Control

The induction motor is controlled using a **scalar control strategy**.

The controller generates the required voltage magnitude and electrical frequency according to the speed reference.

The model contains a dedicated subsystem named:

`Commande Scalaire`

which implements the scalar-control calculations and generates the voltage reference used by the inverter.

---

## PI Controller

A PI controller is used within the control system to regulate the drive response.

The controller parameters implemented in the model are:

```text
Kp = 1.5
Ki = 6
```

A saturation block is also included to limit the controller output between:

```text
-70 and +70
```

This prevents the controller output from exceeding the defined operating range.

---

## Speed Reference

The simulation includes a change in the reference speed to evaluate the dynamic response of the drive.

The reference speed is initially set to:

```text
1000 rpm
```

and changes to:

```text
1500 rpm
```

at:

```text
t = 3 s
```

This allows the transient behavior of the motor and controller to be investigated.

---

## Measured Variables

The model provides measurements of several important drive variables:

### Rotor Speed

The rotor speed is monitored to evaluate the tracking performance of the speed-control system.

### Stator Current

The stator current is monitored to analyze the electrical response of the motor.

### Stator Flux

The model provides measurements of:

- Stator flux `φs_q`
- Stator flux `φs_d`

These signals can be used to evaluate the magnetic behavior of the motor.

### Electromagnetic Torque

The electromagnetic torque `Te` is monitored to analyze the mechanical response of the motor.

### Stator Voltage

The line voltage `Uab` is also measured during simulation.

---


## Simulation Workflow

The simulation follows the following sequence:

1. A speed reference is applied to the control system.
2. The scalar-control subsystem processes the reference.
3. The PI controller regulates the control signal.
4. PWM signals are generated.
5. The six MOSFET switches operate the three-phase inverter.
6. The inverter supplies the induction motor.
7. Motor electrical and mechanical variables are measured.
8. The motor response is analyzed following changes in the speed reference.

---


## Author

**Taha Abdessalem Merad**
