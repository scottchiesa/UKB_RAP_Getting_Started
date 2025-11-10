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

<img src = "https://github.com/scottchiesa/UKB_RAP_Getting_Started/blob/main/vscode.png">

In the terminal, write the following

`pip3 install dxpy`

It may now ask you to upgrade and give you a command to copy and paste. Do this if it happens.

Check if it has installed properly by typing 

`dx --version` 

If something like dx-toolkit 0.360.0 appears, you should be good to go. If it doesn't, it is probably because your computer doesn't know the path for where to find it, so this has to be updated manually. 

To do this, first check where it has installed by typing 

`pip show dxpy`

You will get a whole bunch of info, but look for the line called Location: that will look something like

`C:\Users\scott\AppData\Local\Packages\PythonSoftwareFoundation.Python.3.13_qbz5n2kfra8p0\LocalCache\local-packages\Python313\site-packages`

Your installation will be in the Python313 folder at this location in a 'Scripts' rather than 'site-packages' subfolder, so in this case

`C:\Users\scott\AppData\Local\Packages\PythonSoftwareFoundation.Python.3.13_qbz5n2kfra8p0\LocalCache\local-packages\Python313\Scripts`

To update the path, do the following

- Search Environment Variables in the Start Menu → open Edit environment variables for your account  
- Under User variables, highlight Path → click Edit  
- Click New, and paste the path (in this case C:\Users\scott\AppData\Local\Packages\PythonSoftwareFoundation.Python.3.13_qbz5n2kfra8p0\LocalCache\local-packages\Python313\Scripts)  
- Click OK a few times to escape the settings  
- Restart VS Code

DX Toolkit should now be installed and ready to go on your machine.

## Logging in

In the terminal, type

`dx login`

When prompted, enter your username, password, and 6-digit code from your authentication app (Okta Verify). Note that nothing will appear on the screen when you are typing your password.

If you only have one active project on the RAP you should automatically be logged into that. If you have multiple, you can choose which one you want using the command

`dx select`

Now by typing either `pwd` or`dx pwd` into your terminal, you will be able to see which directory you are currently working in on both your local machine and the RAP, respectively. 










