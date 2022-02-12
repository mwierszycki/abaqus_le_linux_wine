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
5. Import registry keys:
```
$ LANG=en_US.1252 wine64 cmd.exe /c regedit /c abq_se_install_wine.reg
```
6. Create alias to easily run Abaqus from command line:
```
$ alias abaqus='WINEDEBUG=-all LANG=en_US.1252 wine64 abaqus'
```
## Step 5. Verify the installation:
```
$ abaqus info=ver
$ abaqus verify all
```
## Step 6. Run Abaqus
```
$ abaqus cae
```
