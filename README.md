# Abaqus Student Edition (SE) on Linux with Wine
The [Abaqus Student Edition](https://edu.3ds.com/en/software/abaqus-student-edition) (SE) is available free of charge to anyone and can be downloaded from the [SIMULIA Community](https://r1132100503382-eu1-3dswym.3dexperience.3ds.com/#community:39/wiki:_NXifU43Q7yHzTiCX9yEaw). The Abaqus SE package contains:
- Abaqus/Standard,
- Abaqus/Explicit,
- Abaqus/CAE.

In the ABAQUS Student Edition the model size is limited up to 1000 nodes. The features like user subroutines and C++ ODB API are not available. Parallel execution is not available as well.

Abaqus SE files (\*.cae and \*.odb) are compatible with the academic version but not with commercial Abaqus releases.

The Abaqus SE is officially available on Windows platform only but it can be run successfully on Linux using Wine.

Please find below the procedure of Abaqus SE installation and running on Linux using [Wine](https://www.winehq.org/). The installer of the ABAQUS SE requires Microsoft Internet Explorer 10 but the Wine doesn't support MS IE 10 (or later). However, the Abaqus SE installer can be run in the alternative way to overcome it.

## Step 0. Install Wine

The newest stable version of Wine is recommenced. Abaqus Student Edition was tested with 0.5 and 0.7. To install Wine on your Linux machine please follow [instruction on WineHQ website](https://wiki.winehq.org/Wine_Installation_and_Configuration). Please find below an example of installation for Ubuntu 20.04:
```
$ wget -nc https://dl.winehq.org/wine-builds/winehq.key
$ sudo apt-key add winehq.key
$ sudo add-apt-repository 'deb https://dl.winehq.org/wine-builds/ubuntu/ focal main'
$ sudo apt install --install-recommends winehq-stable
```
Run the Wine configuration tool to initialize Wine environment for current user:
```
$ winecfg
```
When the Wine Configuration dialog appears, click Ok.

## Step 1. Download Abaqus Student Edition (SE)
Go to DS SIMULIA web site:     
   
[https://edu.3ds.com/en/software/abaqus-student-edition](https://edu.3ds.com/en/software/abaqus-student-edition)
   
and download Abaqus Student Edition on your disk.

## Step 2. Installation 

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
Follow the instructions of the installation program. The default installation `C:\SIMULIA` and temporary `C:\Temp` directories are recommended. Please ignore the error of documentation installation (click `Continue`) and next one (click `Ok`). Ignore the message about installation failure (click `Close`)

5. Import registry keys:
```
$ LANG=en_US.1252 wine64 cmd.exe /c regedit /c abq_se_install_wine.reg
```
6. Create alias to easily run Abaqus from command line:
```
$ alias abaqus='WINEDEBUG=-all LANG=en_US.1252 wine64 abaqus'
```
To automatically set up alias please use files like .bashrc, .bash_profile, .profile, etc.

## Step 3. Verify the installation:
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

## Step 4. Run Abaqus
```
$ abaqus cae
```
The installation procedure on Linux with Wine skips the documentation. The full documentation of Abaqus is available on [help.3ds.com](https://help.3ds.com/2021/English/DSSIMULIA_Established/SIMULIA_Established_FrontmatterMap/sim-t-SIMULIA_EstablishedDocSearchOnline.htm?contextscope=all).

# Disclaimers
1. "_The ABAQUS Student Edition (SE) is available free of charge to anyone wishing to get started with Abaqus._" (https://edu.3ds.com/en/software/abaqus-student-edition)
2. The Abaqus Student Edition (SE) is officially available on Windows platform only.
3. Running Abaqus Student Edition (SE) on Linux is not recommended or supported by DS SIMULIA.
4. You are running and using Abaqus Student Edition (SE) on Linux only on your own responsibility.
5. If any problems occur during installation or using Abaqus Student Edition (SE) on Linux do not report that to DS SIMULIA or DS Partners.
6. Abaqus/CAE requires OpenGL acceleration for working. Not all graphics cards are supported. If the Abaqus/CAE doesn't start, hangs or crash the incompatible graphics card or driver can be the reason.
7. The procedure of the Abaqus Student Edition (SE) installation and running on Linux with Wine doesn't modify in any way any copyright protected files of DS SIMULIA.
