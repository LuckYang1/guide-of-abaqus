# Trademarks and Legal Notices

## Trademarks

Abaqus, 3DEXPERIENCE , the 3DS logo, the Compass icon, IFWE, 3DEXCITE, 3DVIA, BIOVIA, CATIA, CENTRIC PLM, DELMIA, ENOVIA, GEOVIA, MEDIDATA, NETVIBES, OUTSCALE, SIMULIA and SOLIDWORKS are commercial trademarks or registered trademarks of Dassault Systèmes, a European company (Societas Europaea) incorporated under French law, and registered with the Versailles trade and companies registry under number 322 306 440, or its subsidiaries in the United States and/or other countries. All other trademarks are owned by their respective owners. Use of any Dassault Systèmes or its subsidiaries trademarks is subject to their express written approval.

## Legal Notices

Abaqus and this documentation may be used or reproduced only in accordance with the terms of the software license agreement signed by the customer, or, absent such agreement, the then current software license agreement to which the documentation relates.

This documentation and the software described in this documentation are subject to change without prior notice.

Dassault Systèmes or its Affiliates shall not be responsible for the consequences of any errors or omissions that may appear in this documentation.

© Dassault Systèmes Americas Corp., 2025.

For a full list of the third-party software contained in this release, please go to the Legal Notices in the Abaqus 2025 HTML documentation, which can be obtained from a documentation installation, or in the SIMULIA Established Products 2025 Program Directory, which is available on www.3ds.com.

## Abaqus/CAE User's Guide

The Abaqus/CAE User's Guide is a complete reference to using Abaqus/CAE.

This guide is a part of the Abaqus® documentation collection, which describes all the capabilities of the Abaqus finite element analysis technology used in SIMULIA  applications.

Detailed descriptions of how to use Abaqus/CAE for model generation, analysis, and results evaluation and visualization are provided. Abaqus/Viewer users should refer to the information on the Visualization module in this guide.

## What's New

This page describes recent changes in Abaqus/CAE.

## 2025 FD01

## Animation File Formats

You can now save and load animations in MP4 and animated GIF formats in Abaqus/CAE.

Benefits: New file formats offer improved compatibility with modern media players and editing software, as well as HTML5 and common applications for producing presentations. The file size can be significantly smaller, with no appreciable loss of quality.

You can save MP4 animations with the MPEG-4 codec. If you have an installation of the FFmpeg program that supports H.264 encoding on your system, you can save MP4 animations using the H.264 codec.

For more information, see Choosing the animation file format and Using background images and movies.

## PDF Guides Available

You can download PDF versions of the Abaqus guides from each guide overview.

Benefits: You can easily access the PDF versions of the guides.

In earlier releases, PDF versions of the guides were updated only for the GA (General Availability) release and could be downloaded from the Dassault Systèmes Knowledge Base. As of 2025 FD01, the PDF guides will be updated with each release of the HTML versions of the guides.

For more information, see Abaqus/CAE User's Guide.

## 2025 GA

## AutoCAD DXF Sketch Import

Users can now import polylines, splines, ellipses, and other complex entities from AutoCAD files.

Benefits: The import of .dxf files as sketches in Abaqus/CAE is greatly improved.

For more information, see Importing sketches.

## Wear Modeling in Abaqus/CAE

Abaqus/CAE now supports the wear surface property and its assignment in general contact interactions.

Benefits: The support allows greater flexibility for modeling wear phenomena in Abaqus/CAE without having to use the keyword editor.

For more information, see Specify wear surface property assignments and Defining a wear interaction property.

## Rotordynamic Loads in Abaqus/CAE

Abaqus/CAE now supports rotordynamic loads as a rotational body force type in Abaqus/CAE.

Benefits: This support allows greater flexibility to define a rotordynamic load as a rotational body force in Abaqus/CAE without having to use the keyword editor.

For more information, see Defining a rotational body force.

## Step Dependence for Fluid Inflator and Fluid Exchange

Abaqus/CAE now supports the activation of fluid inflators and fluid exchange in steps.

Benefits: This support allows greater flexibility for modeling the inflator and cavity exchange in Abaqus/CAE without having to use the keyword editor.

Earlier releases of Abaqus/CAE supported automatic activation in Abaqus/Explicit steps, offering no flexibility to the user.

For more information, see Defining a fluid inflator activation interaction and Defining a fluid exchange activation interaction.

## Modeling Cracks and Seams

Abaqus/CAE now supports the creation of a seam on a dependent part instance.

