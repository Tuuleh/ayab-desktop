# AYAB - All Yarns Are Beautiful

This is the GUI interface for AYAB.

For information on how to install the release version of the software, see
[http://manual.ayab-knitting.com](http://manual.ayab-knitting.com)

## Running from Source & Development

The AYAB desktop software runs using Python 3.6. This is not the current
version of Python, so it is recommended to install the software to a
virtual environment. Miniconda provides a virtual environment that is
platform-independent and easy to use: download the lastest version from
https://docs.conda.io/en/latest/miniconda.html and follow the installation
instructions for your operating system.

The Python module dependencies can be found in *requirements.txt*.

This repository uses [pre-commit](https://pre-commit.com/) hooks.
After cloning the repo and installing the requirements, you should run
`pre-commit install` to set up the git hook scripts.

### Linux

For flashing the firmware, avrdude has to be available on your system.
To be able to work on GUI elements and translation files, the Qt Dev tools are
needed also.

#### Debian/Ubuntu

    sudo apt-get install python3-pip python3-dev python3-virtualenv python3-gi
    sudo apt-get install libasound2-dev avrdude qttools5-dev-tools

#### For openSUSE

    sudo zypper install python3-pip python3-virtualenv python3-gi
    sudo zypper install libasound avrdude qttools5-dev-tools

#### All Distributions

To be able to communicate with your Arduino, it might be necessary to add the
rights for USB communication by adding your user to some groups.

    sudo usermod -aG tty [userName]
    sudo usermod -aG dialout [userName]

To install the development version you can checkout the git repository.

    git clone https://github.com/AllYarnsAreBeautiful/ayab-desktop
    cd ayab-desktop

Create a virtual environment for AYAB:

    conda create --name ayab -c conda-forge python=3.6.* pip

Now activate the virtual environment. The command prompt should now display
`(ayab)` at the beginning of each line.

    conda activate ayab

Install the remaining prerequisites.

    python -m pip install --upgrade pip
    pip install --upgrade setuptools
    pip install --ignore-installed -r requirements.txt
    bash setup-environment.sh

Now start AYAB with

    python -m fbs run

### Windows

Run Anaconda Powershell as administrator and install git.

    conda install git

Now you can download the git repository with:

    git clone https://github.com/AllYarnsAreBeautiful/ayab-desktop
    cd ayab-desktop

Next, create a virtual environment for AYAB:

    conda create --name ayab -c conda-forge python=3.6.* pip

Activate the virtual environment. The command prompt should now display
`(ayab)` at the beginning of each line.

    conda activate ayab

Install the prerequisite Python modules.

    python -m pip install --upgrade pip
    pip install --upgrade setuptools
    pip install --ignore-installed -r requirements.txt

To be able to work on GUI elements and translation files, the Qt Dev tools are needed:

    https://download.qt.io/archive/qt/5.12/5.12.12/qt-opensource-windows-x86-5.12.12.exe

Convert the PyQt5 `.ui` files and generate the translation files:

    pwsh setup-environment.sh

Download and install Qt5 from (this link)[https://download.qt.io/archive/qt/5.12/5.12.12/qt-opensource-windows-x86-5.12.12.exe]
and create the remaining files:

Finally, the `fbs` module needs a small patch.

    conda install -c free patch
    $dir = $(pwd).Path
    cd $Env:CONDA_PREFIX\Lib\site-packages\fbs\
    patch -u -i $dir\windows-build\patch-fbs.diff _defaults\src\installer\windows\Installer.nsi

Now start AYAB with:

    python -m fbs run

### macOS

You can install Git using Homebrew:

    brew install git

You will also need the Xcode command line tools:

    xcode-select --install

Next download the git repository:

    git clone https://github.com/AllYarnsAreBeautiful/ayab-desktop
    cd ayab-desktop

Create a virtual environment for AYAB:

    conda create --name ayab -c conda-forge python=3.6.* pip

Now activate the virtual environment. The command prompt should now display
`(ayab)` at the beginning of each line.

    conda activate ayab

Then install the remaining prerequisites with:

    python -m pip install --upgrade pip
    pip install --upgrade setuptools
    pip install -r requirements.txt

To solve pip SSL:TLSV1_ALERT_PROTOCOL_VERSION problem:

    curl https://bootstrap.pypa.io/get-pip.py | python

To be able to work on GUI elements and translation files, the Qt Dev tools are needed also:

    https://download.qt.io/archive/qt/5.12/5.12.12/qt-opensource-mac-x64-5.12.12.dmg

Finally, convert the PyQt5 `.ui` files and generate the translation files:

    bash setup-environment.sh

Now start AYAB with

    python -m fbs run

