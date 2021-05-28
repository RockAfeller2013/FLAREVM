##---------------------------------------------------------------------------------------------------
# Microsoft Windows Images - https://developer.microsoft.com/en-us/microsoft-edge/tools/vms/
# Windows 10 Base Image
# https://virtualizationandstorage.wordpress.com/?s=SOE
# https://virtualizationandstorage.wordpress.com/2014/01/16/windows-2012-r2-soe/
# https://virtualizationandstorage.wordpress.com/2014/10/01/howto-design-a-secure-windows-2012-r2-standard-operating-environment/
###---------------------------------------------------------------------------------------------------
# Other Tools
# https://cutter.re/
# https://www.varonis.com/blog/malware-analysis-tools/
# https://bakerstreetforensics.com/2021/05/26/adding-sift-and-remnux-to-your-windows-forensics-environment/
##---------------------------------------------------------------------------------------------------
# Install Tools
# VMware Tools 
Set-ExecutionPolicy AllSigned
Set-ExecutionPolicy Unrestricted
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))
choco install -y classic-shell
choco install -y bginfo
choco install -y git
choco install -y winzip
choco install -y sysinternals
choco install -y googlechrome
choco install -y firefox
choco install -y 7zip.install
choco install -y git.install
choco install -y mobaxterm
choco install -y monosnap
choco install -y cutepdf
choco install -y open-visual-traceroute
choco install -y sumatrapdf
choco install -y vscode
choco install -y word.viewer
choco install -y excel.viewer
choco install -y powerpoint.viewer
choco install -y visioviewer2016
choco install -y vlc
choco install -y vmware-workstation-player
choco install -y obs-studio
choco install -y rsat
choco install -y x64dbg.portable
##---------------------------------------------------------------------------------------------------
## Install ReTool Kit - https://github.com/mentebinaria/retoolkit
##---------------------------------------------------------------------------------------------------
## DFIR Tools install, FireEye FlareVM, CommandoVM, SANs SIFT, AutoSpy, Sleuth Kit

wget https://github.com/sleuthkit/autopsy/releases/download/autopsy-4.18.0/autopsy-4.18.0-64bit.msi
wget https://github.com/sleuthkit/sleuthkit/releases/download/sleuthkit-4.10.2/sleuthkit-4.10.2-win32.zip
unzip sleuthkit-4.10.2-win32.zip
msiexec.exe /i "autopsy-4.18.0-64bit.msi" /qn
##---------------------------------------------------------------------------------------------------
choco install wireshark
##---------------------------------------------------------------------------------------------------
## Tracelab tools https://www.tracelabs.org/initiatives/osint-vm
##---------------------------------------------------------------------------------------------------
https://github.com/fireeye/commando-vm
##---------------------------------------------------------------------------------------------------
wget http://boxstarter.org/package/url?https://raw.githubusercontent.com/fireeye/flare-vm/master/flarevm_malware.ps1
git clone https://github.com/fireeye/flare-vm
.\install.ps1 -profile_file profile.json -password -norestart
'You may throttled by the repo's, so when it stalls, chance your public IP, by quick reboot of your NTU. as per https://github.com/fireeye/flare-vm/issues/351
'Install-BoxStarterPackage -PackageName flarevm.installer.flare -DisableReboots
cinst x64dbg
cup all
##---------------------------------------------------------------------------------------------------
## Install Windows Debugging Tools for Windows (WinDbg, KD, CDB, NTSD)
https://docs.microsoft.com/en-us/windows-hardware/drivers/debugger/time-travel-debugging-overview
##---------------------------------------------------------------------------------------------------
## Install BoomBox with Cuckoo
## Packer
## Vagrant
## Virtual Box

setx VAGRANT_HOME "E:\data\vagrant" /M
setx VAGRANT_HOME "E:\data\vagrant" 
setx PATH "E:\Program Files\VirtualBox"
setx PATH "E:\Program Files\VirtualBox" /M
https://stackoverflow.com/questions/17240725/setx-doesnt-append-path-to-system-path-variable/17247259

vboxmanage setproperty machinefolder E:\data\VM
vboxmanage list systemproperties | grep folder

git clone https://github.com/nbeede/BoomBox

'Edit build.pst and set the locations of Packer.exe and VBoxManage.exe

[string]$PackerPath = 'C:\ProgramData\chocolatey\lib\packer\tools\packer.exe',
$VBoxManage = "E:\Program Files\Oracle\VirtualBox\vBoxManage.exe"

./build.ps1 -ProviderName virtualbox -VagrantOnly

type vagrant_up_sandbox.log
##---------------------------------------------------------------------------------------------------
https://docs.microsoft.com/en-us/windows/wsl/install-win10
##---------------------------------------------------------------------------------------------------
Install DELL Support Assist - https://www.dell.com/support/contents/en-au/article/product-support/self-support-knowledgebase/software-and-downloads/supportassist
Instal Geforce Expereince
Install Office
Install Visio
##---------------------------------------------------------------------------------------------------
Configure ntptime
Configure location
Configure date format
##---------------------------------------------------------------------------------------------------
C:\ProgramData\chocolatey\lib\sysinternals\tools\bginfo.exe /timer:0 /nolicprompt /silent
##---------------------------------------------------------------------------------------------------
[HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Run]

