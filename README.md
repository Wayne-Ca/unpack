# unpack
 application to retrieve source code from a Basic09 I-Code module

This is currently the application decode. It only works on a single module. The future application unpack will allow processing of merged-module files. Until then you will have to use a modbuster application to separate the modules into separate files for use with decode.

Watch this space as I will be publishing more data and information about decode and it's outstanding issue with record (complex type) statements.

I am still learning to use git, so there may be times when an update isn't here when I thought it was.

decode works for the most part. There are two areas where it still falls short, one of which will require a separate application. The first is identifying all record (complex type) statements. See the file gap.txt for more information. The second is completing the entire TYPE statement when not all fields were used in a single module. See the file types.txt for more information. (types.txt isn't uploaded yet as I have to finish writing it.)