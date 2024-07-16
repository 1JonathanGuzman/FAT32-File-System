# FAT32-File-System
A FAT32 File system parser and command-line interpreter in C.

Tested on Ubuntu 24.04, Linux kernel version 6.8.0, and GCC version 13.2.

Instructions for running the project:
  This program should run with no issue on most new releases of the Linux kernel. 

  To run the program, clone the repository and execute the "make" command while in
  the project's root directory. This will create an executable called "filesys"
  and generate an object file called filesys.o. You can get rid of the filesys.o file
  using "make clean", which will clean the current working directory of all files ending
  in ".o".

  Next, unzip the FAT32 file image using the command "bzip2 -dk fat32.img.bz2". This will
  create a file named "fat32.img", which will be the FAT32 file image that the program will be
  using. The "k" flag is important when executing the bzip command, as this will preserve the 
  .bz2 file in the unzipping process. This way, if you would like to regenerate a new file image
  for you to play with, you can run the "bzip2 -dk fat32.img.bz2" command again.

  Finally, run the program by executing the command

    ./filesys fat32.img

  This will interpret the image and launch the command-line interpreter that will allow you to
  read, modify, and navigate the file image using these commands:

  All available commands ----------
    help:                            Prints out this menu as many times as you need.
    info:                            Provides a brief summary of the current FAT image being processed.
    cd [DIRNAME]:                    Change current working directory to another valid directory inside the current working directory.
    ls:                              Print the contents of the current working directory.
    size [FILENAME | DIRNAME]:       Provides the size of a file or directory immediately within the current working directory.
    lseek [FILENAME] [OFFSET]:       Will set the file pointer of FILENAME, if opened for reading and/or writing, to exactly OFFSET bytes.
    read [FILENAME] [BYTES]:         Will read BYTES amount of content (in bytes, of course) inside FILENAME, and output it to the console.
    open [FILENAME] [-r|-w|-rw|-wr]: Will open FILENAME for reading and/or writing. Note that -rw and -wr are the same, and both will be accepted.
    lsof:                            Will print out a table of all currently opened files.
    close [FILENAME]:                Will close FILENAME if currently opened for reading and/or writing.
    mkdir [DIRNAME]:                 Will create a directory in the current working directory named DIRNAME if one does not already exist.
    creat [FILENAME]:                Will create a file in the current working directory named FILENAME if one does not already exist.
    cp [FILENAME] [DESTINATION]:     Will copy FILENAME to DESTINATION. DESTINATION can be inside of a directory, create a new file, or overwrite an existing file.
    rm [FILENAME]:                   Will remove a file named FILENAME inside the current working directory if it exists.
    rmdir [DIRNAME] [optional: -r]:  Removes a directory named DIRNAME in the current working directory. You can optionally include the -r flag to recursively delete DIRNAME's contents.
    dump [FILENAME | DIRNAME]:       Dump the hex contents of a file or directory.

    Limitations of this program:

    Limitations: 
    
       Arguments that accept a directory are limited to directories inside the current working directory.
       Directories located one subdirectory deeper within the current working directory will not be
       accepted as a valid directory for input.
    
       For instance, if you have /Dir1/Dir2, and you execute the command "cd Dir1/Dir2" while in
       the root, "/", it will not find the directory and the command will fail. You must instead
       use "cd Dir1", then "cd Dir2" to move to the desired directory.
    
       Additionally, only 10 files can be opened at once for reading and/or writing.