C:\ProgramData\chocolatey\lib\sysinternals\tools\bginfo.exe C:\ProgramData\chocolatey\lib\sysinternals\tools\bginfo.bgi /timer:0 /nolicprompt /silent 
bginfo.exe c:\users\lowell\bin\config.bgi /timer:0 /nolicprompt /silent
C:\Users\Administrator\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup
##---------------------------------------------------------------------------------------------------
## Startup

Windows Registry Editor Version 5.00

[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Run]
"WindowsDefender"=hex(2):22,00,25,00,50,00,72,00,6f,00,67,00,72,00,61,00,6d,00,\
  46,00,69,00,6c,00,65,00,73,00,25,00,5c,00,57,00,69,00,6e,00,64,00,6f,00,77,\
  00,73,00,20,00,44,00,65,00,66,00,65,00,6e,00,64,00,65,00,72,00,5c,00,4d,00,\
  53,00,41,00,53,00,43,00,75,00,69,00,4c,00,2e,00,65,00,78,00,65,00,22,00,00,\
  00
"VMware VM3DService Process"="\"C:\\Windows\\system32\\vm3dservice.exe\" -u"
"VMware User Process"="\"C:\\Program Files\\VMware\\VMware Tools\\vmtoolsd.exe\" -n vmusr"
"Classic Start Menu"="\"C:\\Program Files\\Classic Shell\\ClassicStartMenu.exe\" -autorun"
"Biginfo"="C:\\ProgramData\\chocolatey\\lib\\sysinternals\\tools\\bginfo.exe C:\\ProgramData\\chocolatey\\lib\\sysinternals\\tools\\bginfo.bgi /timer:0 /nolicprompt /silent "
##---------------------------------------------------------------------------------------------------
## SYSPREP 
## https://www.windowsafg.com/win10x86_x64.htmlhttps://www.windowsafg.com/win10x86_x64.html
net stop wmpnetworksvc
%windir%\system32\sysprep\sysprep.exe /generalize /oobe /mode:vm /shutdown /unattend:C:\SYSTOOLS\autounattend.xml
c:\Windows\System32\sysprep\sysprep.exe /generalize /oobe /mode:vm /shutdown /unattend:C:\SYSTOOLS\2019.xml
##---------------------------------------------------------------------------------------------------
# https://docs.microsoft.com/en-us/previous-versions//ff793433(v=technet.10)?redirectedfrom=MSDN
# Make sure your MSDN license key matches your ISO and Windows Edition.

cscript //B "%windir%\system32\slmrg.vbs" -dli
cscript //B "%windir%\system32\slmgr.vbs" -upk JDJX-DKKDK-KDKD-DKKD-DKDK - Install Product Key 
cscript //B "%windir%\system32\slmgr.vbs" - ato - Activate Online 
cscript //B "%windir%\system32\slmgr.vbs" -ckms 
cscript //B "%windir%\system32\slmrg.vbs"

slui.exe - Activate via phone
-dli
slmgr.vbs -xpr 
slmgr.vbs /skms kms.xspace.in 
slmgr.vbs /dlv - Show details 

##---------------------------------------------------------------------------------------------------
Rename-Computer -NewName CN1 -LocalCredential WS\Administrator -PassThr
##---------------------------------------------------------------------------------------------------
Windows Features - https://www.windowsafg.com/features10.html
Windows Power Plan - https://www.windowsafg.com/power10.html
Windows Services - https://www.windowsafg.com/win10services.html
##---------------------------------------------------------------------------------------------------
## Optmize Services and Features 

net stop wuauserv
sc config WinDefend start= disabled
sc stop WinDefend
sc config wuauserv start= disabled
sc config Power start= disabled 
sc configiSCSI start= disabled
sc config Superfetch start= disabled
sc config Print Spooler start= disabled
sc config Themes start= disabled
sc config Software Protection start= disabled
sc config Remote Registry start= disabled
sc config Internet Connection Sharing start= disabled
sc config Windows Audio start= disabled
sc config Windows Color System start= disabled
sc config Plug and Play start= disabled
sc config BFE start= disabled
sc config CDPUserSvc_2437d start= disabled
sc config Spooler start= disabled
sc config Themes start= disabled
sc config CryptSvc start= disabled
sc config DPS start= disabled
sc config Schedule start= disabled
sc config Audiosrv start= disabled
sc config MpsSvc start= disabled
sc config FontCache start= disabled
sc config DoSvc start= disabled
sc config MapsBroker start= disabled
sc config wscsvc start= disabled
sc config OneSyncSvc_2437d start= disabled
sc config WSearch start= disabled
sc config CDPSvc start= disabled
sc config sppsvc start= disabled
sc config Power start= disabled
sc config SysMain start= disabled
sc config AudioEndpointBuilder start= disabled
sc config wscsvc start= disabled
sc config OneSyncSvc_2437d start= disabled
sc config WSearch start= disabled
##---------------------------------------------------------------------------------------------------
