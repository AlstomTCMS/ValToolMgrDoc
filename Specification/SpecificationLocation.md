Specification of location descriptor
=========================================

Introduction
------------------------

This document aims to exhaustively describe Multiple Unit target addressing, and, in a more generic point of view, how to address a multiple Targetting environment.

Solution proposal shall adress teams usages and points of view, allowing some customization without breaking compatibility.

Identified usages
------------------------

In order to simplify comparison, we use a standardized train configuration, made with following equipments:
 * MPU1;
 * MPU2;
 * ENV : for LV schemes and simulated equipments.

### Parts common for all teams ###

This configuration is identified as identical on all sites. As a consequence, there are written hereafter as a reminder.

Target to address | Physical equipment | path to address                      | Nickname usage
----------------- | ------------------ | ------------------------------------ | ------------------
Section1/MPU1     | MPU1 of Section 1  | /path/to/my/variable/inside/software | #VariableNickname
Section1/MPU2     | MPU2 of Section 1  | /path/to/my/variable/inside/software | #VariableNickname
Section2/MPU1     | MPU1 of Section 2  | /path/to/my/variable/inside/software | #VariableNickname
Section2/MPU2     | MPU2 of Section 2  | /path/to/my/variable/inside/software | #VariableNickname
Section3/MPU1     | MPU1 of Section 3  | /path/to/my/variable/inside/software | #VariableNickname
Section3/MPU2     | MPU2 of Section 3  | /path/to/my/variable/inside/software | #VariableNickname
Section4/MPU1     | MPU1 of Section 4  | /path/to/my/variable/inside/software | #VariableNickname
Section4/MPU2     | MPU2 of Section 4  | /path/to/my/variable/inside/software | #VariableNickname


### **Belfort** team ###

#### Description ####

Testbenches environments are configured to handle two units (called sections) at the same time, in order to use only one physical testbench for two sections, in order to limit required hardware (testbenches). It requests that these environment are of light complexity.

#### Result on sequence modelling ####

As two unit are present on the same physical equipment, they must be differentiated through their path, as shown on hereafter table.

Target to address   | Physical equipment           | path to address                                | Nickname usage
------------------- | ---------------------------- | ---------------------------------------------- | ---------------------------
Section1/ENV        | Testbench1 for Sections 1+2  | /SECTION1/path/to/my/variable/inside/software  | #SECTION1_VariableNickname
Section2/ENV        | Testbench1 for Sections 1+2  | /SECTION2/path/to/my/variable/inside/software  | #SECTION2_VariableNickname
Section3/ENV        | Testbench2 for Sections 3+4  | /SECTION1/path/to/my/variable/inside/software  | #SECTION1_VariableNickname
Section4/ENV        | Testbench2 for Sections 3+4  | /SECTION2/path/to/my/variable/inside/software  | #SECTION2_VariableNickname

### **La Rochelle** team ###

#### Description ####

Testbenches environments are configured to handle only one unit. It corresponds to a standard configuration, used also on other teams from other sites. It requests that these environment are of average complexity.

#### Result on sequence modelling ####

As one unit are present on the same physical equipment, table looks like a physical equipment.

Target to address | Physical equipment     | path to address                       | Nickname usage
----------------- | ---------------------- | ------------------------------------- | ------------------
Unit1/ENV         | Testbench1 for Unit 1  | /path/to/my/variable/inside/software  | #VariableNickname
Unit2/ENV         | Testbench2 for Unit 2  | /path/to/my/variable/inside/software  | #VariableNickname
Unit3/ENV         | Testbench3 for Unit 3  | /path/to/my/variable/inside/software  | #VariableNickname
Unit4/ENV         | Testbench4 for Unit 4  | /path/to/my/variable/inside/software  | #VariableNickname

### **Reichshoffen** team ###

#### Description ####

Testbenches environments are configured to handle ***only partially*** one unit at the same time. It corresponds to a specific configuration, used mainly for very complex environments, which cannot stand on a single testbench.

#### Result on sequence modelling ####

As one unit is partially represented, these are splitted through testbenches. Split of environment is performed in order to have almost equal load on every testbench. Actually, environment of other sections are simulated with a basic environment (usually, some interfaces, and basic functions), so that only one testbench is required for other sections.

Target to address | Physical equipment             | path to address                       | Nickname usage
----------------- | ------------------------------ | ------------------------------------- | ------------------
Unit1/ENV         | Testbench1 for car A of Unit 1 | /path1/to/my/variable/inside/software | #VariableNickname
Unit1/ENV         | Testbench2 for car B of Unit 1 | /path2/to/my/variable/inside/software | #VariableNickname
Unit2/ENV         | Testbench3 for Unit 2          | /path/to/my/variable/inside/software  | #VariableNickname
Unit3/ENV         | Testbench4 for Unit 3          | /path/to/my/variable/inside/software  | #VariableNickname
Unit4/ENV         | Testbench5 for Unit 4          | /path/to/my/variable/inside/software  | #VariableNickname

Synthesis
--------------------------------------------

Usages are clearly different from one team to another. As a generic rule, three cases must by differentiated. These are presented hereafter.

### Main case ###

Most used configuration is also the simplest configuration. It consists of a ONE-TO-ONE association : one testbench computer is holding only one environment. 

It is also usefull to to note that in the case of ***Reichshoffen***, this scheme is also applicable, but just for trailer units (e.g. units 1, 2, 3).

### Specific cases ###

#### One unit to many testbenches association ####

Although no examples are available, it can be expected following two processes:
 1. ***Explicit adressing :*** Name of environment is specified through its name a ONE-TO-ONE association : for example *Unit1/ENV_CAR_A* is adressing TestBench 1, simulating CAR A of unit 1.
 2. ***Implicit adressing :*** Name of environment can lead to variables on several testbenches. As a consequence, a second discriminator is used : *path* in the case of a variable, *nickname* in case of nickname variable.
 
#### Many units to one testbench association ####

Following two processes can be expected:
 1. ***Explicit adressing :*** Environment name and exact path/nickname are specified. In this case, no more processes are needed, because variables can be differentiated.
 2. ***Implicit adressing :*** Environment name and a partial path/nickname is specified, in order to not have to change path/nickname because of environment. *Path* or *nickname* is recreated through specific rules.
 
Specification
------------------------------------------

### Requirements ###

Based on synthesis, following requirements are applicable:
 1. Unit configuration can be specified unit per unit;
 2. Unit configuration can handle three following associations:
    * One to One testbench association
    * One unit to many testbenches association : both explicit adressing and implicit adressing shall be handled.
	* Multiple unit to one testbench association : both explicit adressing and implicit adressing shall be handled.
 3. Configuration of real equipments are also defined, because it is possible to access equipments through multiple systems : *TrainTracer* and *ControlBuild*
	
### Proposal ####

Configuration can be done through a XML file.
