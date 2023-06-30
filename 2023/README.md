## Abaqus Learning Edtion 2023 installation

Note: [Install and configure Wine](https://github.com/mwierszycki/abaqus_se_linux_wine/blob/main) before start to install Abaqus Learning Edtion 2023

1. The JRE 17 must be installed under Wine before Abaqus LE installation is run. Download [OpenJDK 17 (LTS) OpenJ9](https://github.com/ibmruntimes/semeru17-binaries/releases/download/jdk-17.0.7%2B7_openj9-0.38.0/ibm-semeru-open-jre_x64_windows_17.0.7_7_openj9-0.38.0.zip) from AdoptOpenJDK Github (ZIP file) and extract it to `C:\jre` (`~/.wine/drive_c/jre/`):

2. Unzip the downloaded Abaqus Learning Edtion 2023 installation files:
```
$ unzip Abaqus_2023.AM_SIM_Abaqus_Learning.Windows64.1-1.zip
```
3. Change directory to `AM_SIM_Abaqus_Learning.Windows64/1/`:
```
$ cd AM_SIM_Abaqus_Learning.Windows64/1/
```
4. Download files required for installation (bat script and registry keys):
```
$ wget https://raw.githubusercontent.com/mwierszycki/abaqus_se_linux_wine/main/2023/abq_le_install_wine.reg
$ wget https://raw.githubusercontent.com/mwierszycki/abaqus_se_linux_wine/main/2023/abq_le_install_wine.bat
```
5. Run installation process:
```
$ LANG=en_US.1252 wine64 cmd.exe /c abq_le_install_wine.bat
```
The installer with text interface is run - follow the instructions of the installation program. The default installation `C:\SIMULIA` and temporary `C:\Temp` directories are recommended. Set `c:\jre` as Java Runtime Enviroment (JRE) path. Please ignore the errors of documentation installation (type `2`) and next ones (type `1`). Ignore the message about installation failure (press `Enter`)

6. Import registry keys:
```
$ LANG=en_US.1252 wine64 cmd.exe /c regedit /c abq_le_install_wine.reg
```
7. Create alias to easily run Abaqus from command line:
```
$ alias abaqus='WINEDEBUG=-all LANG=en_US.1252 wine64 abaqus'
```
To automatically set up alias please use files like .bashrc, .bash_profile, .profile, etc.

8. Verify the installation:
```
$ abaqus info=ver
win32wnet error:  (1222, 'WNetOpenEnum', 'No network.')
Abaqus JOB abaqus
Abaqus Learning Edition 2023
Abaqus Site ID: LE2023
Abaqus is located in the directory c:\SIMULIA\CAE\2023LE\win_b64\code\bin\LE c:\SIMULIA\CAE\2023LE c:\SIMULIA\CAE\2023LE\
win_b64 c:\SIMULIA\CAE\2023LE\win_b64\code c:\SIMULIA\CAE\2023LE\win_b64\code\bin c:\SIMULIA\CAE\2023LE\win_b64\code\bin\
SMAExternal c:\SIMULIA\CAE\2023LE\win_b64\CAEresources c:\SIMULIA\CAE\2023LE\win_b64\SMA
Sequence Information:
    c:\SIMULIA\CAE\2023LE\win_b64: 2023_03_20-20.15.03 RELr425 183417
The Abaqus information files are located in the directory c:\SIMULIA\CAE\2023LE\win_b64\SMA\info

Official Version: Abaqus Learning Edition 2023
Internal Version: Abaqus Learning Edition 6.23-3

Abaqus JOB abaqus COMPLETED

$ abaqus verify all
win32wnet error:  (1222, 'WNetOpenEnum', 'No network.')
------------------------------------------------------------

Abaqus Product Verification

6/30/2023 11:27:12 PM

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

6/30/2023 11:29:03 PM

------------------------------------------------------------
```

9. Run Abaqus
```
$ abaqus cae
```
Note: The installation procedure on Linux with Wine skips the documentation. The full documentation of Abaqus is available on [help.3ds.com](https://help.3ds.com/2023/English/DSSIMULIA_Established/SIMULIA_Established_FrontmatterMap/sim-t-SIMULIA_EstablishedDocSearchOnline.htm?contextscope=all).
