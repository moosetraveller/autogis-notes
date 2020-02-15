## Setup a GIS Environment on Ubuntu Linux
- https://github.com/moosetraveller/gis-test-env#setup-on-ubuntu-linux

## Setup a GIS Environment on Windows:
- https://github.com/moosetraveller/gis-test-env#setup-on-windows

## Setup a GIS Environment on Mac OS:
- https://github.com/moosetraveller/gis-test-env#setup-on-macos

----

# Setup on Ubuntu Linux
Note: This tutorial uses an older Ubuntu version. Use this tutorial at your own risk.
## Install Ubuntu 18.04
### Virtual Box
- https://www.virtualbox.org
- https://linuxhint.com/install_ubuntu_18-04_virtualbox

### Parallels
Note: If you use Parallels on Mac, go to your configuration and disable "Preserve text formatting" in Option/More Options.

## Install ZSH Console (optional)
- https://kifarunix.com/how-to-install-and-setup-zsh-and-oh-my-zsh-on-ubuntu-18-04/

## Install Anaconda
Change to your console and type:
```shell
cd ~/Downloads
wget https://repo.anaconda.com/archive/Anaconda3-2019.10-Linux-x86_64.sh
bash Anaconda3-2019.10-Linux-x86_64.sh
```
Follow the instructions and install Anaconda to `~/anaconda3`. If you are asked to initialize Conda do it. After the installation you need to restart your console.

Check Conda with:
```shell
conda --version
```

Sources:
- https://www.anaconda.com/

### Use Anaconda in a ZSH Console
Open `~/.zshrc` in a text editor, for example with nano:
```shell
nano ~/.zshrc
```
Add add the end of the file following two lines and restart your console.
```shell
.  ~/anaconda3/etc/profile.d/conda.sh
conda activate base
```

Check Conda with:
```shell
conda --version
```

### Sources
- https://stackoverflow.com/a/52029602/42659

## Install PyCharm for Anaconda
Note: You will need a licence for PyCharm. If you are student, sign up for the GitHub Student Pack and get a free Education licence.
```shell
cd ~/Downloads
wget https://download.jetbrains.com/python/pycharm-professional-anaconda-2019.3.3.tar.gz
sudo tar xfz pycharm-*.tar.gz -C /opt/
```
Start PyCharm with:
```shell
sh /opt/pycharm-anaconda-2019.3.3/bin/pycharm.sh
```
After PyCharm is started, go to  `Tools -> Create Desktop Entry...` to create a link in your Application list.

### Sources
- https://www.jetbrains.com/pycharm/promo/anaconda
- https://www.jetbrains.com/help/pycharm/installation-guide.html
- https://askubuntu.com/a/108794
- https://education.github.com/pack

## Install R
```shell
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E298A3A825C0D65DFD57CBB651716619E084DAB9
sudo add-apt-repository 'deb https://cloud.r-project.org/bin/linux/ubuntu bionic-cran35/'
sudo apt update
sudo apt install r-base
```
Test R with: `sudo -i R`.

### Sources
- https://www.digitalocean.com/community/tutorials/how-to-install-r-on-ubuntu-18-04

## Install QGIS
Add following lines to `/etc/apt/sources.list`:
```shell
deb     https://qgis.org/debian bionic main
deb-src https://qgis.org/debian bionic main
```
Then execute following commands in your terminal:
```shell
wget -O - https://qgis.org/downloads/qgis-2019.gpg.key | gpg --import
gpg --fingerprint 51F523511C7028C3
gpg --export --armor 51F523511C7028C3 | sudo apt-key add -
sudo apt-get update
sudo apt-get install qgis qgis-plugin-grass
```

