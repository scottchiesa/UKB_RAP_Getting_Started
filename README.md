# Getting Started on the UK Biobank Research Analysis Platform using Command Line Interface (CLI)

UK Biobank provide a tonne of tutorials, YouTube videos, and forums for using the DNANexus Research Analysis Platform (RAP). If you are not an experienced user, however, it can still be very confusing and difficult to find where to even get started. 

The UKB RAP has two main ways it can be accessed and used, either through the web interface at https://platform.dnanexus.com/login or via command line interface (CLI) from a terminal on the user's local machine. While the former may be easier and more intuitive in the short-term, more advanced analyses are often better carried out using the latter.

This short tutorial has therefore been written to give new users some useful scripts and other useful info that should get them up-and-running on the RAP using a command line interface. 

## Software Needed

Visual Studio Code - Download at [https://code.visualstudio.com/download]  
GitBash - Download at [https://git-scm.com/install/]  

**Note that there are countless programmes and methods for using CLI, these are just the ones I currently use**

## Prior Knowledge Needed

This tutorial assumes that users have some knowledge of basic Linux commands that can be typed into a terminal such as:

`pwd` - display present working directory  
`cd` - change directory (~ for home, . for current, .. for one directory up)  
`ls` - list everything in directory (type list -l to see in long rather than wide list)  
`mkdir` - make a new directory  
`cp` - copy file  
`mv` - move file  
`rm` - delete file (can't be undone so be careful!)  

It is also very important to understand how the filesystem works when you are moving around or trying to access files. This can become quite confusing on the RAP depending on how you are accessing the data or running analyses, but if you were in a local machine in the following folder - /c/User/UKB/Data/

`cd ~` Would take you back to your home directory (so from /c/User/UKB/Data to /c/)   
`cd ..` Would take you up one level to UKB (so from /c/User/UKB/Data to /c/User/UKB/)  
`cd ../Scripts` If your UKB folder contained folders called both Data and Scripts, this would take you directly from the former to latter (so up one directory from /c/User/UKB/Data into /c/User/UKB/ then back down into /c/User/UKB/Scripts).
`./` This would point to files in your current directory

## Installing DX Toolkit

DX Toolkit is the command-line interface (CLI) that lets you interact with the DNAnexus platform, the underlying system running the UKB RAP. By prefacing certain commands in your terminal with 'dx', you can perform actions inside the RAP in a similar way to on your local machine. So for example, if you type `pwd` into your terminal it will tell you the current working directory on your machine (e.g. /c/User/UKB/). If you type `dx pwd` though (presuming you're logged into the RAP), it will give you the current working directory on the RAP (e.g. /home/dnanexus/). This lets you use the same terminal to control files both on your local machine and on the RAP.  

To install DX Toolkit, open VS Code and select 'Terminal -> New Terminal'. Once the terminal opens at the bottom of the screen, click on the arrow next to the + sign on the right of the page (marked on screenshot) and change from powershell to bash (so the terminal recognises Linux commands).

<img src = "https://github.com/scottchiesa/UKB_RAP_Getting_Started/vscode.png">



