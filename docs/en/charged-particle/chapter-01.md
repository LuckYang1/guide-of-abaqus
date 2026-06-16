# Chapter 1 – Introduction

## Welcome

Welcome to CST Studio Suite for Particle Dynamics Simulation, the powerful and easyto-use electromagnetic field and charged particle dynamics simulation software. This program combines a user-friendly interface with high simulation performance.

Please refer to the CST Studio Suite Getting Started manual first. The following explanations assume that you have already installed the software and familiarized yourself with the basic concepts of the user interface.

## How to Get Started Quickly

We recommend that you proceed as follows:

1. Read the CST Studio Suite - Getting Started manual.  
2. Work through this document carefully. It provides all the basic information necessary to understand the advanced documentation.  
3. Look at the examples provided in the Component Library (File: Component Library  Examples). Especially the examples which are tagged as Tutorial provide detailed information of a specific simulation workflow. Press the Help button of the individual component to get to the help page of this component. Please note that all these examples are designed to give you a basic insight into a particular application domain. Real-world applications are typically much more complex and harder to understand if you are not familiar with the basic concepts.  
4. Start with your own first example. Choose a reasonably simple example, which will allow you to quickly become familiar with the software.  
5. After you have worked through your first example, contact technical support for hints on possible improvements to achieve even more efficient usage of the software.

## CST Studio Suite for Particle Dynamics Simulation

CST Studio Suite for Particle Dynamics Simulation is a fully featured software package for the design and analysis of electromagnetic components for accelerating and guiding charged particle beams. It simplifies the structure generation by providing a powerful solid modeling front end based on the industry-standard ACIS modeling kernel. Strong graphical feedback simplifies the definition of your device even further. After the component has been modeled, a fully automatic meshing procedure (based on an expert system) is applied for the electromagnetic computation before the simulation engine is started.

The simulators support the Perfect Boundary Approximation (PBA) feature, which increases the accuracy of the electromagnetic simulation significantly in comparison to conventional simulators. To calculate electromagnetic fields and analyze particle dynamics this software contains four different solvers: a time domain Wakefield simulator, a time domain Electromagnetic Particle-in-Cell solver, an Electrostatic Particle-in-Cell solver and a Particle Tracking solver.

Additionally, CST Studio Suite for Thermal and Mechanical Simulation allows subsequent multiphysical analysis.

If you are unsure which solver best suits your needs, contact your local sales office for further assistance.

Each solver's simulation results can be visualized with a variety of different options. Again, a strongly interactive interface will help you to achieve the desired insight into your device quickly.

The last – but not least – outstanding feature is the full parameterization of the structure modeler, which enables the use of variables in the definition of your component. In combination with the built-in optimizer and parameter sweep tools, CST Studio Suite for Particle Dynamics Simulation is capable of both the analysis and design of particle accelerating devices.

## Who Uses CST Studio Suite for Particle Dynamics Simulation?

Anyone who has to deal with electromagnetic problems that involve the effect of charged particle dynamics will greatly benefit from using CST Studio Suite. The program is especially suited to the fast, efficient analysis and design of components like electron guns, deflecting devices, guiding configurations and more. Since the underlying method is a general 3D approach, CST Studio Suite for Particle Dynamics Simulation can solve virtually any field problem that involves interaction with charged particles.

The software is based on an electromagnetic solving method, which requires the discretization of the entire calculation volume; for this reason the applications are limited only by the complexity of the structure.

## Key Features for Particle Dynamics Simulation

The following list gives you an overview of the main features for this part of CST Studio Suite. Please note that not all of these features may be available to you because of license restrictions. Please contact a sales office for more information.

## General

 Graphical user interface for Windows 10, Windows Server 2016/2019, Windows 11 and Windows Server 2022  
 The structure can be viewed either as a 3D model or as a schematic. The latter allows a parametrized approach of coupled simulation with our System Assembly and Modeling workflow.  
 Various independent solver strategies allow accurate results with a high performance  
 For specific solvers, highly advanced numerical techniques offer features like Perfect Boundary Approximation (PBA) ® for hexahedral grids and curved and higher order elements for tetrahedral meshes

