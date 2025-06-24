[![version](https://img.shields.io/badge/version-1.0.0-blue)](https://github.com/ibarram/thermal-fluid-predictor/)
[![GitHub commit activity (branch)](https://img.shields.io/github/commit-activity/w/ibarram/thermal-fluid-predictor)](https://github.com/ibarram/thermal-fluid-predictor/)
[![GitHub discussions](https://img.shields.io/github/discussions/ibarram/thermal-fluid-predictor)](https://github.com/ibarram/thermal-fluid-predictor/discussions)
[![GitHub issues](https://img.shields.io/github/issues/ibarram/thermal-fluid-predictor)](https://github.com/ibarram/thermal-fluid-predictor/issues)
[![Readme-ES](https://img.shields.io/badge/README-Español-green.svg)](README_ES.md)
![Gitter](https://img.shields.io/gitter/room/ibarram/thermal-fluid-predictor)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

<br />
<div align="center">
  <a href="https://github.com/ibarram/thermal-fluid-predictor">
    <img src="/doc/img/escudo-png.png" alt="Logo" width="120" height="120">
  </a>

  <h3 align="center">thermal-fluid-predictor</h3>

  <p align="center">
    Experimental dataset and multi-language implementation for real-time fluid temperature prediction in gas-based water heaters using embedded systems.
    <br />
    <a href="https://github.com/ibarram/thermal-fluid-predictor"><strong>Explore the docs »</strong></a>
    <br />
    <br />
    <a href="https://github.com/ibarram/thermal-fluid-predictor">View Demo</a>
    ·
    <a href="https://github.com/ibarram/thermal-fluid-predictor/issues">Report Bug</a>
    ·
    <a href="https://github.com/ibarram/thermal-fluid-predictor/issues">Request Feature</a>
  </p>
</div>

<details><summary>Table of Contents</summary><p>
 
 * [Abstract](#abstract)

 * [Testbench](#testbench)

 * [Get the data](#get-the-data)

 * [Database](#database)

 * [Loading data](#loading-data)

 * [Implementations](#implementations)

 * [Benchmark](#benchmark)

 * [Publications](#publications)

 * [Contact](#Contact)

 * [Citing thermal-fluid-predictor database](#citing-thermal-fluid-predictor-database)

 * [License](#license)

</p></details><p></p>

## Abstract

Thermal Fluid Predictor is a cross-platform project for modeling and predicting fluid temperature behavior in real-time. The repository includes implementations in Python, MATLAB, C, and R, tailored for integration into energy-constrained embedded systems such as gas water heaters. It provides curated datasets, trained models, and system diagrams to support reproducible development, simulation, and deployment.

The dataset contains measurements of five variables obtained from the Rapid Recovery Water Heater. The sampling methodology is based on the “water state process.”

Each process has a total sampling duration of 12 minutes, divided into three distinct phases:

A. From 0 to 4 minutes, the water is heated (Heating).

B. From 4 to 8 minutes, the water temperatura is maintained and must not exceed a defined setpoint (Steady).

C. From 8 to 12 minutes, the system begins to cool down (Cooling).

Samples are recorded every 200 ms, which means that in each 4-minute phase we have 1,200 samples.

Each process includes three stages (Heating, Steady, and Cooling). After defining the stages, a water flow level is assigned(Zero, Low, or High); followed by a gas flow setting, (Zero, Low, or High). Finally, each process is carried out with two different initial water temperatures (Low and High). Therefore, the total number of data files is calculated as: 3 (Water flow levels) x 4 (Gas Flow levels) x 10 (Water processes) x 2 (Inlet temperatures) = 240 files.

## Testbench

The dataset was acquired in the Laboratory of Electrical Engineering, Division of Engineering at Irapuato-Salamanca Campus of the University of Guanajuato, Mexico.

The testbench consists of a Rapid Recovery Water Heater System that operates with LP gas, a Calorex COXDP-09 13 Lt/min, with a power supply of 2 batteries of 3V, one servo valve for control of LP gas supply.

<div align="center">
  <a href="https://github.com/ibarram/thermal-fluid-predictor">
    <img src="/doc/img/testbench_fullview.png" alt="testbenchfullview1" width="800" height="400">
  </a>


Figure 1. Above is a photograph of the test bench part 1 used to generate the database. This setup provides a visual representation of our data collection process. Left View of System | Front View of System | Right View of System.
