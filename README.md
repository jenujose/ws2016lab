# Project Description
 Deployment Automation of Windows Server 2016 labs on WS2016/Windows10 Hyper-V
 
 Simply deploy your lab just with these scripts and ISO file.

 Major differentiator is that once hydrated (first 2 scripts), deploy takes ~5 minutes. Cleanup is ~10s. 

 This solution is used in Microsoft Premier Workshop for Software Defined Storage, Hyper-V and System Center VMM
 
 Check [this](https://github.com/Microsoft/ws2016lab/tree/master/Scenarios) page for end to end scenarios! It's just a small portion I wrote for internally for consultants and PFEs in Microsoft

# Videos

Videos are bit outdated as subtle changes are in scripts.

* [1 Lab Hydration](https://youtu.be/xDrMYdSCIpM)
* [2 Lab Deployment](https://youtu.be/SzewA7C9lzI)
* [3 S2D Scenario](https://youtu.be/CX3ny0ON9X0)
* [4 Bonus-S2D to S2D Storage Replica Scenario](https://youtu.be/JRzBIOMEUO8)

**Step 1** Download required files (prerequisities):
* [Scripts](https://github.com/Microsoft/ws2016lab/blob/master/scripts.zip?raw=true)
* [Windows Server 2016](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2016) 
* [Latest Cumulative Update](http://catalog.update.microsoft.com/v7/site/Search.aspx?q=Cumulative%20Update%20for%20Windows%20Server%202016%20for%20x64-based%20Systems%20)  for Windows Server 2016.

**Step 2** Create folder and Unzip scripts there

**Step 3** Right-click and run with PowerShell 1_Prereq.ps1
 * 1_Prereq.ps1 will create folder structure and downloads neccessary files from internet
 * If you don't have an internet connection on your server, run this on internet connected machine, copy created files over and run 1_prereq.ps1 again
 
**Step 4** Right-click and run with PowerShell 2_CreateParentDisks.ps1
 * 2_CreateParentDisks.ps1 will check if you have Hyper-V installed, it will prompt you for Windows Server 2016 ISO file, Cumulative Update and then will hydrate parent disks and Domain Controller.

**Step 5** Right-click and run with PowerShell 3_Deploy.ps1
 * 3_Deploy.ps1 will deploy S2D Hyperconverged [scenario](https://github.com/Microsoft/ws2016lab/tree/master/Scenarios) defined in Labconfig.ps1 [different examples](https://github.com/Microsoft/ws2016lab/blob/master/Scripts/LabConfig.ps1)
 
**Step 6** Continue with [S2D Hyperconverged Scenario](https://github.com/Microsoft/ws2016lab/tree/master/Scenarios/S2D%20Hyperconverged)

* This scenario will help you understand new Windows Server 2016 feature Storage Spaces Direct.

* It will deploy 4 Servers simulating 200TB Storage

**Step 7** Cleanup lab with Cleanup.ps1

**Step 8** Try different scenarios
* [Local Admin Password solution for NanoServer](https://github.com/Microsoft/ws2016lab/tree/master/Scenarios/LAPS%20on%20Nano)
* [Testing first boot performance](https://github.com/Microsoft/ws2016lab/tree/master/Scenarios/Testing%20Nano%20performance)

# What's in the lab

Automatically hydrated Domain Controller with DHCP and one scope. There are several accounts automatically provisioned - SQL Run As Account, SQL Agent Account,  VMM Service Account and one additional Domain Admin with name you can specify, so you can install SQL + SC VMM easily.

![](https://github.com/Microsoft/ws2016lab/blob/master/Docs/Screenshots/dhcp01.png)
![](https://github.com/Microsoft/ws2016lab/blob/master/Docs/Screenshots/ActiveDirectory01.png)

You can then modify LabConfig.ps1 to hydrate whatever you want. Like this 4 node nano s2d cluster with 200TB capacity - all running on ultrabook.

![](https://github.com/Microsoft/ws2016lab/blob/master/Docs/Screenshots/HVConsole01.png)
![](https://github.com/Microsoft/ws2016lab/blob/master/Docs/Screenshots/ServerManager01.png)
![](https://github.com/Microsoft/ws2016lab/blob/master/Docs/Screenshots/FCConsole01.png)
![](https://github.com/Microsoft/ws2016lab/blob/master/Docs/Screenshots/FCConsole02.png)
![](https://github.com/Microsoft/ws2016lab/blob/master/Docs/Screenshots/FCConsole03.png)

# Known issues

* DISM does not work on Cluster Shared Volumes
* When waiting on DC to come online, the script trows some red errors. It's by design, nothing to worry about.
* DISM sometimes throws errors on NTFS volumes also. Just build the lab again in different folder.
* sometimes if all machines are started at once, some are not domain joined. Just cleanup and deploy again.


# So what is it good for?

Simulations such as
* how to script against servers
* how to automate configuration
* what will happen when I run this and that command
* how change drive in S2D cluster
* what will happen when one node goes down
* testing new features before pushing to production
* ...