## Structure Modeling

 Advanced ACIS-based, parametric solid modeling front end with excellent structure visualization  
 Feature-based hybrid modeler allows quick structural changes  
 Import of 3D CAD data from ACIS SAT (e.g. AutoCAD®), ACIS SAB, Autodesk Inventor®, IGES, VDA-FS, STEP, Pro/ENGINEER®, CATIA®, Siemens NX, Parasolid, Solid Edge, SolidWorks, CoventorWare®, Mecadtron®, NASTRAN, STL or OBJ files  
 Import of 2D CAD data from DXF™, GDSII and Gerber RS274X, RS274D files  
 Import of EDA data from design flows including Cadence Allegro® / APD® / SiP®, Mentor Graphics HyperLynx®, Zuken CR-5000® / CR-8000®, IPC-2581 and ODB++® (e.g. Altium Designer, Mentor Graphics Expedition / PADS / Boardstation®, CADSTAR®, Visula®)  
 Import of PCB designs originating from CST PCB Studio®  
 Import of 2D and 3D sub models  
 Import of Agilent ADS® layouts  
 Import of Sonnet® EM models  
 Import of a visible human model dataset or other voxel datasets

 Export of CAD data to ACIS SAT, ACIS SAB, IGES, STEP, NASTRAN, STL, DXF™, GDSII, Gerber or POV files  
 Parameterization for imported CAD files  
 Material database  
 Structure templates for simplified problem setup

## Particle Tracking Simulator

 Arbitrary shaped particle source surfaces  
 Circular particle sources with spatially inhomogeneous current distribution  
 Particle interfaces for coupling of tracking/tracking or tracking/PIC simulations  
 ASCII emission data imports based on particle interfaces

 Static-, eigenmode- and multiple external field distributions as source fields  
 Support for hexahedral as well as linear and curved tetrahedral meshes  
 Import of tetrahedral and hexahedral source fields into simulations

 Space charge limited, plasma-sheath, thermionic (Child’s Law and Langmuir-Fry model), fixed and field-induced emission model  
 Oblique emission  
 Secondary electron emission induced by ions or electrons as material property  
 Optically stimulated electron emission  
 Material specific Monte-Carlo collision modelling:

o Volume ionization due to electron impact  
o Volume ionization due to ion impact  
o Neutral atom excitation due to electrons  
o Elastic collisions between electrons and neutral gas  
o Elastic collisions between ions and neutral gas

 Definable material transparency of sheets for particles  
 Consideration of space charge via gun iteration  
 Consideration of self-magnetic fields in gun iteration

 Analysis of extracted particle current and space charge  
 Monitoring of beam cross-section, phase-space diagram and other statistical data of the beam  
 Emittance calculation  
 Thermal coupling (export of thermal loss distribution from crashed particles)

 Automatic parameter studies using built-in parameter sweep tool  
 Automatic structure optimization for arbitrary goals using built-in optimizer  
 Network distributed computing for remote computations  
 Coupled simulations with the Thermal Solver from CST Studio Suite  
 Support of Linux batch mode

Note: some solvers features may be available for hexahedral or tetrahedral meshes only.

## Electrostatic Particle-in-Cell Simulator

 Arbitrary shaped particle source surfaces  
 Circular particle sources with spatially inhomogeneous current distribution  
 Volumetric particle source featuring Maxwellian distribution  
 Particle interfaces for coupling of tracking/tracking or tracking/PIC simulations  
 ASCII emission data imports based on particle interfaces

 Static-, eigenmode- and multiple external field distributions as source fields  
 Support for hexahedral as well as linear and curved tetrahedral meshes

 Import of tetrahedral and hexahedral source fields into simulations  
 Gaussian-, DC-, field induced- and explosive emission model  
 Oblique emission  
 Secondary electron emission induced by ions or electrons as material property  
 Material specific Monte-Carlo collision modelling:  
