---
title: Trademarks and Legal Notices
description: Abaqus Execution Guide chapter
---

# Trademarks and Legal Notices

## Trademarks

Abaqus, 3DEXPERIENCE, the 3DS logo, the Compass icon, IFWE, 3DEXCITE, 3DVIA, BIOVIA, CATIA, CENTRIC PLM, DELMIA, ENOVIA, GEOVIA, MEDIDATA, NETVIBES, OUTSCALE, SIMULIA, and SOLIDWORKS are commercial trademarks or registered trademarks of Dassault Systèmes, a European company (Societas Europaea) incorporated under French law and registered with the Versailles trade and companies registry under number 322 306 440, or its subsidiaries in the United States and/or other countries. All other trademarks are owned by their respective owners. Use of any Dassault Systèmes or its subsidiaries trademarks is subject to their express written approval.

## Legal Notices

Abaqus and this documentation may be used or reproduced only in accordance with the terms of the software license agreement signed by the customer, or, absent such agreement, the then current software license agreement to which the documentation relates.

This documentation and the software described in this documentation are subject to change without prior notice. Dassault Systèmes and its Affiliates shall not be responsible for the consequences of any errors or omissions that may appear in this documentation.

© Dassault Systèmes Americas Corp., 2025.

For a full list of the third-party software contained in this release, please refer to the Legal Notices in the Abaqus 2025 HTML documentation, which can be obtained from a documentation installation, or in the SIMULIA Established Products 2025 Program Directory, which is available at www.3ds.com.

## About Execution Procedures

### Overview

Abaqus is executed by using the Abaqus execution procedure. In the following discussion the command to run the execution procedure is assumed to be abaqus. However, you can customize the execution procedure to run Abaqus using any alias you choose. (See the Abaqus Configuration Guide for details.)

The abaqus command is described in Execution Procedures. The following sections contain further information about running Abaqus jobs:

- Environment File Settings
- Managing Memory and Disk Resources
- Parallel Execution
- File Extension Definitions
- Fortran Unit Numbers

### Conventions

The following conventions are used in these sections:

- Each discussion includes a "Command summary" section that provides the syntax for the command in the left column and the syntax for its options in the right column. The full command must appear first, followed by the options. In some cases the command has multiple words, such as abaqus fetch; you must enter all words of the command before issuing any option statements.
- Options are presented in boldface. They can appear in any order and can be abbreviated.
- Default options are underlined ( __ ).
- Items enclosed in square brackets ([ ]) are optional.
- Items appearing in a list separated by bars ( | ) are mutually exclusive.
- One value must be selected from a list of values enclosed by curly brackets ({ }).
- You must supply values in italics.
- Blanks are used as separators between options and must not precede nor follow an equal sign.
- An alternate syntax of -optionvalue can be used instead of the option=value format.

The abaqus procedure will prompt for any information required that is not provided on the command line. If abaqus is typed with no options, prompts are issued for all options.

### Environment Settings

The Abaqus execution procedure uses environment parameters to customize the execution of a job. These settings can be changed using one of the Abaqus environment files: custom_v6.env or abaqus_v6.env.

If the same job parameter is defined in more than one environment file or is defined more than once within the same environment file, the last definition encountered will be used. Some exceptions to this rule are noted in Environment File Settings. These environment files can be used to customize the behavior of Abaqus, including modification of the default options.

### Selecting TCP/UDP Port Numbers

Several of the execution procedure command line options, such as port and listenerport, require that you specify a port number. TCP/UDP port numbers can range from 0 to 65535.

Port numbers 0 to 1023 are well-known ports used by system processes (such as FTP, SSH, SMTP, etc.) and should never be used. Port numbers 1024 to 49151 are registered ports with the Internet Assigned Number Authority (IANA) by software vendors. These ports can be used, but you should be careful that you are not conflicting with any software installed on your system that may be using this port. Port numbers 49152 to 65535 are unreserved and can be used freely, as long as no other application uses them.

Ports may be blocked by a firewall. Contact your system administrator to ensure that the ports that you want to specify are not blocked.

You can use the netstat command to obtain information on TCP/UDP network connections.

---

*Source: Abaqus 2025 FD02 Execution Guide*
