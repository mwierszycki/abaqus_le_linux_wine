# Abaqus Student Edition (SE) on Linux with Wine
Installation and running [Abaqus Student Edition](https://edu.3ds.com/en/software/abaqus-student-edition) (SE) on Linux using [Wine](https://www.winehq.org/).

1. Install Wine
```
$ sudo apt install -y wine | sudo yum install -y wine
```
2. Run the Wine configuration tool to initiallizate Wine enviroment for current user:
```
$ winecfg
```
3. Download Abaqus Student Edition (SE) from DS SIMULIA web site:
[https://edu.3ds.com/en/software/abaqus-student-edition](https://edu.3ds.com/en/software/abaqus-student-edition)

4 Unzip downloaded file:
```
$ unzip Abaqus_2021.SIMULIA_Abaqus_Student.Windows64.1-1.zip
```
5. Change directory to `SIMULIA_Abaqus_Student.Windows64/1`:
```
$ cd SIMULIA_Abaqus_Student.Windows64/1
```
6. Download files required for installation (bat script and registry keys):
```
$ wget https://raw.githubusercontent.com/mwierszycki/abaqus_se_linux_wine/main/2021/abq_se_install_wine.reg
$ wget https://raw.githubusercontent.com/mwierszycki/abaqus_se_linux_wine/main/2021/abq_se_install_wine.bat
```
7. Run installation process:
```
$ LANG=en_US.1252 wine64 cmd.exe /c abq_se_install_wine.bat
$ LANG=en_US.1252 wine64 cmd.exe /c regedit /c abq_se_install_wine.reg
```
8. Create alias to easly run Abaqus from command line:
```
$ alias abaqus='WINEDEBUG=-all LANG=en_US.1252 wine64 abaqus'
```
9. Verify the installation:
```
$ abaqus info=ver
$ abaqus verify all
```
10. Run Abaqus:

```
$ abaqus cae
```