o Volume ionization due to electron impact  
o Volume ionization due to ion impact  
o Neutral atom excitation due to electrons  
o Elastic collisions between electrons and neutral gas  
o Elastic collisions between ions and neutral gas  
 Definable material transparency of sheets for particles  
 Analysis of extracted particle current and space charge  
 User defined excitation signals and signal database  
 Monitoring of beam cross-section, phase-space diagram and other statistical data of the beam  
 Particle Monitors on Solids or Boundaries including Energy Histogram  
 Phase space monitoring  
 Thermal coupling (export of thermal loss distribution from crashed particles)  
 Online visualization of intermediate results during simulation  
 Periodic boundary conditions for particles and the hexahedral field solver  
 Particle merging  
 PEC charging due to colliding particles  
 Automatic parameter studies using built-in parameter sweep tool  
 Automatic structure optimization for arbitrary goals using built-in optimizer  
 Network distributed computing for remote computations  
 Coupled simulations with the Thermal Solver from CST Studio Suite  
 Support of Linux batch mode  
 Single-GPU acceleration for hexahedral meshes (not all solver features are supported)

Note: some solvers features may be available for hexahedral or tetrahedral meshes only.

## Particle-in-Cell Simulator

 Arbitrary shaped particle source surfaces  
 Circular particle sources with spatially inhomogeneous current distribution  
 Circular particle source in open boundaries  
 Volumetric particle source featuring Maxwellian distribution  
 Gaussian-, DC-, field induced- and explosive emission model  
 Oblique emission  
 Particle interfaces for coupling of tracking and PIC simulations  
 ASCII emission data imports based on particle interfaces  
 Selection of active Particle Sources  
 Static-, eigenmode- and multiple external field distributions as additional source fields  
 Import of tetrahedral source fields  
 Automatic detection of multipaction breakdown  
 Thermal coupling (export of thermal loss distribution from crashed particles)  
 Periodic boundary conditions for particles

 Support for Single- / Multi-GPU acceleration

 Single node parallelization

 Support of Linux batch mode

 Online visualization of intermediate results during simulation  
 Calculation of field distributions as a function of time or at multiple selected frequencies from one simulation run  
 Time domain monitoring of particle position and momentum  
 Particle Monitors on Solids or Boundaries including Energy Histogram  
 Time domain monitoring of output power  
 Time domain monitoring of particle current density  
 Phase space monitoring  
 Emittance calculation  
 Secondary electron emission induced by ions or electrons as material property  
 Material specific volume ionization due to electron impact based on Monte-Carlo collision model  
 Definable material transparency of sheets for particles  
 Isotropic and anisotropic material properties  
 Frequency dependent material properties with arbitrary order for permittivity and permeability as well as a material parameter fitting functionality  
 Field-dependent microwave plasma and gyrotropic materials (magnetized ferrites)  
 Non-linear material models (Kerr, Raman)  
 Surface impedance models (tabulated surface impedance, Ohmic sheet, lossy metal, corrugated wall, material coating)  
 Frequency dependent multilayered thin panel materials (isotropic and symmetric)  
 Time dependent conductive materials  
 Port mode calculation by a 2D eigenmode solver in the frequency domain  
 Efficient calculation of higher order port modes by specifying target frequency  
 Automatic waveguide port mesh adaptation  
 Multipin ports for TEM mode ports with multiple conductors  
 User defined excitation signals and signal database  
 Charge absorbing open boundaries for CPU solver  
 High performance radiating/absorbing boundary conditions  
 Conducting wall boundary conditions  
 Calculation of various electromagnetic quantities such as electric fields, magnetic fields, surface currents, power flows, current densities, power loss densities, electric energy densities, magnetic energy densities, voltages or currents in time and frequency domain  
 Calculation of time averaged power loss volume monitors  
 Calculation of time averaged surface losses  
 Discrete edge and face elements (lumped resistors) as ports  
 Ideal voltage and current sources  
 Discrete edge and face R, L, C, and (nonlinear) diode elements at any location in the structure  
 Automatic parameter studies using built-in parameter sweep tool  
 Automatic structure optimization for arbitrary goals using built-in optimizer  
 Network distributed computing for remote computations  
 Support for Transient Co-Simulation with CST Design Studio™  
 Coupled simulations with the Thermal Solver from CST Studio Suite

