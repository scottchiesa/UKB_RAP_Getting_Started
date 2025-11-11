# Getting Started on the UK Biobank Research Analysis Platform using Command Line Interface (CLI)

The UK Biobank Research Analysis Platform (RAP) is a secure cloud-based environment that allows approved researchers to access, store, and analyse UK Biobank data without downloading it locally. There are countless tutorials, YouTube videos, and forums available on the internet for the myriad of functions the RAP performs. If you are not an experienced user, however, it can still be very confusing and difficult to find where to even get started. 

The UKB RAP has two main ways it can be used, either through the web interface accessed at https://platform.dnanexus.com/login or via command line interface (CLI) from a terminal on the user's local machine. While the former may be easier and more intuitive in the short-term (although even that can be very confusng for the uninitiated), more advanced analyses are often better carried out using the latter.

This short tutorial has therefore been written to give new users a walkthrough of all of the steps required to set themselves up on the RAP using a command line interface. 

## Software Needed

Visual Studio Code - Download at [https://code.visualstudio.com/download]  
GitBash - Download at [https://git-scm.com/install/]  

**Note that there are countless programmes and methods for using CLI, these are just the ones I currently use**

## Assumptions

This tutorial assumes that users have already registered as users of UK Biobank, have an approved project, have completed their training and are registered to use the UKB RAP, and have dispensed their data to their project space. 

It also assumes some knowledge of basic Linux commands that can be typed into a terminal, some examples of which can be seen below:

`pwd` - display present working directory  
`cd` - change directory (~ for home, . for current, .. for one directory up)  
`ls` - list everything in directory (type list -l to see in long rather than wide list)  
`mkdir` - make a new directory  
`cp` - copy file  
`mv` - move file  
`rm` - delete file (can't be undone so be careful!)  

It is also very important to try to understand how the filesystem works when you are either moving around the RAP, or between the RAP and your local machine. This can become quite confusing as the RAP works on an object-based file system (where every file has a unique identifier) rather than a POSIX-based system (where files are arranged in folders like most casual computer users are used to). The RAP employs a tool called DxFUSE to make it look like the files in its system are in folders though, so a lot of the time you are able to use standard commands like those shown above to move around. 

Some examples of commands and what they would do if you typed them into a POSIX-based system while in the folder `/c/Users/scott/UKB/Data/` are provided below.

`pwd` Would return the text /c/User/UKB/Data/ to show you where you are  
`cd ~` Would take you back to your home directory (so from /c/Users/scott/UKB/Data to /c/)   
`cd ..` Would take you up one level from data to UKB (so from /c/Users/scott/UKB/Data to /c/User/UKB/)  
`cd ../Scripts` Would take you directly from Data to Scripts (so up one directory from /c/Users/scott/UKB/Data into /c/Users/scott/UKB/ then back down into /c/Users/scott/UKB/Scripts).  
`ls -l ~/` Would list all files in your home directory (/c/Users/scott/)  
`ls -l ./` Would list all files in your current directory (/c/Users/scott/UKB/Data)  
`ls -l ../` Would list all files one folder up (/c/Users/scott/UKB)  

## Installing DX Toolkit

DX Toolkit is the command-line interface (CLI) that lets you interact with the DNAnexus platform (the underlying system running the UKB RAP). By prefacing certain commands in your terminal with 'dx', you can perform actions inside the RAP in a similar way to on your local machine. So for example, if you type `pwd` into your terminal it will tell you the current working directory on your machine (e.g. /c/Users/scott/UKB/). If you type `dx pwd` though (presuming you've already logged into the RAP as described below), it will tell you the current directory in which you are located on the RAP (e.g. /home/dnanexus/). The dx command therefore lets you view and/or control files both on your local machine and on the RAP from a single terminal window.  

To install DX Toolkit, open VS Code and select 'Terminal -> New Terminal'. Once the terminal opens at the bottom of the screen, click on the arrow next to the + sign on the right of the page (marked on screenshot) and change from powershell to bash (so the terminal recognises Linux commands). It may also be a good idea to change the option for CRLF at the bottom of the screen to LF.

<img src = "https://github.com/scottchiesa/UKB_RAP_Getting_Started/blob/main/vscode.png">

In the terminal, write the following

`pip3 install dxpy`

It may now ask you to upgrade. If it does, copy and paste the command it supplies to do so.

Once complete. check if it has installed properly by typing 

`dx --version` 

If something like dx-toolkit 0.360.0 appears, you should be good to go. If it doesn't, it is probably because your computer doesn't know the path for where to find your newly installed programme, so this has to be updated manually. 

To do this, first check where it has installed by typing 

`pip show dxpy`

This will return a whole bunch of info, but look for the line called Location: that will look something like

`Location: C:\Users\scott\AppData\Local\Packages\PythonSoftwareFoundation.Python.3.13_qbz5n2kfra8p0\LocalCache\local-packages\Python313\site-packages`

Your installation will be in the Python313 folder at this location in a 'Scripts' rather than 'site-packages' subfolder, so in this case

`C:\Users\scott\AppData\Local\Packages\PythonSoftwareFoundation.Python.3.13_qbz5n2kfra8p0\LocalCache\local-packages\Python313\Scripts`

To update the path to this location, do the following

- Search for Environment Variables in the Start Menu then select Edit Environment Variables For Your Account  
- Under User variables, select 'Path' then click Edit  
- Click New and paste the path (which in my case would have been C:\Users\scott\AppData\Local\Packages\PythonSoftwareFoundation.Python.3.13_qbz5n2kfra8p0\LocalCache\local-packages\Python313\Scripts)  
- Click OK a few times to escape the settings  
- Shut down then re-open VS Code

Type `dx --version` again to see if it now detects it and, if so, DX Toolkit should now be installed and ready to go on your machine!

## Logging in

Before logging in for the first time, you may need to set up an API token. You can easily do this using the following steps

- Go to the UK Biobank RAP website  
- Click your profile icon → “Profile” → “API Tokens.”
- Click “Generate New Token.”  
- Give it a label.  
- Set the expiry time.  
- Copy the token (it looks like a long string of letters and numbers).  

Now go back to your terminal and type

`dx login`

When prompted, enter your username, password, and the 6-digit code from your authentication app (Okta Verify). Note that nothing will appear on the screen when you are typing your password.

If you only have one active project on the RAP you should automatically be logged into that. If you have multiple, you can view which ones are available using the command

`dx select`

Now try typing `pwd` then`dx pwd` into your terminal. You should see that the first states which directory you are currently working in on your local machine and the second lists your current directory on the RAP. If dx pwd shows your RAP home directory, you're logged in!

## Setting Up a Cloud Workstation 

Next it is necessary to set up a virtual environment within the RAP to access all of your project files and run any analyses (easy ones at least, more complex stuff may have to be run through tools such as Swiss Army Knife, more on that later). This can be achieved by setting up a Cloud Workstation, a virtual workspace which lets you access and work with data stored on the DNAnexus Platform without having to download files to your computer (i.e. the whole point of the RAP).

Before doing this for the first time, you will need to configure something called ssh access to let you 'dial-in' to this virtual environment. Do this by typing the following command in your terminal and following any instructions.

`dx ssh_config`

Now you can activate a Cloud Workstation using the command

`dx run --ssh app-cloud_workstation`

At this point you will be given three options. More on these can be seen at https://platform.dnanexus.com/panx/tool/app/cloud_workstation. For now though you can just press enter to bypass these and you will - by default - be logged into a virtual environment for 1hr with the following computing hardware - mem1_ssd1_v2_x8. If you want to choose different settings, run the below code instead in which you can choose your desired setting

`dx run --ssh app-cloud_workstation --instance-type mem1_ssd1_v2_x36`

It may take a few minutes to log-in, but soon your terminal should update to display a screen that looks like the following

<img src = "https://github.com/scottchiesa/UKB_RAP_Getting_Started/blob/main/cloud.png">

Before your virtual space is ready to use, there are two more commands you need to type in order for it to find your project.

`unset DX_WORKSPACE_ID`  
`dx cd $DX_PROJECT_CONTEXT_ID:`

Your virtual workstation should now be ready to use! 

Note that from this point on, typing a command such as `ls` will list everything in your temporary virtual environment (i.e. the Cloud Workstation) rather than your local machine, whereas `dx ls` will list everything in your project space (your permanent file storage space).

**Important: Cloud Workstations are temporary virtual environments and therefore anything created or stored on them is permanently deleted as soon as the workstation times out or is shut down. Make sure to upload any important files back to your permanent project storage as soon as you create them to avoid them being lost. Also note that as long as you are connected to a Cloud Workstation you are being charged, so remember to always terminate the session once you're done! This can be done with the following command**

`dx terminate $DX_JOB_ID`

## Creating a Data Dictionary 

The RAP contains two types of data, tabular (i.e. a big spreadsheet with lots of variables that have been collected over the years like age, sex, BMI, etc), and bulk (i.e. genetic data, raw scans from MRIs, etc).

One of the first things you'll likely want to do once inside the RAP is create a data dictionary that lists every tabular variable that your project contains. You can then use this to identify the variable names you need to extract for your analysis in R/Stata/etc. For many people, this will be the only UK Biobank data they ever use.

First, make sure you are logged into your Cloud Workstation as described above and then make a new folder within your virtual environment to store your data using the command

`mkdir Tabular_Data`

Now go into this folder using

`cd Tabular_Data/` 

Now you need to create a data dictionary specific to your project. This step only needs to be carried out once and then the necessary files will be available to use for data extraction from that point on. There are two bits of information you need here - your project ID and your dataset record ID. 

You can find and make a note of your project ID (which will look like project-XXXXXXXXXXXXXX) by typing 

`dx find projects`

and your record ID (which will look like record-XXXXXXXXXXXXXX) by typing 

`dx ls -l`

For the record ID, you want the one after the .dataset file which will look something like 

`closed  2025-10-29 23:45:30           app71702_20251029213934.dataset (record-XXXXXXXXXXXXXXXXX)`

Once you have both of these, you can create your data dictionary by simply typing the following code

`dx extract_dataset project-XXXXXXXXXXXXXXXXX:record-XXXXXXXXXXXXXXXXX -ddd --delimiter ","`

If you happen to get an error message when you run the above command that tells you that something called pandas is necessary to create these files, simply install it using the following code then run the above code again

`pip3 install pandas`

You should now see three csv files starting with the word 'app' on your virtual environment in your Tabular_Data folder (provided this was your present working directory when running the dx extract_dataset command). The file ending with .data_dictionary.csv can now be used to view all of the variables available to you and is specific to your project. There are various ways to do this in the workstation, but for now it might be easiest to just open a new local terminal in VS Code (Terminal -> New Terminal) and type the following command to download it as a csv file that you can open in Excel on your computer

`dx download project-XXXXXXXXXXXXXXXX:/Tabular_Data/appXXXXX_XXXXXXXXXXXXXXXX.dataset.data_dictionary.csv -o data_dictionary.txt

You should now have an Excel file in the home directory of your local machine (i.e. your computer/laptop) that looks something like the example below

<img src = "https://github.com/scottchiesa/UKB_RAP_Getting_Started/blob/main/ddd.png">

At this point it is a good idea to also upload these files to your RAP project space so you have them stored there for future acccess. This can be done using the command below

`dx upload -r Tabular_Data/ --destination project-XXXXXXXXXXXXXXXXXXXXXX:/Tabular_Data/ `

## Extracting the Data Required for your Analysis

Now you have your data dictionary, you can easily extract the variables you need for your analysis. Make a note of the exact entity (column 1) and variable (column 2) names you want from the data dictionary as these have to be supplied in the form 'entity.name' and be exactly as listed in the dictionary in order for the next command to work. 

So for example, if you wanted to extract participant sex (row 28 in the above screenshot) the entity name for this is 'participant' and the name is 'p31', so the variable you need will be called 'participant.p31'. Similarly, participant ID would be 'participant.peid'.

It is important to note though that any variable measured repeatedly across multiple visits also has an 'instance' attached to it. So if you wanted to extract spirometry method for example (rows 24-27 on above screenshot), you would need to decide if you wanted it at instance 0, 1, 2, or 3 (which correspond to the initial assessment visit, the first repeat visit, the first imaging visit, and the repeat imaging visit, respectively). If it was the baseline visit (when all ~450k were measured) the variable would be called 'participant.p23_i0', whereas if it was the repeat imaging visit (when ~4k were measured) it would be called 'participant.p23_i3' 

This can get more detailed still when there are measures that are taken repeatedly at each visit, which are then listed as arrays. So for systolic blood pressure for example, as this was measured twice in each person at each visit and you might want an average of the two, you would need both 'participant.p4080_i0_a0' and 'participant.p4080_i0_a1'.

Once you have made a list of all the variables you want (just age and sex here as an example), you can quickly create a dataset containing only these by using the following command with each of your variable names listed after the flag for --fields and separated by commas.

`dx extract_dataset project-JXXXXXXXXXXXXXXXXX:record-XXXXXXXXXXXXXXXXX --fields participant.eid,participant.p31 -o ./extracted_data.csv`

There are potentially quicker ways to locate and list your variables of interest using different Linux commands and then submitting a txt file list of everything needed, but the above is shown as a basic example.

Now you have extracted your data, make sure you upload it to your project space for permanent storage as anything stored on a Cloud Workstation is automatically deleted every time it is terminated. This can again easily be done using a command like the following

`dx upload extracted_phenotpyes.csv --destination project-XXXXXXXXXXXXXXXXXXXXXX:/Data/ `

You should now have a dataset of all necessary variables ready for analysis!

## Running a Basic Analysis on Tabular Data using R

Coming soon.

## Submitting a Batch of Swiss Army Knife Jobs to Run in Parallel

Coming soon.

















