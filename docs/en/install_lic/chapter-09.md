# Chapter 9: Verification Procedures

The verification procedure checks the installation of all licensed Abaqus products and reports success or failure of verification for each product.

The verification procedure runs automatically after the Abaqus installation procedure completes, but only verifies a subset of products. The verification procedure can also be run as an Abaqus command option.

The procedure runs verification problems for each licensed product and compares the results to reference values. Command line options are not affected by license type; that is, the verification procedure attempts to verify all products named in the command. License requirements for the selected products are checked before running the verification procedure. If a teaching academic license is detected, the verification procedure run during installation checks only Abaqus/Standard, Abaqus/Explicit, and Abaqus/CAE.

If a product is not licensed, product verification is skipped. These checks can be bypassed using the `-noLic` command line option. Verification problems for all Abaqus products are automatically extracted from disk during installation.

## Running the Verification Procedure from the Command Line

Run the procedure by entering the following command:

```tcl
abaqus verify [-adams -all -ams -tosca -cae -catiav4 -cPerf -dcatiav5 -design -docUrl -exp -foundation -help -install -ioPerf -log -make -moldflow -noGui -noLic -parallel -param -parasolid -proe -retainFiles -scripting -std -swi -user_exp -user_std -verbose -viewer]
```

## Common Options

| Option | Description |
|--------|-------------|
| -all | Verify all licensed products. All other verify options are ignored except for log and noLic. |
| -help | Print a verification usage summary. |
| -install | Verify Abaqus parametric studies and Abaqus/CAE. |
| -log | Direct all output to a file named `verify.log` in the current working directory. |

## Product Options

| Option | Description |
|--------|-------------|
| -ams | Verify Abaqus/AMS. |
| -tosca | Verify Tosca for Abaqus. |
| -cae | Verify Abaqus/CAE. |
| -design | Verify Abaqus/Design. |
| -exp | Verify Abaqus/Explicit. |
| -foundation | Verify Abaqus/Foundation. |
| -param | Verify parametric studies in Abaqus. |
| -std | Verify Abaqus/Standard. |
| -user_exp | Verify Abaqus/Explicit with user subroutines. |
| -user_std | Verify Abaqus/Standard with user subroutines. |
| -viewer | Verify Abaqus/Viewer. |

## Translator Options

| Option | Description |
|--------|-------------|
| -adams | Verify the Abaqus Interface for MSC.ADAMS. |
| -catiav4 | Verify the geometry translator for CATIA V4. |
| -dcatiav5 | Verify the direct geometry import for CATIA V5 (geometry import functionality within Abaqus/CAE; does not verify the installation or functionality of the CATIA V5 Associative Interface plugin). |
| -moldflow | Verify the Abaqus Interface for Moldflow. |
| -parasolid | Verify the geometry translator for Parasolid. |
| -proe | Verify the geometry translator for Pro/ENGINEER (geometry import functionality within Abaqus/CAE; does not verify the installation or functionality of the Pro/ENGINEER Associative Interface plugin). |
| -swi | Verify the geometry translator for SolidWorks (geometry import functionality within Abaqus/CAE; does not verify the installation or functionality of the SolidWorks Associative Interface plugin). |

## Additional Options

| Option | Description |
|--------|-------------|
| -cPerf | Verify Abaqus/CAE performance. |
| -docUrl | Verify Abaqus HTML documentation URL. |
| -ioPerf | Verify I/O performance. |
| -make | Verify the abaqus make utility. |
| -noGui | Verify the -noGUI option for Abaqus/CAE and Abaqus/Viewer. |
| -noLic | Required with -all, -install, or a product option list. Runs the verification procedure for the specified products but bypasses all license checks. The procedure attempts to verify all selected products regardless of licensing status. |
| -parallel | Verify Abaqus analysis jobs using parallelization. |
| -scripting | Verify the Abaqus scripting interface. |
| -retainFiles | Retain all files in the verify directory after successful verification (by default, files are deleted). |
| -verbose | Include additional details for debugging purposes. |

## Reviewing and Resolving Verification Procedure Failures

If the verification procedure completes successfully, all files and the verify directory are deleted (unless you use the retainFiles option). Error diagnostics for all products that failed verification are retained in the verify directory. It is important to review these error messages.

After installation verification, the verify directory and results can be found in the `install_dir/InstallDate/logs/.../tmp/` directory.

The following suggestions may help you correct common installation errors that cause verification procedure failures:

1. Ensure that the license file was installed correctly. If there is a problem with the license file, error messages are written to standard output.
2. Ensure that you are not attempting to execute an Abaqus product that is not licensed.
3. Ensure that the operating system and compiler levels are consistent with those specified for this release in the Program Directory.

If you are still unable to resolve the problem, contact your local office or representative for assistance.

---

[Return to Contents](./index.md) | [Previous Chapter: Accessing Remote File Systems](./chapter-08.md)