Benefits: Seam creation on a dependent part instance allows greater flexibility when modeling seams for fracture simulation in Abaqus/CAE.

Earlier releases of Abaqus/CAE supported seam creation only for independent instances.

For more information, see The Special menu in the Interaction module.

## 2024 FD03

## State Space Solver for Transient Modal Dynamic Analysis

The new state space solver for transient modal dynamic analysis of systems with nondiagonal modal damping operators is now the default solver in Abaqus/CAE.

Benefits: The state space solver is unconditionally stable and offers improved performance for models with many time increments and a moderate number of modes.

In earlier releases, the conventional solver was the default for transient modal dynamic analysis in Abaqus/CAE. Now, you must use the keywords editor to access the conventional solver in Abaqus/CAE.

For more information, see Transient Modal Dynamic Analysis.

## Job Execution Using 3DEXPERIENCE On-Cloud Licensing

When you launch Abaqus/CAE from the 3DEXPERIENCE Platform Connector for Abaqus/CAE, you can now specify that jobs should execute using the 3DEXPERIENCE Platform license server instead of a locally installed license server.

Benefits: You can take advantage of available cloud SIM Unit licenses to execute an Abaqus analysis locally.

For more information, see Setting the license type for the SimUnit license model.

## 2024 GA

## Python 3

Abaqus Python and Abaqus/CAE are now based on Python 3.10 instead of Python 2.7.

Benefits: This update brings Abaqus Python into conformance with a version of Python that is supported in the open-source community.

For more information, see https://go.3ds.com/AbaqusPython.

## Render Styles in Plots for Continuum Particle Elements

Abaqus/CAE now supports visualization of element particle edges with wireframe, hidden, filled, and shaded render styles (View > ODB Display Options).

Benefits: The ability to assign different render styles makes it easier to distinguish between continuum particle elements.

For more information, see Output, Output, and Controlling the display of model entities.

## Step-Dependent General Contact

Abaqus/CAE now supports the definition of general contact in Abaqus/Standard in any analysis step or in the initial step.

Benefits: Defining general contact in analysis steps enables definition of more complex contact behaviors in Abaqus/Standard simulations.

For more information, see Defining general contact and About General Contact in Abaqus/Standard.

## Contact Mass Scaling

Abaqus/CAE now supports the definition of contact mass scaling in Abaqus/Explicit.

Benefits: Contact mass scaling can reduce the number of increments required for Abaqus/Explicit simulations that use nondefault penalty stiffness.

You can apply mass scaling to the contact surfaces or elements involved in the contact definition. Contact mass scaling reduces the impact of higher-than-default contact penalty stiffness on the global stable time increment in an Abaqus/Explicit analysis by increasing the mass associated with the contact surfaces.

For more information, see Defining contact mass scaling and \*CONTACT MASS SCALING.

## Channel and Hat Section Profiles

You can now define channel and hat section profiles in the Property module.

Benefits: The addition of channel and hat profiles simplifies the specification of these common beam cross-sections in Abaqus/CAE.

For more information, see Defining a channel profile, Defining a hat profile, ChannelProfile object, HatProfile object, and Beam cross-section analysis.

## Beam Section Offset for \*BEAM SECTION

Abaqus/CAE now supports the definition of a beam section offset for beam sections integrated during the analysis (\*BEAM SECTION).

Benefits: Beam offsets allow greater flexibility when modeling with beam elements in Abaqus/CAE. Earlier releases of Abaqus/CAE supported beam section offsets only for \*BEAM GENERAL SECTION.

For more information, see \*BEAM SECTION, Using a Beam Section Integrated during the Analysis to Define the Section Behavior, and BeamSection object.

## Rotational Couplings

You can now define a rotational coupling type in discrete fasteners and coupling constraints in Abaqus/CAE.

Benefits: Defining the rotational coupling type gives you greater control over the behavior of distributing couplings involving cloud nodes with rotational degrees of freedom.

For more information, see \*DISTRIBUTING, Creating discrete fasteners, and Defining coupling constraints.

## Using the Linearized Contact Capability to Solve for Contact Status and Contact Stresses

Abaqus/CAE now supports the activation of the linearized contact capability to solve for contact status and contact stresses within a static perturbation step with small-sliding, frictionless contact.

Benefits: The Linear Complementarity Problem (LCP) solution technique provides a faster solution for certain classes of contact problem.

For more information, see Configuring a static, linear perturbation procedure and \*SOLUTION TECHNIQUE.

---

[Previous: Overview and Contents](overview.md) · [Next: Interacting with Abaqus/CAE](interacting.md)
