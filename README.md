# unpack
 application to retrieve source code from a Basic09 I-Code module

This is currently the application decode. It only works on a single module. The future application unpack will allow processing of merged-module files. Until then you will have to use a modbuster application to separate the modules into separate files for use with decode.

decode works for the most part. There are two areas where it still falls short, one of which will require a separate application. The first is identifying all record (complex type) statements. See the file **gap.txt** for more information. The second is completing the entire TYPE statement when not all fields were used in a single module. See the file **types.txt** for more information.

When loading decode into Basic09, open Basic09 with 40K of workspace: OS9:basic09 #40k

You will not be able to load and pack* the decode.B09 module without this much space. I have not tried to see if the defVars.B09, buildSrc.B09 or instruction.B09 files will load into a smaller space.

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

I have added the disk image files for the most current working version of decode. The files are:

* decode.os9 - binaries
* decodePP.os9 - source in pretty print format
* decodeSRC.os9 - source in standard print format

The source in the repository has been modified since those disk images were made so don't try to use that version without expecting issues. The changes made are pertaining to the TYPE statement problem, as well as issues with TYPE/DIM/PARAM statement construction.

There is one other issue that I keep forgetting to document. When the TYPE, DIM and PARAM statements are being printed the last statement is being left out. I don't know why this is happening, and I have not been able to determine a fix. Also, I need to point anyone interested in looking into the types and dim statement problems to the module that performs that work. It is buildSrc.B09. Both issues  will be found in that source file.

October 3, 2023

I failed to include the EXEC file access token. To correct this I added the missing token to the decode.B09 and instruction.B09 source files. Testing shows that any file opened in EXEC mode will be correctly identified by decode.

I haven't rebuilt the .os9 disk image files yet, so you will have to grab the decode.B09 and instruction.B09 source files and re-pack them. Be sure to use the pack* command in Basic09 for each file as they both include merged modules.

October 4, 2023

I have made the changes to the disk image files so the source, pretty print and I-Code modules reflect the change to the decode and instruction modules allowing the EXEC file access mode to be properly decoded.

November 4, 2023

I have made significant changes to the code. I added a new field variable to the variables file record which required updating almost every procedure. You must run createDB (the new one which you must pack and overwrite the old one) in order to update the initDB file (and the other work files in the DATA directory) to account for the new field variable.

decode now has a new option (command line), -v(-V). This option allows you to see what version of decode you are using. This will become more important with future versions of the program.

createDB now allows you to choose between keeping the default fg/bg colors you have saved in the old initDB file or using the current fg/bg colors as the default screen colors. These colors are set when decode is finished and exits back to NitrOS-9.

There is a new output file created when <procname>Raw.txt is created. I wanted to be able to see what the token counts are after decode is finished, so I created an output file called <procname>Refs.txt that gets written when you see the token counts in the overlay window. It has the same format as the text in the window as to be easily identifiable.

Because of an issue with Basic09 and the hi-res characters I use in building the source statements I had to revert to an older version of instruction.B09. Instruction still works, but there is now a case where if you have PRINT USING with no path inbetween, it displays PRINT  USING (note the extra space). I remember having that issue before, but I don't recall how I fixed it. It is not a major issue since Basic09 will remove the extra space without issue, but I am waiting to correct it as the last thing after all other issues with the DSAT and building the TYPE, DIM and PARAM statements have been dealt with.

buildSrc.B09 is still very buggy. On the procedures I am testing with it currently runs without crashing, but on two of them the output of the DSAT Validation is not correct (read that waaaaaaay off). I am still working on it and have uploaded the source just so it is consistent with the other files. I have not yet advanced past the DSAT Validation code in order to keep the remainder of the code working the way it did before. This means that the current changes to the code concerning the DSAT have no bearing on the output of the source statements.

November 7, 2023

I have buildSrc working  with getHeader1-4, with the caveat that getHeader3 still assigns a field record to the wrong type. The source here has been updated, but the disk image files have not. I will be updating them shortly.