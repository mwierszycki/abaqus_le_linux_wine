# Abaqus Student Edition (SE) on Linux with Wine
Installation and running [Abaqus Student Edition](https://edu.3ds.com/en/software/abaqus-student-edition) (SE) on Linux using [Wine](https://www.winehq.org/).

## Step 1. Install Wine

The newest stable version of Wine is recommenced. Abaqus Student Edition was tested with 0.5 and 0.7. To install Wine on your Linux machine please follow [instruction on WineHQ website](https://wiki.winehq.org/Wine_Installation_and_Configuration). Please find below an example of installation for Ubuntu 20.04:
```
$ wget -nc https://dl.winehq.org/wine-builds/winehq.key
$ sudo apt-key add winehq.key
$ sudo add-apt-repository 'deb https://dl.winehq.org/wine-builds/ubuntu/ focal main'
$ sudo apt install --install-recommends winehq-stable
```
## Step 2. Initialization of Wine environment
Run the Wine configuration tool to initialize Wine environment for current user:
```
$ winecfg
```
When the Wine Configuration dialog appears, click Ok.

## Step 3. Download Abaqus Student Edition (SE)
Go to DS SIMULIA web site:     
   
[https://edu.3ds.com/en/software/abaqus-student-edition](https://edu.3ds.com/en/software/abaqus-student-edition)
   
and download Abaqus Student Edition on your disk.

## Step 4. Installation 

1. Unzip downloaded file:
```
$ unzip Abaqus_2021.SIMULIA_Abaqus_Student.Windows64.1-1.zip
```
2. Change directory to `SIMULIA_Abaqus_Student.Windows64/1`:
```
$ cd SIMULIA_Abaqus_Student.Windows64/1
```
3. Download files required for installation (bat script and registry keys):
```
$ wget https://raw.githubusercontent.com/mwierszycki/abaqus_se_linux_wine/main/2021/abq_se_install_wine.reg
$ wget https://raw.githubusercontent.com/mwierszycki/abaqus_se_linux_wine/main/2021/abq_se_install_wine.bat
```
4. Run installation process:
```
$ LANG=en_US.1252 wine64 cmd.exe /c abq_se_install_wine.bat
```
Follow the instructions of the installation program. The default installation and temporary directories are recommended. Please ignore the error of documentation installation (click Continue) and next one (click Ok). Ignore the message about installation failure (click Close)
5. Import registry keys:
```
$ LANG=en_US.1252 wine64 cmd.exe /c regedit /c abq_se_install_wine.reg
```
6. Create alias to easily run Abaqus from command line:
```
$ alias abaqus='WINEDEBUG=-all LANG=en_US.1252 wine64 abaqus'
```
To automatically set up alias files like .bashrc, .bash_profile, .profile, etc. can be used.

## Step 5. Verify the installation:
```
$ abaqus info=ver

win32wnet error:  (1222, 'WNetOpenEnum', 'No network.')
Abaqus JOB abaqus
Abaqus Student Edition 2021
Abaqus Site ID: SE2021
Abaqus is located in the directory c:\SIMULIA\CAE\2021SE\win_b64\code\bin\SE c:\SIMULIA\CAE\2021SE c:\SIMULIA\CAE\2021SE\win_b64 c:\SIMULIA\CAE\2021SE\win_b64\code c:\SIMULIA\CAE\2021SE\win_b64\code\bin c:\SIMULIA\CAE\2021SE\wi
n_b64\code\bin\SMAExternal c:\SIMULIA\CAE\2021SE\win_b64\CAEresources c:\SIMULIA\CAE\2021SE\win_b64\SMA
Sequence Information:
    c:\SIMULIA\CAE\2021SE\win_b64: 2021_02_02-20.03.25 167982
The Abaqus information files are located in the directory c:\SIMULIA\CAE\2021SE\win_b64\SMA\info

Official Version: Abaqus Student Edition 2021
Internal Version: Abaqus Student Edition 6.21-6

Abaqus JOB abaqus COMPLETED
```
```
$ abaqus verify all

win32wnet error:  (1222, 'WNetOpenEnum', 'No network.')
------------------------------------------------------------

Abaqus Product Verification

2/12/2022 8:29:30 PM

------------------------------------------------------------

Verify test : Abaqus/Standard verification

     result : PASS

------------------------------------------------------------

Verify test : Abaqus/Explicit verification

  - 'Abaqus/Explicit single precision' completed, validation Succeeded

  - 'Abaqus/Explicit double precision' completed, validation Succeeded

     result : PASS

------------------------------------------------------------

Verify test : Abaqus/Foundation verification

     result : PASS

------------------------------------------------------------

Verify test : Abaqus parametric studies verification

  - 'Abaqus/Standard parametric studies' completed, validation Succeeded

  - 'Abaqus/Explicit parametric studies' completed, validation Succeeded

     result : PASS

------------------------------------------------------------

Verify test : Abaqus/CAE verification

     result : PASS

------------------------------------------------------------

Verify test : Abaqus/Viewer verification

     result : PASS

------------------------------------------------------------

Verify test : Abaqus scripting interface verification

     result : PASS

------------------------------------------------------------

Verify test : Abaqus noGUI (CAE/Viewer) verification

     result : PASS

------------------------------------------------------------

Verify test : Abaqus I/O performance

     result : PASS

------------------------------------------------------------

Verification procedure complete

2/12/2022 8:31:15 PM

------------------------------------------------------------
```
The error message `win32wnet error:  (1222, 'WNetOpenEnum', 'No network.')` comes from the Python for Win32 Extension module that exposes the Windows Networking API.  Since Abaqus doesn't require a network to run, that error can be ignored as well.

## Step 6. Run Abaqus
```
$ abaqus cae
```
