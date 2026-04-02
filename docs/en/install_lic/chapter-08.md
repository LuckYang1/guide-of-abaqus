# Chapter 8: Accessing Remote File Systems

This appendix describes accessing remote file systems for Abaqus installation and execution.

Abaqus can be run on NFS-mounted file systems, or the display can be exported from a remote computer; however, users may experience performance and reliability problems with these alternatives.

## 8.1 Running Abaqus Remotely on Linux

### NFS Mounted File Systems

There are several scenarios for running Abaqus on NFS-mounted file systems; the impact of using NFS varies with how NFS is used. The most common scenarios for running Abaqus on NFS-mounted file systems are as follows:

**Scenario 1: Abaqus is installed on a remote file system. The CPU, save directory, and temporary directory are local (on the computer where Abaqus will run).**

In this case, Abaqus executables and shared libraries are loaded into local memory from the file system where Abaqus is installed as needed over the network. Processing and output occur locally. If there is enough local memory to prevent frequent paging, network traffic is relatively light. When local memory is insufficient to prevent paging, performance degrades and reliability may be affected.

**Scenario 2: Abaqus is installed on a remote file system. The save directory and/or temporary directory are not local to the CPU executing Abaqus.**

In this case, program files and data used during execution are written over the network. There may be large amounts of data transferred to the network, and performance may be adversely affected. Abaqus performance may be very slow and may affect other users of the network, as the network may become saturated. Additionally, Abaqus does not catch file errors caused by accessing NFS-mounted files, so even temporary NFS-mounted file access failures cause Abaqus jobs to fail. Using Abaqus in this configuration should be avoided whenever possible. If an Abaqus/Standard job requires this configuration, users should move the save directory to the NFS-mounted file system before moving the temporary directory.

### Exporting the Display

This configuration is relevant only to Abaqus/CAE and Abaqus/Viewer. In this configuration, Abaqus is installed on a remote file system, and the CPU, save directory, and temporary directory are all on the same remote computer, accessed via remote login. All processing occurs on the remote computer, and only output messages or graphics are exported to and displayed on the local computer. This approach causes performance problems. Slight incompatibilities between the OpenGL and GLX libraries can cause severe graphics problems and may, in some cases, prohibit Abaqus/CAE or Abaqus/Viewer from running. Using Abaqus in this configuration is not supported and should be avoided whenever possible.

## 8.2 Using the Network ODB Connector

Users can create a network ODB connector to access output databases on remote computers (see Accessing Output Databases on Remote Computers). Abaqus/CAE or Abaqus/Viewer can start a server on the remote system and assign a port number if the following conditions are met:

- The username on the remote host is the same as the username on the local system.
- The remote shell command (rsh) or secure shell command (ssh) is configured to not prompt users for passwords.

Abaqus checks the security of the connection by passing keys back and forth between the server and client.

If users encounter problems using the network ODB connector, or if the usernames differ, they can manually start the network ODB server by running the `abaqus networkDBConnector` execution procedure from the command line on the remote computer.

You can disable the network ODB connector by deleting `dmbwtr` and `dmbwtrd` from the `install_dir/os/code/bin/SMAExternal/dmbwtr/` directory.

---

[Return to Contents](./index.md) | [Previous Chapter: Installation Subdirectories](./chapter-07.md) | [Next Chapter: Verification Procedures](./chapter-09.md)
