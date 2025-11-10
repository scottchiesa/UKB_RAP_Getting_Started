# Getting Started on the UK Biobank Research Analysis Platform using Command Line Interface (CLI)

UK Biobank provide a tonne of tutorials, YouTube videos, and forums for using the DNANexus Research Analysis Platform (RAP). If you are not an experienced user, however, it can still be very confusing and difficult to find where to even get started. 

The UKB RAP has two main ways it can be accessed and used, either through the web interface at https://platform.dnanexus.com/login or via command line interface (CLI) from a terminal on the user's local machine. While the former may be easier and more intuitive in the short-term, more advanced analyses are often better carried out using the latter.

This short tutorial has therefore been written to give new users some useful scripts and other useful info that should get them up-and-running on the RAP using a command line interface. 

## Software Needed

Visual Studio Code - Download at [https://code.visualstudio.com/download]  
GitBash - Download at [https://git-scm.com/install/]  

**Note that there are countless programmes and methods for using CLI, these are just the ones I currently use**

## Prior Knowledge Needed

This tutorial assumes that users have some knowledge basic Linux commands such as:

pwd - display present working directory  
cd - change directory (~ for home, . for current, .. for one directory up)  
ls - list everything in directory (type list -l to see in long rather than wide list)  
mkdir - make a new directory  
cp - copy file  
mv - move file  
rm - delete file (can't be undone so be careful!)  

It is also very important to understand how the filesystem works when you are moving around in it or trying to access files. This can become quite confusing on the RAP depending on how you are accessing the data or running analyses, but for a local machine, if you were in the following folder- /c/Users/scott/UKB/Data

__cd ~__ Would take you back to your home directory (so /c/)   
**cd ..** Would take you up one level to /c/Users/scott/UKB/  
**cd ../Scripts** If your UKB folder contained folders called both Data and Scripts, this would take you directly from the former to latter (so up one directory into UKB then back down into Scripts)  