## Wakefield Simulator

 Particle beam excitation for ultra-relativistic and non-relativistic beams

 Transmission line injection scheme (improved dispersion characteristics)  
 Arbitrary particle beam shapes for ultra-relativistic beams  
 Automatic wake-potential calculation  
 Automatic wake-impedance, loss and kick factor calculation  
 Wakefield postprocessor allows to recompute wake impedances  
 Mesh settings for particle beams  
 Direct and two indirect wake-integration methods available  
 MPI Cluster parallelization via domain decomposition  
 Support of Linux batch mode  
 Efficient calculation for loss-free and lossy structures  
 Calculation of field distributions as a function of time or at multiple selected frequencies from one simulation run  
 Adaptive mesh refinement in 3D  
 Isotropic and anisotropic material properties  
 Frequency dependent material properties  
 Gyrotropic materials (magnetized ferrites)  
 Surface impedance model for good conductors  
 Port mode calculation by a 2D eigenmode solver in the frequency domain  
 Automatic waveguide port mesh adaptation  
 Multipin ports for TEM mode ports with multiple conductors  
 High performance absorbing boundary conditions also for charged particle beams  
 Conducting wall boundary conditions  
 Calculation of various electromagnetic quantities such as electric fields, magnetic fields, surface currents, power flows, current densities, power loss densities, electric energy densities, magnetic energy densities, voltages or currents in time and frequency domain  
 Calculation of time averaged power loss volume monitors  
 Calculation of time averaged surface losses  
 Discrete edge and face elements (lumped resistors) as ports  
 Ideal voltage and current sources  
 Discrete edge and face R, L, C, and (nonlinear) diode elements at any location in the structure  
 Automatic parameter studies using built-in parameter sweep tool  
 Automatic structure optimization for arbitrary goals using built-in optimizer  
 Network distributed computing for optimizations, parameter sweeps and multiple port/mode excitations  
 Support for Transient Co-Simulation with CST Design Studio™  
 Coupled simulations with the Thermal Solver from CST Studio Suite

## Eigenmode Simulator

 Calculation of modal field distributions in closed loss-free or lossy structures  
 Support of hexahedral meshes as well as linear and curved tetrahedral meshes  
 Isotropic and anisotropic materials  
 Multithread parallelization  
 Adaptive mesh refinement in 3D using eigenmode frequencies as stop criteria, with True Geometry Adaptation  
 Periodic boundary conditions including phase shift

Calculation of losses and internal / external Q-factors for each mode (directly or using perturbation method)  
 Discrete L,C elements at any location in the structure  
 Target frequency can be set (calculation within the frequency interval)  
 Calculation of all eigenmodes in a given frequency interval  
 Sensitivity analysis with respect to materials and geometric deformations defined by face constraints (with tetrahedral mesh)  
 Automatic Lorentz force calculation  
 Introduction of a General (Lossy) solver  
 Support of Open Boundary conditions for accurate internal / external Q-factors calculation  
 Support Tetrahedral mesh only with automatic Adaptive mesh refinement  
 Automatic parameter studies using built-in parameter sweep tool  
 Automatic structure optimization for arbitrary goals using built-in optimizer  
 Network distributed computing for optimizations and parameter sweeps  
 Coupled simulations with the Thermal Solver from CST Studio Suite

## Electrostatics Simulator

 Isotropic and (coordinate-dependent) anisotropic material properties  
 Sources: potentials, charges on conductors (floating potentials), uniform volumeand surface-charge densities  
 Force calculation  
 Capacitance calculation  
 Electric / magnetic / tangential / normal / open / fixed-potential boundary conditions  
 Periodic boundary conditions for hexahedral meshes  
 Perfect conducting sheets and wires  
 Discrete edge capacitive elements at any location in the structure  
 Adaptive mesh refinement in 3D  
 Automatic parameter studies using built-in parameter sweep tool  
 Automatic structure optimization for arbitrary goals using built-in optimizer  
 Network distributed computing for optimizations, parameter sweeps and remote calculations  
 Coupled simulations with the Mechanical Solver from CST Studio Suite

