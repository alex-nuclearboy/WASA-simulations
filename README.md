# Simulation of reactions in the WASA-at-COSY experiment

This repository contains the source code for simulating nuclear reactions in the WASA-at-COSY experiment. 
The software is designed to simulate proton-deuteron fusion reactions. 

All files are distributed under the terms of the GNU General Public Licence Version 3.

## Simulation Software

### ROOT 
ROOT is an object-oriented framework for large-scale data analysis based on C++. It was originally developed for particle physics data analysis at CERN. 
ROOT provides an extensive library with modules for physics, mathematics, statistics, histograms, and graphics. It also offers powerful statistical tools for data analysis.

### PLUTO
PLUTO is a simulation framework for heavy ions and hadronic physics built on the ROOT environment. Initially developed by the HADES collaboration at GSI, PLUTO provides a library of C++ classes for simulating various reactions in particle physics. 
It includes models for resonance and Dalitz decays, resonance spectral functions with mass-dependent widths, and anisotropic angular distributions for selected channels. 
PLUTO simulations generate output files in the ROOT format, containing the four-vectors of all final-state particles and decay vertices. 
Note that PLUTO does not account for any detector effects. The output of a PLUTO simulation serves as input for the WASA Monte Carlo simulation program.

### WASA Monte Carlo (WMC)
WMC is a software package based on the GEANT3 package developed at CERN. It is used to determine the detector's response to particles generated by PLUTO simulations. 
Using physical models, WMC calculates signals from different detector elements.

## Environment Variables

Before running the simulations, ensure the following environment variables are set:

- `ROOTSYS`: path to the ROOT installation.
- `PLUTOSYS`: path to the PLUTO installation.
- `WASA_ROOT`: path to the WMC installation.
- `PLUTO_OUTPUT`: path to store resulting files after running PLUTO simulations.
- `WMC_DATA`: path to store resulting data after running WMC simulations.

## Getting Started

Follow these steps to compile and run the simulation:

    # Clone the repository to your local machine
    git clone https://github.com/alex-nuclearboy/WASA-Simulations.git
    # Configure the WMC package in accordance with the experimental setup used in the project
    cd WASA-Simulations/config
    ./apply_geometry.sh
    # Navigate to the working directory
    cd ../pluto/basic-reactions
    # Create a directory for building the project
    mkdir build && cd build
    # Run CMake to configure the project
    cmake ..
    # Build the project
    make
    # Return to the main directory
    cd ..

## Running the simulation

To run the simulation, follow these steps:

- Start by running the simulation for your desired reaction. Replace <reaction_products> with the appropriate reaction products input (e.g., "p d"):
  
      ./generator <reaction_products>

- Next, navigate to the WASA Monte Carlo directory:

      cd ../wmc

- Run the WMC simulation by replacing <reaction> with the appropriate reaction input (e.g., "pd-pd"):

      ./wmc_run.sh <reaction>

The simulated data generated by this software can be used for analysis in two repositories:

- for analysis tools and scripts related to luminosity calculations, please refer to the [LuminosityDetermination](https://github.com/alex-nuclearboy/LuminosityDetermination) repository.

- for analysis and visualisation the decay of mesic bound state, pleae explore the [BoundStateAnalysis](https://github.com/alex-nuclearboy/BoundStateAnalysis) repository.
