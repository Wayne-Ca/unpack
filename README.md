# unpack
 application to retrieve source code from a Basic09 I-Code module

This is currently the application decode. It only works on a single module. The future application unpack will allow processing of merged-module files. Until then you will have to use a modbuster application to separate the modules into separate files for use with decode.

decode works for the most part. There are two areas where it still falls short, one of which will require a separate application. The first is identifying all record (complex type) statements. See the file **gap.txt** for more information. The second is completing the entire TYPE statement when not all fields were used in a single module. See the file **types.txt** for more information.

Watch this space as I will be publishing more data and information about decode and it's outstanding issue with record (complex type) statements.

I am still learning to use git, so there may be times when an update isn't here when I thought it was.

All of these files are text files. You will need to pack them with Basic09 to have stand-alone apps. **DO NOT** try to load all of the application files into Basic09 at once. They will not fit into Basic09's workspace. Each file must be loaded and pack*'d separately. Each file contains more than one procedure, so make sure you pack* or the app won't run. Also, you cannot run the program in Basic09's workspace (even after packing).

The application:

* decode.B09
* defVars.B09
* buildSrc.B09
* instruction.B09
* setOpts.B09

Other tools:

* createDB.B09 - create a fresh database (used when the InitDB file is modified to create a new database)
* readVars.B09 - reads the contents of the variables file
* readLins.B09 - reads the contents of the line numbers file
* readInitDB.B09 - reads the contents of the InitDB file

Documentation:

* README.md - This file
* gap.txt - DSAT issue explanation
* types.txt - record (complex type) identification issue explanation

December 18, 2021

I have added the disk image files for the mlost current working version of decode. The files are:

* decode.os9 - binaries
* decodePP.os9 - source in pretty print format
* decodeSRC.os9 - source in standard print format

The source in the repository has been modified since those disk images were made so don't try to use that version without expecting issues. The changes made are pertaining to the TYPE statement problem, as well as issues with TYPE/DIM/PARAM statement construction.