## Prepare Conda Environment
### Setup Base Environment
```shell
cd ~
rm .condarc
conda config
conda config --add channels defaults
conda install geopandas jupyterlab
```
### Setup GIS Environment
```shell
conda create -n gis python=3.7
conda activate gis

conda install jupyterlab
conda install gdal

conda install geopandas matplotlib mapclassify
conda install -c conda-forge geojson contextily folium mplleaflet osmnx
conda install pysal rasterio
conda install dill
conda install -c conda-forge geoplot rasterstats

conda install psycopg2
conda install sqlalchemy
conda install -c conda-forge geoalchemy2

pip install urbanaccess pandana
pip install dash==0.19.0
pip install dash-renderer==0.11.1
pip install dash-html-components==0.8.0
pip install dash-core-components==0.14.0
pip install plotly --upgrade
```
#### Test Environment
```shell
python -c 'import gdal; print(dir(gdal))'
```
There should be also no error occuring when executing:
```python
import geopandas as gpd
import pysal
import cartopy
import geoplot
import osmnx
import folium
import dash
import rasterio
import osmnx
import contextily
import psycopg2
import sqlalchemy
import geoalchemy2
```

### Sources
- https://automating-gis-processes.github.io/site/course-info/Installing_Anacondas_GIS.html
- https://github.com/ContinuumIO/anaconda-issues/issues/10351#issuecomment-528378258 

## Install PosgreSQL/PostGIS
```shell
sudo apt update
sudo apt install postgresql postgresql-contrib
sudo apt-get install postgis

sudo -u postgres createuser --interactive -P # username: gisuser, password: gisuser
sudo -u postgres createdb --encoding=UTF8 --owner=gisuser gis
sudo -u postgres psql --username=postgres --dbname=gis -c "CREATE EXTENSION postgis;"
sudo -u postgres psql --username=postgres --dbname=gis -c "CREATE EXTENSION postgis_topology;"
```

### Set posgres Password
```shell
sudo -u postgres psql
```

Then type in `\password postgres` and follow prompt. After the password is set close with `\q`.

### Install pgAdmin4
```shell
wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -
echo "deb http://apt.postgresql.org/pub/repos/apt/ `lsb_release -cs`-pgdg main" |sudo tee  /etc/apt/sources.list.d/pgdg.list

sudo apt update
sudo apt install pgadmin4 pgadmin4-apache2
```
Change to `http://127.0.0.1/pgadmin4` and sign in with your credential you have set during the installation.

Add New Server
- Name: postgresql-local
- Description: Local PostgreSQL server
- Host address: 127.0.0.1
- Port: 5432
- Username: postgres
- Password: <empty> unless you have a password set

### Sources
- https://www.digitalocean.com/community/tutorials/how-to-install-and-use-postgresql-on-ubuntu-18-04
- https://wiki.openstreetmap.org/wiki/PostGIS/Installation
- https://computingforgeeks.com/how-to-install-pgadmin-4-on-ubuntu
- https://stackoverflow.com/a/12721020/42659

----

# Setup on Windows
## Install Python (optional, there is a Python build delivered with Anaconda)
Download Python 3.7.6 from the internet and install Python to `c:\apps\python-3.7.6`. 
- Keep path simple
- Customize Installation
  - Install pip
  - Install tcl/tk and IDLE
  - Install py launcher
- Do not add Python to your `PATH` environment variable
  - if already set by another application, remove all other Python versions from the `PATH` environment variable

### Sources
-  https://www.python.org/downloads/release/python-376

## Install Anaconda
Download Anaconda 3 from the internet and install Anaconda to `c:\apps\anaconda3`.
- Keep path simple
- Do not add Python to your `PATH` environment variable
  - if already set by another application, remove all other Python versions from the `PATH` environment variable
- Register Anaconda as the system Python 3.7 (not 2.7!)

### Sources
- https://www.anaconda.com/distribution
- https://medium.com/@GalarnykMichael/install-python-on-windows-anaconda-c63c7c3d1444

## Install PyCharm for Anaconda
Note: You will need a licence for PyCharm. If you are student, sign up for the GitHub Student Pack and get a free Education licence.

Install PyCharm for Anaconda.

### Sources
- https://www.jetbrains.com/pycharm/promo/anaconda
- https://education.github.com/pack

## Install R
Download R 3.6.2 from the internet and install Anaconda to `c:\apps\R-3.6.2`.

### Sources
- https://cran.r-project.org/bin/windows/base

## Install QGIS
Download OSGeo4W Network Installer (64 bit) and install the tools with the Express Desktop Install to `c:\apps\OSGeo4W`.
- Select all packages (QGIS, GDAL, GRASS GIS)

### Sources
- https://qgis.org/en/site/forusers/download.html

