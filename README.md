# unpack
 application to retrieve source code from a merged module Basic09 I-Code file

This is the application unpack. It works on merged module files, but is still a work in progress.

unpack works for the most part. There are two areas where it still falls short, one of which will require a separate application. The first is identifying all record (complex type) statements. See the file **gap.txt** for more information. The second is completing the entire TYPE statement when not all fields were used in a single module. See the file **types.txt** for more information.

When loading unpack into Basic09, open Basic09 with 24K of workspace: OS9:basic09 #24k

All of these files are text files. You will need to pack them with Basic09 to have stand-alone apps. **DO NOT** try to load all of the application files into Basic09 at once. They will not fit into Basic09's workspace. Each file must be loaded and pack*'d separately. Each file contains more than one procedure, so make sure you pack* or the app won't run. Also, you cannot run the program in Basic09's workspace (even after packing).

The application:

* unpack.B09
* udecode.B09
* udefVars.B09
* uusymTabVal.B09
* ubuildSrc.B09
* uinstruction.B09 (This file hasn't been converted yet.)

Other tools:

* createUDB.B09   - create a fresh database (used when the InitDB file is modified to create a new database)
* ureadInitDB.B09 - reads the contents of the InitDB file (This file hasn't been converted yet.)
* ureadLins.B09   - reads the contents of the line numbers file
* ureadVars.B09   - reads the contents of the variables file

Documentation:

* README.md - This file
* gap.txt   - Description Area issue explanation
* types.txt - record (complex type) identification issue explanation

I have added the disk image files for the most current version of unpack. The files are:

* unpack_40trk.os9 - source files for unpack, including test files
* unpack_80trk.os9 - 80 track version of the 40 track disk image

There is one other issue that I keep forgetting to document. When the TYPE, DIM and PARAM statements are being printed the last statement is being left out. I don't know why this is happening, and I have not been able to determine a fix. Also, I need to point anyone interested in looking into the types and dim statement problems to the module that performs that work. It is ubuildSrc.B09. Both issues  will be found in that source file.

unpack usage:
 * unpack <pathname> #16k            The memory modifier is necessary. Don't leave it out.
 * unpack <pathname> -v (or -V) #16k This option is verbose mode. It will create the output file and display what's being done in greater detail.
 * unpack <pathname> -o (or -O) #16k This option is also verbose mode and display what's being done in greater detail, but will not create the output file.

setup:
 * Each file must be packed separately. udecode, udefVars abd ubuildSrc have sort procedures as part of that file. Use pack* (pack all) when packing those files.
 * I suggest creating an UNPACK directory on your hard drive to work in. (/DD/UNPACK)
 * Create a subdirectory at the root level named DATA if it doesn't already exist. In the DATA directory create a subdirectory named UNPACK. (/DD/DATA/UNPACK)
 * The following instructions are for creating the data files and executable modules:
  1. CHD to your UNPACK directory.
  2. Copy all files from the unpack.os9 disk to the UNPACK directory. (OS0:dircopy /d2 . (if D2 is where the unpack disk is))
  3. Open Basic09 with 24K of workspace. (OS9:basic09 #24k)
  4. Load createUDB.B09
  5. Run createUDB (Create the data files in /DD/DATA/UNPACK)
  6. Kill createUDB (B:kill (createUDB is the only procedure in the workspace, so procName is not necessary.)
  7. Load unpack.B09
  8. Pack unpack (B:pack (unpack is the only procedure in the workspace, so procName is not necessary.)
  9. Kill unpack (B:kill (unpack is the only procedure in the workspace, so procName is not necessary.)
  10. Load udecode.B09
  11. Pack all procedures in the workspace to udecode (B:pack* udecode)
  12. Kill all procedures in the workspace (B:kill*)
  13. Load udefVars.B09
  14. Pack all procedures in the workspace to udefVars (B:pack* udefVars)
  15. Kill all procedures in the workspace (B:kill*)
  16. Load ubuildSrc.B09
  17. Pack all procedures in the workspace to ubuildSrc (B:pack* ubuildSrc)
  18. Kill all procedures in the workspace (B:kill*)

In the UNPACK directory (your current data directory) will be the following files (these files, except test and connect, are in the Files folder on gitHub):
 * connect          The test module
 * test             The merged test module (includes 2 object code subroutines for testing unpack's skipping routine)
 * vars.txt         The variables output file from unpack
 * connectDSAT.txt  The description area output file from decode
 * connectVars.txt  The variables output file from decode
 * connectVDT.txt   The symbol table output file from decode

The last 3 files show what the output is supposed to look like.
The vars.txt file shows what the variables records currently look like.