## Magnetostatics Simulator

 Isotropic and (coordinate-dependent) anisotropic material properties  
 Nonlinear material properties  
 Laminated material properties  
 Sources: coils, permanent magnets, current paths, external fields, stationary current fields  
 Discrete edge inductances at any location in the structure  
 Force calculation  
 Inductance calculation  
 Flux linkages  
 Electric / magnetic / tangential / normal / open boundary conditions  
 Adaptive mesh refinement in 3D  
 Automatic parameter studies using built-in parameter sweep tool  
 Automatic structure optimization for arbitrary goals using built-in optimizer  
 Network distributed computing for optimizations, parameter sweeps and remote calculations  
 Coupled simulations with the Mechanical Solver from CST Studio Suite

## Visualization and Secondary Result Calculation

 Multiple 1D result view support  
 Import and visualization of external xy-data  
 Copy / Paste of xy-datasets  
 Fast access to parametric data by interactive tuning sliders  
 Automatic parametric 1D result storage  
 Displays port modes (with propagation constant, impedance, etc.)  
 Various field visualization options in 2D and 3D for electric fields, magnetic fields, power flows, surface currents, etc.  
 Animation of field distributions  
 Particle and secondary electrons vs. time 1D plots (PIC)  
 Collision event monitors for Monte-Carlo collisions  
 Current/Power 1D plot of emitted and absorbed particles (PIC)  
 Wave-Particle Power Transfer (PIC)  
 Animation of 2D and 3D particle positions / momenta (PIC)  
 Visualization of 3D particle trajectories (Tracking)  
 Combined Visualization of 2D/3D fields and particle positions (PIC)  
 Visualization of thermal loss distribution due to particle collisions with solids  
 Display of source definitions in 3D  
 Display of nonlinear material curves in xy-plots  
 Display of material distributions for materials with nonlinear permeability  
 Animation of field distributions  
 Display and integration of 2D and 3D fields along arbitrary curves  
 Integration of 3D fields across arbitrary faces  
 Hierarchical result templates for automated extraction and visualization of arbitrary results from various simulation runs. These data can also be used for the definition of optimization goals.

## Result Export

 Export of result data such as fields, curves, etc. as ASCII files  
 Export of particle data as ASCII files  
 Export screen shots of result field plots

## Automation

 Powerful VBA (Visual Basic for Applications) compatible macro language including editor and macro debugger  
 OLE automation for seamless integration into the Windows environment (Microsoft Office®, MATLAB®, AutoCAD®, MathCAD®, Windows Scripting Host, etc.)

## About This Manual

This manual is primarily designed to enable a quick start with CST Studio Suite for Particle Dynamics Simulation. It is not intended to be a complete reference guide to all the available features but will give you an overview of key concepts. Understanding these concepts will allow you to learn how to use the software efficiently with the help of the online documentation.

The main part of the manual is the Simulation Workflow (Chapter 2) which will guide you through the most important features of CST Studio Suite for Particle Dynamics Simulation. We strongly encourage you to study this chapter carefully.

## Document Conventions

 Buttons that should be pressed within dialog boxes are always written in italics, e.g. OK.  
 Key combinations are always joined with a plus (+) sign. Ctrl+S means that you should hold down the Ctrl key while pressing the S key.  
 The program’s features can be accessed through a Ribbon command bar at the top of the main window. The commands are organized in a series of tabs within the Ribbon. In this document a command is printed as follows: Tab name: Group name  Button name  Command name. This means that you should activate the proper tab first and then press the button Command name, which belongs to the group Group name. If a keyboard shortcut exists, it is shown in brackets after the command. Example: View: Change View  Reset View (Space)  
 The project data is accessible through the navigation tree on the left side of the application’s main window. An item of the navigation tree is referenced in the following way: NT: Tree folder  Sub folder  Tree item.  
 Example: NT: 1D Results  Port Signals  i1

## Your Feedback

We are constantly striving to improve the quality of our software documentation. If you have any comments regarding the documentation, please send them to your support center: 3DS.com/Support.
