# NXT-NB
Jupyter notebooks for programming LEGO Mindstorms NXT in Python.

The code consists of [Jupyter notebooks](http://jupyter.org/) 
running locally in a laptop or desktop computer with Ubuntu Linux 
that communicates with the robots via Bluetooth.

The NXT is running its standard firmware.

## Prerequisites

* Ubuntu 22.04.3
* Python 3.10.12
* python3-venv
* python3-bluez 0.23
* libbluetooth-dev 5.64
* [Jupyter](https://jupyter.org/) 1.1.1
* [Matplotlib](https://matplotlib.org/) 3.10.9
* [NXT-Python](https://sr.ht/~ni/nxt-python/) 3.5.1

## Setup
```
sudo apt update && sudo apt install -y libbluetooth-dev python3-bluez python3-venv
python3 -m venv lego-nb
source lego-nb/bin/activate
python3 -m pip install jupyter==1.1.1 matplotlib==3.10.9 nxt-python==3.5.1
cp -R /usr/lib/python3/dist-packages/bluetooth/ lego-nb/lib/python3.10/site-packages/
cd lego-nb && git clone https://github.com/RobInLabUJI/NXT-NB.git
```

## Bluetooth pairing

Activate Bluetooth and pair your robot and computer:
```
bluetoothctl
scan on
pair <bt_mac_addr>
trust <bt_mac_addr>
exit
```
When requested, enter the PIN in your NXT and computer.

## Usage

### NXT

Switch it on, that's all!

### Computer
Terminal 1
```
sudo rfcomm connect 0 <bt_mac_addr> 1
sudo chmod 666 /dev/rfcomm0
```
Terminal 2
```
source lego-nb/bin/activate
cd lego-nb/NXT-NB
jupyter notebook --port=8888 --NotebookApp.port_retries=0 --no-browser \
                 --NotebookApp.token='' --ip 0.0.0.0
```
[Open the NXT notebook in your browser and enjoy!](http://localhost:8888/notebooks/NXT_notebook.ipynb)