## Prepare Conda Environment
### Build Tools for Visual Studio
Note: This is required for certain packages.

Download and Install Build Tools for Visual Studio 2019. (Maybe an older version does work too.)
- Select "C++ build tools"

#### Source
- https://visualstudio.microsoft.com/downloads

### Setup Base Environment
Open the Anaconda Prompt (via Start Menu) and use following commands:
```shell
cd %userprofile%
conda config
conda config --add channels defaults
conda install geopandas jupyterlab
```
### Setup GIS Environment
```shell
conda create -n gis python=3.7
conda activate gis

conda install jupyterlab
conda install gdal

conda install geopandas matplotlib mapclassify
conda install -c conda-forge geojson contextily folium mplleaflet osmnx
conda install pysal rasterio
conda install dill
conda install -c conda-forge geoplot rasterstats

conda install psycopg2
conda install sqlalchemy
conda install -c conda-forge geoalchemy2

pip install urbanaccess pandana
pip install dash==0.19.0
pip install dash-renderer==0.11.1
pip install dash-html-components==0.8.0
pip install dash-core-components==0.14.0
pip install plotly --upgrade
```
#### Test Environment
```shell
python -c 'import gdal; print(dir(gdal))'
```
There should be also no error occuring when executing:
```python
import geopandas as gpd
import pysal
import cartopy
import geoplot
import osmnx
import folium
import dash
import rasterio
import osmnx
import contextily
import psycopg2
import sqlalchemy
import geoalchemy2
```

### Sources
- https://automating-gis-processes.github.io/site/course-info/Installing_Anacondas_GIS.html
- https://github.com/ContinuumIO/anaconda-issues/issues/10351#issuecomment-528378258 

----

# Setup on MacOS
## Install Anaconda
Change to your console and type:
```shell
cd ~/Downloads
wget https://repo.anaconda.com/archive/Anaconda3-2019.10-MacOSX-x86_64.sh
bash Anaconda3-2019.10-MacOSX-x86_64.sh
```
Follow the instructions and install Anaconda to `~/anaconda3`. If you are asked to initialize Conda do it. After the installation you need to restart your console.

Check Conda with:
```shell
conda --version
```

Sources:
- https://www.anaconda.com

## Install PyCharm for Anaconda
Note: You will need a licence for PyCharm. If you are student, sign up for the GitHub Student Pack and get a free Education licence.
```shell
cd ~/Downloads
wget https://download.jetbrains.com/python/pycharm-professional-anaconda-2019.3.3.dmg
```

Change in Finder to your `~/Downloads` and install Pycharm for Anaconda.

### Sources
- https://www.jetbrains.com/pycharm/promo/anaconda
- https://www.jetbrains.com/help/pycharm/installation-guide.html
- https://education.github.com/pack

## Prepare Conda Environment
### Setup Base Environment
```shell
cd ~
rm .condarc
conda config
conda config --add channels defaults
conda install geopandas jupyterlab
```
### Setup GIS Environment
```shell
conda create -n gis python=3.7
conda activate gis

conda install jupyterlab
conda install gdal

conda install geopandas matplotlib mapclassify
conda install -c conda-forge geojson contextily folium mplleaflet osmnx
conda install pysal rasterio
conda install dill
conda install -c conda-forge geoplot rasterstats

conda install psycopg2
conda install sqlalchemy
conda install -c conda-forge geoalchemy2
conda install -c conda-forge pandara

pip install urbanaccess pandana
pip install dash==0.19.0
pip install dash-renderer==0.11.1
pip install dash-html-components==0.8.0
pip install dash-core-components==0.14.0
pip install plotly --upgrade
```
#### Test Environment
```shell
python -c 'import gdal; print(dir(gdal))'
```
There should be also no error occuring when executing:
```python
import geopandas as gpd
import pysal
import cartopy
import geoplot
import osmnx
import folium
import dash
import rasterio
import osmnx
import contextily
import psycopg2
import sqlalchemy
import geoalchemy2
```

### Sources
- https://automating-gis-processes.github.io/site/course-info/Installing_Anacondas_GIS.html
- https://github.com/ContinuumIO/anaconda-issues/issues/10351#issuecomment-528378258 
