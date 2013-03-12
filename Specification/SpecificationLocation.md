# Specification of location descriptor #

## Introduction ##

This document aims to exhaustively describe Multiple Unit target addressing, and, in a more generic point of view, how to address a multiple Targetting environment.

Solution proposal shall adress teams usages and points of view, allowing some customization without breaking compatibility.

## Identified usages ##

In order to simplify comparison, we use a standardized train configuration, made with following equipments:
 * MPU1;
 * MPU2;
 * ENV : for LV schemes and simulated equipments.

### Belfort team ###

#### Description ####

Testbenches environments are configured to handle two units (called sections) at the same time, in order to use only one physical testbench for two sections, in order to limit required hardware (testbenches).

#### Result on sequence modelling ####

As two unit are present on the same physical equipment, they must be differentiated through their path, so we have to address independently these 

Target to address   | Physical equipment           | path to address                                | Nickname usage
------------------- | ---------------------------- | ---------------------------------------------- | ---------------------------
Section1/MPU1       | MPU1 of Section 1            | /path/to/my/variable/inside/software           | #VariableNickname
Section1/MPU2       | MPU2 of Section 1            | /path/to/my/variable/inside/software           | #VariableNickname
Section2/MPU1       | MPU1 of Section 2            | /path/to/my/variable/inside/software           | #VariableNickname
Section2/MPU2       | MPU2 of Section 2            | /path/to/my/variable/inside/software           | #VariableNickname
Section3/MPU1       | MPU1 of Section 3            | /path/to/my/variable/inside/software           | #VariableNickname
Section3/MPU2       | MPU2 of Section 3            | /path/to/my/variable/inside/software           | #VariableNickname
Section4/MPU1       | MPU1 of Section 4            | /path/to/my/variable/inside/software           | #VariableNickname
Section4/MPU2       | MPU2 of Section 4            | /path/to/my/variable/inside/software           | #VariableNickname
Section1/ENV        | Testbench1 for Sections 1+2  | /SECTION1/path/to/my/variable/inside/software  | #SECTION1_VariableNickname
Section2/ENV        | Testbench1 for Sections 1+2  | /SECTION2/path/to/my/variable/inside/software  | #SECTION2_VariableNickname
Section3/ENV        | Testbench2 for Sections 3+4  | /SECTION1/path/to/my/variable/inside/software  | #SECTION1_VariableNickname
Section4/ENV        | Testbench2 for Sections 3+4  | /SECTION2/path/to/my/variable/inside/software  | #SECTION2_VariableNickname
