# peak-particle-velocity
### Raspberry Shake Peak Particle Velocity (PPV) calculation script

*Coded by Giuseppe Petricca (@gmrpetricca)*

[![GitHub](https://img.shields.io/github/license/raspishake/rsudp)](https://github.com/raspishake/rsudp/blob/master/LICENSE)

This script will read data from a 3D unit on the Raspberry Shake AM network (or in stand-alone mode) and convert the output displacement (in mm) into Ground Vibration measurement (PPV - in mm/s). 

The source for the conversion formula is [here](https://www.castlegroup.co.uk/guidance/ground-vibration/ground-vibration/).

![Example output](img/PPVMotion_R55F8.png)

Required software and packages:
- Python 3
- Jupyter
- Obspy
- Matplotlib
- Numpy

For the offline version two more packages are needed:
- datetime
- paramiko

Installation via Anaconda (online version):
```bash
# install the environment with the correct software:
conda create -n ppvmotion python=3 jupyter jupyterlab matplotlib obspy numpy
# activate the environment
conda activate ppvmotion
# navigate to the folder where you have the Python code via command prompt
cd -local address of the Python folder-
# start Jupyter Lab
jupyter lab

Installation via Anaconda (offline version):
```bash
# install the environment with the correct software:
conda create -n ppvmotion python=3 jupyter jupyterlab matplotlib obspy numpy paramiko
# activate the environment
conda activate ppvmotion
# navigate to the folder where you have the Python code via command prompt
cd -local address of the Python folder-
# start Jupyter Lab
jupyter lab
```

Once this is done, it is possible to open one of the two `.ipynb` files in the repository: 
- [PPVmotion-online.ipynb](online/PPVmotion-online.ipynb) for when the station is connected to the network
- [PPVmotion-offline.ipynb](offline/PPVmotion-offline.ipynb) for when the station is in stand-alone mode

Some data are provided in the offline folder for testing purposes. Please keep the folder structure as it is.

The ```station.xml``` provided file is for a RS3D V5 Shake unit. Different Shakes will reqiuire different files, they can be found [here](https://manual.raspberryshake.org/metadata.html#templates-for-manual-metadata-generation).

The file is commented throughout the various steps, however, this is a brief guide to use it: 

1. Insert a valid Raspberry Shake 3D (RS3D) unit code
2. Insert a valid start and end time references for the script to work. The format is "YYYY-MM-DDThh:mm:ss.ddd"
3. If needed, modify the values for the filtering process (the default is a bandpass filter between 0.7 Hz and 2.0 Hz)
4. The filter can also be removed by commenting out (with ```#```) line 48 of the online script or line 94 of the offline script ```st.filter("bandpass", freqmin=f1, freqmax=f2, corners=cor)```

Done! Executing the script will create and save a plot which whill show the Peak Particle Velocity (in mm/s) for each channel (EHZ, EHN, EHE) of the selected RS3D unit.


