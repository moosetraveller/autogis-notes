# Setup Linux
## Install Ubuntu 18.04
### Virtual Box
- https://www.virtualbox.org
- https://linuxhint.com/install_ubuntu_18-04_virtualbox

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

### Use Anaconda in a ZSH Console
Open `~/.zshrc` in a text editor, for example with nano:
```shell
nano ~/.zshrc
```
Add add the end of the file following two lines and restart your console.
```shell
.  ~/miniconda3/etc/profile.d/conda.sh
conda activate base
```

Check Conda with:
```shell
conda --version
```

## Install PyCharm for Anaconda
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
