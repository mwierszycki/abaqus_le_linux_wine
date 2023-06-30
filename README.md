# Abaqus Learning Edition (former Student Edition) on Linux with Wine
The [Abaqus Learning Edition](https://edu.3ds.com/en/software/abaqus-learning-edition) is available free of charge to anyone and can be downloaded from the [SIMULIA Community](https://r1132100503382-eu1-3dswym.3dexperience.3ds.com/#community:39/wiki:_NXifU43Q7yHzTiCX9yEaw). The Abaqus Learning Edition package contains:
- Abaqus/Standard,
- Abaqus/Explicit,
- Abaqus/CAE.

In the ABAQUS Learning Edition the model size is limited up to 1000 nodes. The features like user subroutines and C++ ODB API are not available. Parallel execution is not available as well.

Abaqus Learning Edition files (\*.cae and \*.odb) are compatible with the academic version but not with commercial Abaqus releases.

The Abaqus Learning Edition is officially available on Windows platform only but it can be run successfully on Linux using Wine.

Please find below the procedure of Abaqus Learning Edition installation and running on Linux using [Wine](https://www.winehq.org/). The installer of the ABAQUS Learning Edition requires Microsoft Internet Explorer 10 but the Wine doesn't support MS IE 10 (or later). However, the Abaqus Learning Edition installer can be run in the alternative way to overcome it.

## Install Wine

The newest stable version of Wine is strongly recommended. Abaqus Learning Edition was tested with Wine 0.7. To install Wine on your Linux machine please follow [instruction on WineHQ website](https://wiki.winehq.org/Wine_Installation_and_Configuration). Please find below an example of installation for Ubuntu 20.04:
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

## Download Abaqus Learning Edition
Go to DS SIMULIA web site:     
   
[https://edu.3ds.com/en/software/abaqus-learning-edition](https://edu.3ds.com/en/software/abaqus-learning-edition)
   
and download Abaqus Learning Edition on your disk.

## Install Abaqus Learning/Student Edtion

Follow the installation guide for selected release:

* [Abaqus 2021 Student Edition](https://github.com/mwierszycki/abaqus_se_linux_wine/tree/main/2021)
* [Abaqus 2022 Learning Edition](https://github.com/mwierszycki/abaqus_se_linux_wine/tree/main/2022)
* [Abaqus 2023 Learning Edition](https://github.com/mwierszycki/abaqus_se_linux_wine/tree/main/2023)

# Disclaimers
1. "_The ABAQUS Learning Edition is available free of charge to anyone wishing to get started with Abaqus_" (https://edu.3ds.com/en/software/abaqus-learning-edition)
2. The Abaqus Student/Learning Edition is officially available on Windows platform only.
3. Running Abaqus Student/Learning Edition on Linux is not recommended or supported by DS SIMULIA.
4. You are running and using Abaqus Student/Learning Edition on Linux only on your own responsibility.
5. If any problems occur during installation or using Abaqus Student/Learning Edition on Linux do not report that to DS SIMULIA or DS Partners.
6. Abaqus/CAE requires OpenGL acceleration for working. Not all graphics cards are supported. If the Abaqus/CAE doesn't start, hang or crash the incompatible graphics card or driver can be the reason.
7. The procedure of the Abaqus Student/Learning Edition installation and running on Linux with Wine doesn't modify in any way any copyright protected files of DS SIMULIA.
